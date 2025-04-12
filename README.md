# 🧠 Thought OS – Personal Knowledge & Capture System

Welcome to **Thought OS**, a voice-enabled, AI-enhanced interface to your brain — capturing what matters, organizing it invisibly, and helping you think clearly at scale.

---

## 🎯 Purpose

**Thought OS** is built to:

- Enable fast, flexible capture of thoughts, updates, and ideas (text, voice, audio)
- Structure and store this data for later processing and querying
- Use AI to enrich raw input with summaries, tags, insights, and next actions
- Serve as a second brain + timeline of work, creativity, goals, and life events
- Scale with minimal friction across desktop, mobile, and CLI interfaces

---

## 🧱 Current Framework

### Tech Stack

| Layer | Stack |
|-------|-------|
| Frontend | Next.js + Tailwind (Vercel hosted) |
| Backend | Supabase (PostgreSQL + Auth + Storage) |
| Input Channels | Web UI, CLI (planned), Chrome Extension (planned) |
| Voice Input | Web Speech API (for in-browser dictation) |
| AI Enrichment | OpenAI API (future phase) |

### Core Data Model

#### `captures` Table (central thought/input log)

| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Unique identifier |
| `created_at` | Timestamp | Auto-generated |
| `source` | Text | Where the capture came from (e.g. `web_ui`, `cli`, `voice`) |
| `raw_content` | Text | Main input field (text or voice transcript) |
| `project_id` | FK → `projects.id` | Optional – assigns entry to project |
| `tags` | Text[] | Optional tags for sorting/filtering |
| `status` | Text | Workflow status (`new`, `processed`, etc.) |
| `ai_summary` | Text | One-paragraph AI-generated summary |
| `ai_entities` | JSONB | Structured AI output (action items, people, topics, etc.) |

#### `projects` Table

| Field | Type |
|-------|------|
| `id` | UUID |
| `name` | Text |
| `description` | Text |
| `status` | Text |
| `created_at` | Timestamp |

---

## 🔮 Future State & Considerations

### AI Processing Layer

- Transcribe uploaded audio (Whisper or AssemblyAI)
- Summarize and classify thoughts with GPT-4
- Extract tasks, ideas, questions, blockers
- Suggest project or tag assignment

### Multi-Modal Capture

- 🎤 Voice-only mode (`/fast-talk`)
- 📱 Mobile optimization (or native app/PWA)
- 🧑‍💻 CLI command-line capture (`thought "Update..." --project x`)
- 🧠 Chrome extension to send content directly

### Output & Review Tools

- 🗓️ Daily/weekly thought summaries
- 🔎 Search + filter by tag/project/time
- 📊 Effort/time tracking per project
- 📁 Thought timeline / activity feed

---

## 🧩 Open Design Considerations

- Use structured tags or allow freeform? (currently freeform, AI-assisted tagging planned)
- Support voice-only classification via keyword/hashtag detection?
- How to handle audio file storage and transcription securely?
- Will long-term thoughts be versioned, merged, or linked?
- Data backup/export options (e.g., JSON, Markdown)?

---

## ⚠️ Known Limitations & Friction (As Scale Grows)

- Browser-only speech input doesn’t work on iOS Safari (Web Speech API)
- Supabase row security + auth needs refinement as CLI/extension grow
- Large scale AI processing may need queueing or external pipelines
- Input structure might need schema updates (e.g., sub-tasks, linked entities)
- As voice/audio use increases, storage & bandwidth costs may grow

---

## 🛣️ Roadmap

### ✅ MVP (Completed)
- [x] Web capture form with structured input + freeform memo
- [x] Project selection
- [x] Tag input
- [x] Voice dictation into memo field
- [x] Supabase schema for `captures` + `projects`

### 🔜 In Progress / Next Steps
- [ ] CLI input tool
- [ ] Chrome extension capture
- [ ] Mobile voice capture (PWA tweaks)
- [ ] Daily summary UI or email digest

### 🧠 AI Pipeline (Next Phase)
- [ ] Auto-tagging and project assignment
- [ ] Summarization + entity extraction
- [ ] Audio file upload + Whisper transcription
- [ ] Task extraction and to-do suggestions

