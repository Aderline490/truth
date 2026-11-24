# Truth — Personal Bible Study Companion
> A minimal, AI-powered Bible study tracker built for Jehovah's Witnesses — no copyrighted content hosted, just intelligent scheduling, tracking, and daily AI-generated flashcards.

---

## App Concept

**Name:** Truth
**Why:** JWs uniquely refer to the faith as *"the Truth"* — instantly recognizable to the community. Also resonates philosophically (John 8:32 — *"the truth will set you free"*) and scripturally (Greek: *Aletheia*).

**Core idea:** Truth doesn't host any Bible text or Watch Tower content. Instead it acts as an intelligent companion — managing your reading schedule, tracking progress, and using AI to generate daily flashcards and answer faith questions based on what you read in your own Bible or JW Library.

---

## What Truth Does NOT Include (Copyright)
- ❌ Bible text (NWT or any version)
- ❌ Daily text from JW.org
- ❌ Watchtower / Awake articles
- ❌ "Enjoy Life Forever" lessons
- ❌ Any Watch Tower Society publications

> The user reads from their own physical Bible or JW Library app. Truth only manages **references** (e.g. "John 8:32") never actual text.

---

## Target User

- Jehovah's Witnesses doing personal Bible study
- iOS-first mobile app

---

## Core Features

### 📅 Reading Schedule Manager
The heart of the app. User sets a schedule, Truth tracks where they are each day and tells them what to read.

**Schedule types:**

| Schedule | Description |
|--|--|
| Cover to cover | Genesis to Revelation in order |
| By theme | History, prophecy, gospels, letters etc. |
| Hebrew + Greek daily | One passage from each testament per day |
| Chronological | Order things historically occurred |
| Completion order | Order books were written |
| Custom | User picks book, chapter, verse to start from |

**Schedule settings:**
- Verses per day (slider — e.g. 5, 10, 15, 20)
- Chapters per day
- Start book & chapter (for custom mode)
- One year plan toggle (auto-calculates daily portion)
- Daily reminder time

**Daily flow:**
```
App says → "Today: Read Matthew 5:1-12"
User reads in their own Bible / JW Library
User comes back → marks reading as done
App generates flashcards from that passage
```

---

### 🤖 AI Study Companion (Claude API)
Since no Bible text is hosted, the AI fills the gap — user brings their study, AI helps them go deeper.

**What the AI does:**
- Generate daily flashcards based on the day's reading reference
- Answer questions about faith, doctrine, scripture meaning
- Quiz the user on what they've read
- Explain JW understanding of any topic
- Help prepare talking points for field ministry
- Connect today's passage to broader Bible themes
- Suggest reflection questions

**Example AI interactions:**
- *"I just read John chapter 8, what questions should I reflect on?"*
- *"Explain the JW understanding of the soul"*
- *"Quiz me on what I studied this week"*
- *"How does Matthew 5:1-12 relate to the Kingdom hope?"*

> **AI grounding:** Claude API will be given a system prompt grounding it in JW theology and NWT language to ensure accurate, respectful answers.

---

### 🃏 Daily AI Flashcards (Killer Feature)
After marking today's reading as done, the AI automatically generates a set of flashcards:

| Card Type | Example |
|--|--|
| **Recall** | "What happened in today's reading?" |
| **Understanding** | "Why did Jesus say X in this passage?" |
| **Connection** | "How does this relate to [other scripture]?" |
| **Doctrine** | "How does this passage support the JW understanding of Y?" |
| **Personal** | "How can you apply this in your life today?" |

