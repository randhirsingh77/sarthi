# Features — differentiators

Sarthi is a LibreChat-style AI chat app, but aimed at Indian students and
job-seekers. The essentials (auth, conversations, markdown chat UI, SSE
streaming, provider adapters, presets, token/₹ cost tracking, search) are
the base. The features below are what make it different from LibreChat —
they are the planned extras, not features that are built yet.

Status: planning. Build starts after my STET exam (Nov 2026). The build
order below is the plan, not a changelog.

## Recommended first five

These five are the planned first set (weeks 6–7 of the build plan):

1. **Resume-vs-JD Gap Analyser** — Upload a resume PDF and paste a job
   description; get matched/missing skills, an ATS-style score and
   bullet-point fixes, saved per application.
2. **Mock Interview Mode** — Pick a role/company type; the AI asks one
   question at a time, scores each answer against a rubric, and produces
   a final report with score history.
3. **Exam-Answer Modes** — One tap on any answer: a 5-mark short version,
   a 13-mark detailed version, "simple English", or "Hindi me samjhao".
4. **Hinglish + Language Toggle & "Samjhao" button** — UI and answer
   language switch (Hindi first); every answer gets a "Samjhao (explain
   simply)" button.
5. **₹ Cost-Aware Smart Routing** — Show the estimated ₹ cost per chat;
   simple questions go to a cheap/fast model, hard ones (coding,
   interviews) to the strong model; a daily budget meter caps spend.

## All twelve differentiators

| # | Feature | Scope | Difficulty |
|---|---------|-------|------------|
| 1 | Resume-vs-JD Gap Analyser | Resume PDF text + pasted JD → matched/missing skills, ATS-style score, bullet fixes, saved per application | Easy–Med |
| 2 | Mock Interview Mode | Role/company picker → one question at a time → rubric-scored answers → final report + score history | Easy |
| 3 | Hint-Ladder DSA Coach | Paste a DSA problem → Hint 1 → Hint 2 → approach → code, never the solution first; edge-case quiz at the end | Easy |
| 4 | Notes → Flashcards & MCQ Quiz | Semester PDF notes → flashcards + MCQs as revisable decks with simple spaced repetition | Medium |
| 5 | Exam-Answer Modes | One-tap rewrites: 5-mark short, 13-mark detailed, simple English, Hindi me samjhao | Very easy |
| 6 | Hinglish + Language Toggle & "Samjhao" button | Language switch for UI and answers; "Samjhao" re-explains any answer simply | Easy |
| 7 | ₹ Cost-Aware Smart Routing | Per-chat ₹ estimate, cheap/fast model for simple questions, strong model for hard ones, daily budget meter | Medium |
| 8 | Placement Prep Planner | "45 days to my interview" → day-by-day checklist (DSA, aptitude, CS fundamentals) with ticks and streaks | Easy–Med |
| 9 | Application Content Studio | One-click generators fed by the saved resume: Naukri profile summary, Internshala answers, LinkedIn About, referral message, cover letter | Very easy |
| 10 | Voice-First PWA Mode | Installable app, voice input/output via the browser's free Web Speech API, lite chat view, answers downloadable as small text files for offline revision | Easy–Med |
| 11 | Study-Room Share Links | Read-only share link to a conversation (e.g. a class DBMS revision chat) that classmates can open and fork; live rooms only as a stretch goal | Medium |
| 12 | Cited-Answers Mode | Toggle: answers must carry numbered citations from a quick web search, flagging anything that could not be sourced | Medium |

## Why these, in interview terms

- **Resume-vs-JD Gap Analyser** — PDF text extraction, structured JSON
  prompting, schema design. Directly useful to anyone watching the demo.
- **Mock Interview Mode** — Two-stage prompting (ask, then score), state
  over a conversation, data modelling for scores.
- **Hint-Ladder DSA Coach** — Prompt orchestration + per-conversation
  state. Shows product thinking, not just API calling.
- **Notes → Flashcards & MCQ Quiz** — Text chunking, JSON generation, a
  small scheduling algorithm (SM-2-lite). The most "real product" extra.
- **Exam-Answer Modes** — Prompt wrappers/presets. A weekend feature with
  huge demo value for Indian students, including STET-style prep.
- **Hinglish + "Samjhao"** — i18n plus language injected into the system
  prompt; the model does the heavy lifting.
- **₹ Cost-Aware Smart Routing** — Cost engineering: usage tracking, a
  price table, routing rules. A genuinely senior-sounding topic.
- **Placement Prep Planner** — The LLM generates a JSON plan once; the
  rest is checklist CRUD + progress UI.
- **Application Content Studio** — A template/preset library with form
  fields. Something I will use myself while job-hunting.
- **Voice-First PWA Mode** — PWA basics, Web Speech API, designing for
  low-end phones and low bandwidth.
- **Study-Room Share Links** — Share tokens, public/private access
  control. (Live rooms via Socket.io only as a stretch goal.)
- **Cited-Answers Mode** — A search API (free tier) + context injection +
  citation formatting: a mini version of LibreChat's real web-search
  pipeline.

## Deliberately not in scope

Real RAG/vector search, AI agents/MCP, a code-interpreter sandbox, image
generation, SSO/LDAP, an admin panel, paid speech APIs and billing. The
PDF features above use full-text-in-prompt within limits instead of RAG —
that trade-off is named on purpose (see `docs/architecture.md` and the
README).
