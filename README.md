# Sarthi

An AI chat app for Indian students and job-seekers.

I'm building Sarthi by taking the concept from [LibreChat](https://github.com/danny-avila/LibreChat) — a self-hosted, multi-model AI chat interface — and scoping it down to what students and job-seekers in India actually need every day: study help, exam answers, and job preparation, with costs kept visible in rupees.

> **Status:** Planning. No code yet; this repo currently holds the design docs. LibreChat is my reference for features and architecture — all code here will be my own, written from scratch.

## What it will do

- Chat with multiple LLM providers through one interface, with streaming replies
- Conversations you can save, search, and organise
- Presets for common tasks (study, revision, interview prep)
- Token and cost tracking shown in ₹, so usage never surprises you

## Planned features

1. **Resume-vs-JD analyser** — compare a resume against a job description and show the gaps
2. **Mock Interview Mode** — practice interviews with follow-up questions
3. **Exam-Answer Modes** — answers shaped for exam marking schemes, not just chat
4. **Hinglish / Samjhao** — explain in simple Hinglish when English gets in the way
5. **₹ smart routing** — pick the cheapest provider that can handle the task

The full feature list is in `docs/features.md`; the design is in `docs/architecture.md`.

## Tech stack

- **Frontend:** React + TypeScript
- **Backend:** Express (Node.js)
- **Database:** MongoDB
- **Providers:** Gemini first, then Groq and OpenRouter (free tiers), behind a provider-adapter layer

## Scope: essentials only

JWT auth, conversation CRUD, markdown chat UI, SSE streaming, provider adapters, presets, token/₹ cost tracking, search, and deployment.

## Out of scope for v1

Real RAG, agents/MCP, code interpreter, image generation, SSO, and an admin panel.

## License

MIT — see `LICENSE` (to be added with the first code).
