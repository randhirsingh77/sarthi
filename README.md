# Sarthi

An AI chat app for Indian students and job-seekers.

Sarthi takes its concept from [LibreChat](https://github.com/danny-avila/LibreChat) — a self-hosted, multi-model AI chat interface — and scopes it down to what students and job-seekers in India actually need every day: study help, exam answers, and job preparation, with costs kept visible in rupees.

> **Status:** Planning — build starts after my STET exam (Nov 2026). No code yet; this repo currently holds the plan. Everything here will be written from scratch — LibreChat is a reference for features and architecture, not a source to copy from.

## What it will do

- Chat with multiple LLM providers through one interface, with streaming replies
- Conversations you can save, search, and organise
- Presets for common tasks (study, revision, interview prep)
- Token and cost tracking shown in ₹, so usage never surprises you

## Planned differentiators (first five)

1. **Resume-vs-JD analyser** — compare a resume against a job description and show the gaps
2. **Mock Interview Mode** — practice interviews with follow-up questions
3. **Exam-Answer Modes** — answers shaped for exam marking schemes, not just chat
4. **Hinglish / Samjhao** — explain in simple Hinglish when English gets in the way
5. **₹ smart routing** — pick the cheapest provider that can handle the task

## Tech stack

- **Frontend:** React + TypeScript
- **Backend:** Express (Node.js)
- **Database:** MongoDB
- **Providers:** Gemini first, then Groq and OpenRouter (free tiers), behind a provider-adapter layer

## Scope: essentials only

JWT auth, conversation CRUD, markdown chat UI, SSE streaming, provider adapters, presets, token/₹ cost tracking, search, and deployment.

## Deliberately cut (for now)

Real RAG, agents/MCP, code interpreter, image generation, SSO, and an admin panel. These are out of scope for v1 and are named here so the scope stays honest.

## Roadmap

An 8-week build plan lives in `docs/roadmap.md` (coming with the docs). The build checklist, differentiators, and interview Q&A are tracked alongside the project plan.

## License

MIT — see `LICENSE` (to be added with the first code).
