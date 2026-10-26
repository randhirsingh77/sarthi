# Architecture

> Planning document. No code exists yet. This doc describes the design
> the build will follow, so the code can be written against it rather
> than improvised.

Sarthi is a scoped, original AI chat app for Indian students and
job-seekers: one chat window for several LLM providers, with study and
placement-prep modes that the reference product (LibreChat) does not have.
It is not a copy of LibreChat — LibreChat is the reference for the feature
list and the architecture shape only.

## Stack

| Layer | Choice |
|---|---|
| Frontend | React + TypeScript |
| Backend | Express (Node.js) |
| Database | MongoDB |
| AI providers | Gemini first, then Groq and OpenRouter (all on free tiers) |
| Streaming | Server-Sent Events (SSE) |
| Deployment (planned) | Client on Vercel, API on Render |

The stack is deliberately the same shape as the reference's: a React client,
an Express API, and MongoDB — one consistent stack across client and server.

## Layout

Monorepo-lite — one repo, two packages, no workspace tooling until it is
needed:

```
sarthi/
  client/     # React + TypeScript chat UI
  server/     # Express + TypeScript API
  docs/       # architecture.md (this file), features.md, roadmap.md
```

TypeScript on both sides, ESLint, and a `.env.example` on the server.
API keys live only in the server `.env` — never in the frontend or in Git.

## How a chat message flows

1. The user sends a message from the chat screen. The client saves nothing
   locally as the source of truth; it POSTs to the API.
2. The API saves the user message to MongoDB, then calls the selected
   provider adapter with the conversation history.
3. The provider streams tokens back. The API forwards them to the client
   as Server-Sent Events, so the answer renders token by token.
4. When the stream ends, the API saves the full assistant message —
   including token usage — and the client stops rendering.

The non-streaming version comes first (send → wait → save reply), then
streaming replaces the wait. Getting the boring version working before the
streaming version is a deliberate sequencing choice.

## Why SSE, not WebSockets

Chat replies are one-way: server to client. SSE runs over plain HTTP, works
through proxies, and needs no socket server to scale. WebSockets would only
earn their complexity for true two-way features (live study rooms, typing
indicators) — those are stretch goals, not v1.

### Streaming states the UI must handle

- Streaming in progress, with a **Stop** button.
- **Stop pressed**: the client aborts its fetch, the server aborts the
  provider request, and the partial message is saved marked as stopped.
- **Retry / regenerate**: re-runs the same prompt through the adapter.
- **Provider down or timed out**: a clean error message plus Retry — never
  a spinner that runs forever.

## Provider adapter pattern

This is the core design decision of the project. The chat code never talks
to Gemini or Groq directly. It talks to one interface:

```
sendMessage(messages, options) -> stream of tokens + usage
```

Each provider gets one adapter behind that interface: a Gemini adapter
first, then Groq (and later OpenRouter, which speaks the OpenAI-compatible
shape). Adding a model means adding an adapter; the UI and the database
never change. The model picker in the UI and the saved presets both sit on
top of this layer.

If a provider fails, the adapter layer can fall back to the next provider —
the reliability twin of the ₹ smart-routing differentiator.

## API shape (planned)

REST, with every route protected by JWT auth except register/login:

| Area | Endpoints |
|---|---|
| Auth | `POST /auth/register`, `POST /auth/login`, token refresh |
| Conversations | `GET /conversations`, `POST /conversations`, `PATCH /conversations/:id`, `DELETE /conversations/:id` |
| Chat | `POST /conversations/:id/messages` (SSE stream) |
| Presets | CRUD under `/presets` |
| Search | `GET /conversations/search?q=...` (by title) |

Conversations are always filtered by the user id from the verified token —
never by a user id taken from the request body.

## Authentication

Register/login with bcrypt-hashed passwords, a short-lived JWT access
token plus a refresh token in an httpOnly cookie, and middleware that
verifies the token on every protected route. The same middleware enforces
the per-user rate limit and daily token budget (see Cost below).

## MongoDB schemas

### User

- `email` (unique), `passwordHash`
- `createdAt`

### Conversation

- `userId` (index with `updatedAt`, newest-first sidebar sorting)
- `title` (renamed from the first message; searchable)
- `model` (the provider/model this chat uses)
- `presetId` (optional — which preset started this chat)
- `createdAt`, `updatedAt`

### Message

- `conversationId`
- `role` (`user` | `assistant`)
- `content` (markdown; rendered XSS-safe — see Security)
- `parentId` (nullable; reserved for future branching/edit-resubmit)
- `tokens` — prompt/completion token counts from the provider
- `costEstimate` — estimated ₹ cost, from the static price table
- `stopped` (boolean — true if the user stopped the stream mid-way)
- `createdAt`

### Preset

- `userId`
- `name` (e.g. "DBMS tutor")
- `systemPrompt` (the hidden instruction that sets the assistant's role)
- `model`, plus generation parameters
- Presets power half the differentiators later: Mock Interview and
  Exam-Answer Modes are presets with strict output rules plus, where
  needed, a second scoring call.

### UsageRecord

- `userId`, `date`
- `tokensUsed`, `estimatedCost` (₹)
- Aggregated per user per day for the budget meter. Before each call, the
  API checks the user's daily budget; the UI shows the meter so the cost
  is visible, not a surprise.

## Token and ₹ cost tracking

Provider responses include usage (prompt and completion tokens). The API
stores those counts per message, computes `cost = tokens × model price`
from a static price table, and aggregates per user per day. The same
records feed the ₹ smart-routing differentiator: simple questions go to a
cheap/fast model, hard ones (coding, interviews) to the strong model.

## Long conversations and context limits

History cannot grow forever — a model has a context limit. The planned
approach is to send the last N messages, and to name the trade-off if that
changes (summarising older messages instead of truncating them) when the
build reaches it.

## Security notes

- **API keys**: server `.env` only. The browser never sees them; every AI
  call goes through the Express API, which enforces login, rate limits,
  and budgets.
- **Markdown/XSS**: AI answers are markdown and may contain HTML. Never
  inject raw HTML — render with a sanitiser (DOMPurify) and escape code
  blocks properly.
- **Quota abuse**: per-user daily token budget in Mongo, checked before
  each call, plus rate-limiting middleware. One user cannot burn the
  whole free tier.
- **Ownership**: every read and write is scoped to the token's user id.
  A user must never read another user's conversations, presets, or usage.

## Testing plan

Jest + Supertest for the API (auth, conversations, chat) with the provider
adapter mocked — fake stream of chunks, so tests are deterministic and cost
nothing. Mocking the provider is a deliberate choice: real calls would
make tests slow, flaky, and expensive.

## What is deliberately not in v1

Real RAG/vector search (the reference runs it as a separate Python service
— this project's PDF features use full-text-in-prompt within limits
instead), AI agents/MCP, a code-interpreter sandbox, image generation,
SSO/LDAP, an admin panel, and paid speech APIs. See the README for the
v1 scope.

## Related docs

- `features.md` — the full feature list.
- `roadmap.md` — the build roadmap.