- Cards are swipeable (know / don't know)
- Scores tracked over time
- Weak cards resurface the next day (spaced repetition)

---

### 📊 Progress Tracking
- % of Bible completed
- Current reading streak 🔥
- Chapters/verses read this week and month
- Flashcard quiz scores over time
- Achievements (finished a book, 7-day streak, completed a testament, etc.)
- Study history timeline

---

### 📝 Study Notes & Journal
- Write personal notes per reading session
- Tag notes by book, chapter, or topic
- "What I learned today" daily reflection prompt
- Searchable notes history

---

### 🔖 Verse Reference Bookmarks
- Save verse *references* (not text) e.g. "Romans 8:38-39"
- Organize bookmarks by topic or theme
- Add personal notes to any saved reference

---

### ⏰ Reminders & Notifications
- Daily reading reminder at chosen time
- Streak protection reminder ("Don't break your streak!")
- Weekly summary notification

---

## Tech Stack

| Layer | Technology | Why |
|--|--|--|
| **Mobile** | Flutter | Smooth UI, great for content-heavy apps, pixel-perfect design |
| **AI** | Claude API (Anthropic) | Handles nuanced religious conversation, customizable via system prompt |
| **Backend** | FastAPI (Python) | Lightweight, fast, auto-docs, easy to learn |
| **Database** | PostgreSQL | Reliable, powerful, great for structured data |
| **Local Storage** | SQLite / Hive | Offline access, fast reads for notes and schedule data |
| **Containerization** | Docker | Portable, consistent environments |
| **Orchestration** | Kubernetes (Minikube locally first) | DevOps learning, scalable later |
| **GitOps** | ArgoCD | Automated deployments from Git |
| **CI/CD** | GitHub Actions | Free, integrates with GitHub |
| **Cloud** | Fly.io or DigitalOcean | Affordable, beginner friendly |

---

## Architecture Overview

```
Flutter App (iOS)
      ↕  HTTP requests
FastAPI Backend
      ↕                    ↕
Claude API             PostgreSQL
(flashcards, Q&A)     (schedule, notes, progress)
      ↕
Docker → Kubernetes → ArgoCD
      ↕
GitHub Actions (CI/CD)
      ↕
Cloud (Fly.io / DigitalOcean)
```

> **Why a backend?** Keeps Claude API keys secure, enables multi-device sync, user accounts, and provides full DevOps learning with Docker/Kubernetes/ArgoCD/CI/CD.

---

## API Endpoints (Planned)

```
POST /ask                  → send question, get AI answer
POST /flashcards/generate  → generate flashcards for a reading reference
GET  /schedule             → get user's current reading schedule
POST /schedule             → create or update reading schedule
POST /schedule/complete    → mark today's reading as done
GET  /progress             → get reading progress and stats
POST /notes                → save a study note
GET  /notes                → get all notes
POST /bookmarks            → save a verse reference
GET  /bookmarks            → get all bookmarks
POST /auth/login           → user login
POST /auth/register        → user registration
```

---

## App Screens (Planned)

```
1. Onboarding       → welcome, set up first schedule
2. Home / Dashboard → today's reading, streak, quick AI chat
3. Schedule Setup   → pick schedule type, verses/day, reminders
4. Today's Reading  → what to read today, mark as done button
5. Flashcards       → swipeable daily cards after reading
6. AI Chat          → open-ended faith/study questions
7. Progress         → stats, streaks, achievements
8. Notes & Journal  → write, search, tag notes
9. Bookmarks        → saved verse references
10. Settings        → schedule, notifications, preferences
```

---

## DevOps Learning Path

This project is intentionally structured to teach DevOps progressively:

1. **Docker** — containerize FastAPI backend
2. **Minikube** — run Kubernetes locally for free
3. **GitHub Actions** — CI/CD pipeline (free)
4. **ArgoCD** — GitOps deployment automation
5. **Cloud deployment** — Fly.io or DigitalOcean when ready

---

## Cost Estimate (30 users)

| Scenario | Monthly Cost |
|--|--|
| Fly.io free tier + light AI usage | ~$5–10/month |
| DigitalOcean $12 droplet + moderate AI | ~$25–35/month |
| AWS free tier year 1 + light AI | ~$5–15/month |

**Claude API cost for 30 users:**
- Light usage (5–10 questions/day): ~$3–8/month total
- Moderate usage (20–30 questions/day): ~$10–20/month total

**Recommended starting setup:**
- Fly.io free tier for backend hosting ($0)
- Minikube locally to learn Kubernetes (free)
- GitHub Actions for CI/CD (free)
- Scale to paid cloud only when needed

---

## Suggested First Steps

1. [ ] Scaffold Flutter project (`flutter create truth`)
2. [ ] Set up FastAPI project structure
3. [ ] Build `/flashcards/generate` endpoint with Claude API
4. [ ] Build schedule setup screen in Flutter
5. [ ] Build today's reading screen with "Mark as Done" flow
6. [ ] Connect Flutter to FastAPI backend
7. [ ] Build swipeable flashcard UI in Flutter
8. [ ] Dockerize the FastAPI backend
9. [ ] Set up GitHub Actions CI/CD pipeline
10. [ ] Learn Kubernetes locally with Minikube
11. [ ] Set up ArgoCD for GitOps
12. [ ] Deploy to Fly.io or DigitalOcean

---

## Notes for Claude Code

- App name is **Truth** — keep all references consistent
- **Never store or display Bible text** — only verse references (e.g. "John 8:32")
- AI responses must be grounded in **JW theology** via system prompt
- User reads from their own **physical Bible or JW Library app** — Truth just tracks
- Flashcard generation is the **core daily loop** — prioritize this feature
- Design should feel **minimal, modern, interactive, and calm** — clean typography, lots of white space, dark mode first
- Start **local-first** — most data stored on device, backend handles AI calls and sync
- Keep infrastructure **simple and cheap** — max 30 users, no need to over-engineer
- Bible book and chapter data (just names/counts, no text) can be stored locally as a JSON file

---

*Updated from brainstorming session on Claude.ai — May 2026*