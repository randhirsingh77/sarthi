# Features

Sarthi is an AI chat app aimed at Indian students and job-seekers. The
essentials — auth, conversations, markdown chat UI, SSE streaming,
provider adapters, presets, token/₹ cost tracking, search — are the
base. The features below are the planned extras on top of that base.
None of them are built yet; this is the design target for v1 and
beyond.

## Planned for v1

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

## Full list

| # | Feature | What it does |
|---|---------|--------------|
| 1 | Resume-vs-JD Gap Analyser | Resume PDF text + pasted JD → matched/missing skills, ATS-style score, bullet fixes, saved per application |
| 2 | Mock Interview Mode | Role/company picker → one question at a time → rubric-scored answers → final report + score history |
| 3 | Hint-Ladder DSA Coach | Paste a DSA problem → Hint 1 → Hint 2 → approach → code, never the solution first; edge-case quiz at the end |
| 4 | Notes → Flashcards & MCQ Quiz | Semester PDF notes → flashcards + MCQs as revisable decks with simple spaced repetition |
| 5 | Exam-Answer Modes | One-tap rewrites: 5-mark short, 13-mark detailed, simple English, Hindi me samjhao |
| 6 | Hinglish + Language Toggle & "Samjhao" button | Language switch for UI and answers; "Samjhao" re-explains any answer simply |
| 7 | ₹ Cost-Aware Smart Routing | Per-chat ₹ estimate, cheap/fast model for simple questions, strong model for hard ones, daily budget meter |
| 8 | Placement Prep Planner | "45 days to my interview" → day-by-day checklist (DSA, aptitude, CS fundamentals) with ticks and streaks |
| 9 | Application Content Studio | One-click generators fed by the saved resume: Naukri profile summary, Internshala answers, LinkedIn About, referral message, cover letter |
| 10 | Voice-First PWA Mode | Installable app, voice input/output via the browser's free Web Speech API, lite chat view, answers downloadable as small text files for offline revision |
| 11 | Study-Room Share Links | Read-only share link to a conversation that classmates can open and fork; live rooms only as a stretch goal |
| 12 | Cited-Answers Mode | Toggle: answers must carry numbered citations from a quick web search, flagging anything that could not be sourced |
