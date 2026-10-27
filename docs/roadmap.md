# Roadmap

Product phases for Sarthi, in build order. Each phase ships when its
milestone is met; this is a product order, not a calendar.

## Phase 1 — Core chat

The essentials from the README and `docs/architecture.md`:

- JWT auth and user accounts
- Conversation CRUD, search, and organisation
- Markdown chat UI with SSE streaming replies
- Provider adapters: Gemini first, then Groq and OpenRouter
- Presets for common tasks (study, revision, interview prep)
- Token and ₹ cost tracking per chat
- Deployment

**Milestone:** a usable multi-provider chat app with saved, searchable
conversations and visible ₹ costs.

## Phase 2 — First differentiators

The five features listed as planned for v1 in `docs/features.md`:

- Resume-vs-JD Gap Analyser
- Mock Interview Mode
- Exam-Answer Modes
- Hinglish + Language Toggle & "Samjhao" button
- ₹ Cost-Aware Smart Routing

**Milestone:** Sarthi answers the two daily jobs — exam prep and job
prep — in a way a generic chat app does not.

## Phase 3 — Study and placement prep

The remaining study-focused features from `docs/features.md`:

- Hint-Ladder DSA Coach
- Notes → Flashcards & MCQ Quiz
- Placement Prep Planner
- Application Content Studio

**Milestone:** a full prep loop — learn, revise, practise, and apply —
inside one app.

## Phase 4 — Sharing and access

- Voice-First PWA Mode (installable, voice input/output, lite chat view)
- Study-Room Share Links (read-only links classmates can open and fork)
- Cited-Answers Mode (numbered citations from a quick web search)

**Milestone:** Sarthi works on the go, offline-friendly, and shareable
between classmates.

## Beyond v1

Deliberately out of scope for v1, and only reconsidered once Phases 1–4
are done: real RAG, agents/MCP, code interpreter, image generation, SSO,
and an admin panel.
