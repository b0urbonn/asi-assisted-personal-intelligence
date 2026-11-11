# Product Requirements Document (PRD)

> **Status:** draft · **Version:** 0.3 · **Last updated:** 2026-11-11 · **Owner:** project lead

## Table of Contents

1. [Overview](#1-overview)
2. [Problem Statement](#2-problem-statement)
3. [Goals & Success Metrics](#3-goals--success-metrics)
4. [Personas](#4-personas)
5. [User Stories by Phase](#5-user-stories-by-phase)
6. [Scope](#6-scope)
7. [Platforms & Deployment](#7-platforms--deployment)
8. [Privacy & Data](#8-privacy--data)
9. [Risks](#9-risks)
10. [Open Questions](#10-open-questions)

---

## 1. Overview

**Assisted Personal Intelligence (ASI)** is a self-hosted AI companion you install across your own devices — iOS, Android, macOS, Windows — all connected to a private ASI core running on hardware you control (your Mac, PC, or home server). It combines persistent memory, conversational and voice interaction, task management, and proactive assistance to reduce mental overhead.

**One private brain. Every device. Ready before you ask.**

| Attribute | Value |
|-----------|-------|
| Product type | Personal AI assistant (single-user, self-hosted) |
| Platforms | macOS · Windows · iOS · Android · Web |
| Deployment | Your hardware — `~/.asi/` data dir |
| Interaction | Chat + voice + ambient briefings |
| AI backend | Pluggable — your API keys or local models |

## 2. Problem Statement

People juggle tasks, calendars, email, and notes across disconnected tools — relying on memory to hold it together:

- Missed follow-ups and forgotten commitments
- Constant context-switching between apps and devices
- Mental overhead of tracking "what needs doing"
- No single place that understands the full picture
- Different context on phone vs desktop — you re-explain yourself
- Every "smart" tool wants your most personal data stored on *their* cloud
- No single place that holds your whole life — and no easy way to back it up or leave

## 3. Goals & Success Metrics

### Goals

- Morning routine under 2 minutes (glance → briefed → done)
- Task/reminder capture in under 5 seconds via natural language
- >70% positive feedback on proactive suggestions
- Daily use across at least 2 devices

### Success Metrics

| Metric | Target (MVP) |
|--------|--------------|
| Task capture time (p50) | < 5s |
| Morning briefing open rate | > 60% |
| Suggestion acceptance rate | > 30% |
| Device sync reliability | > 99% when server is on |
| Time-to-install (fresh machine → first conversation) | < 30 min |

## 4. Personas

ASI is designed for **one person with many roles** — the same user might be a developer in the morning, a teacher in the afternoon, and a researcher at night. Personas below describe work *modes*, not different users.

| Persona / Mode | Profile | Core needs | Pain |
|---------|---------|------------|------|
| 💻 Developer | Writes and ships code daily | Code help, debugging, docs, repo context | Context switching; remembering project details |
| 🎓 Educator / Teacher | Teaches, creates materials, grades | Lesson planning, student context, resource finding | Scattered materials; repetitive admin work |
| 🧑‍💼 Professional / Office | Meetings, docs, coordination | Email drafts, meeting prep, follow-ups | Admin overhead; things fall through cracks |
| 🔬 Researcher | Explores topics, synthesizes info | Literature summaries, note organization, citations | Information overload; lost sources |
| 📱 Social / Personal | Messaging, plans, life admin | Quick replies, schedule coordination, reminders | Mental load of keeping up |
| 🧘 Wellness-Focused | Habits, goals, routines | Accountability, weekly reviews, insights | Tracking tools too complex or too shallow |
| 🔒 Privacy-Conscious | Technical user wary of cloud AI | Self-hosted, inspectable data, provider choice | Doesn't trust vendor clouds with personal data |

### Use-Case Domains

ASI should be genuinely useful across all of these — not just task management:

| Domain | What ASI helps with |
|--------|---------------------|
| **Coding** | Explain/debug code, draft implementations, summarize repos/PRs, remember project conventions, track dev tasks |
| **Education** | Lesson plans, quiz generation, student progress notes, resource curation, grading assistance |
| **Office work** | Email drafting, meeting prep & notes, document summaries, follow-up tracking, report writing |
| **Research** | Source finding & summaries, citation tracking, knowledge organization, literature reviews |
| **Social/personal** | Message drafting, plan coordination, reminders, gift/occasion tracking |
| **Life admin** | Bills, appointments, goals, habits, weekly reviews |

## 5. User Stories by Phase

### Phase 1 — Core Assistant
- As a user, I can install ASI on my machine and start chatting in under 30 minutes.
- As a user, I can chat with ASI in natural language to create tasks and set reminders.
- As a user, I can see today's tasks and mark them complete.
- As a user, I can dictate or type quick notes.
- As a user, I can talk to ASI via voice and hear it respond.
- As a user, my conversation context carries across messages and devices.
- As a user, I can pair my phone/desktop to my ASI server with a simple code.

### Phase 2 — Personal Context
- As a user, ASI remembers my preferences, routines, and recurring commitments.
- As a user, I can view, edit, or delete anything ASI remembers about me.
- As a user, I can connect my calendar and see my schedule inside ASI.
- As a user, I receive a morning briefing combining schedule, tasks, and reminders.
- As a user, ASI tracks my goals and shows progress over time.
- As a developer, I can point ASI at a repo and ask questions about my codebase.
- As a teacher, I can ask ASI to draft a lesson plan or quiz from my topic.
- As a researcher, I can save sources and ask ASI to summarize/synthesize them.

### Phase 3 — Proactive Intelligence
- As a user, ASI briefs me each morning before I even open the app.
- As a user, I get smart suggestions based on my context and schedule.
- As a user, ASI reminds me to follow up on things I said I'd do.
- As a user, I get a weekly review of how I spent my time and what I accomplished.
- As a user, I can set natural-language automations ("every Friday, remind me to…").
- As a user, I can have a hands-free voice conversation while driving or cooking.
- As a developer, ASI notices when I've been heads-down too long and suggests a break.
- As a teacher, ASI reminds me of upcoming deadlines (grading, parent meetings).

### Phase 4 — Everywhere
- As a user, I can use ASI on iOS, Android, macOS, and Windows with fully synced data.
- As a user, I can wake ASI by voice for ambient, always-on interaction.
- As a user, I can use ASI offline for core features.
- As a user, I can access ASI remotely via a private VPN/tunnel.
- As a developer, I can build integrations via a public API and plugin system.

## 6. Scope

### In Scope (MVP — Phase 1)

- ASI core server (single-user, self-hosted, auto-start)
- Web chat UI + voice I/O
- Task CRUD + reminders + quick notes
- Session memory + basic preferences
- Device pairing auth
- Local data store (`~/.asi/`)

### Out of Scope (for now)

| Item | Reason / when |
|------|---------------|
| Social/sharing features | Not a social product |
| Team/enterprise collaboration | Single-user first; revisit later |
| Third-party plugin marketplace | API first, marketplace later |
| Local LLM inference | Phase 4+ — hosted/user-key APIs first |
| Hardware integrations (smart home, wearables) | Future exploration |
| Multi-user / accounts | Personal system, not SaaS |

## 7. Platforms & Deployment

ASI is **self-hosted**: a single-user core server runs on your own hardware; every device connects to it.

| Component | Platform | Strategy | Priority |
|-----------|----------|----------|----------|
| Core server | macOS / Windows / Linux | Always-on service (menu bar app or daemon) | Phase 1 |
| Desktop client | macOS, Windows | Native app or menu-bar companion | Phase 1–2 |
| Mobile client | iOS, Android | App connecting to your server over LAN/VPN | Phase 2–4 |
| Web client | Any browser | Thin client to your server (LAN or tunnel) | Phase 1 |

**Remote access** (phone away from home): Tailscale/WireGuard or user-configured tunnel — never an open port by default.

See [ARCHITECTURE.md](ARCHITECTURE.md) for the technical approach.

## 8. Privacy & Data

- **Self-hosted by default** — all personal data (memory, tasks, notes, logs) lives on your hardware
- Encryption at rest and in transit; per-device pairing tokens
- Full memory transparency: view, export, delete — it's just files on your disk
- Per-integration opt-in consent
- LLM calls: configurable — local models, your own API keys, or provider APIs you choose; nothing is sent anywhere you didn't configure
- Easy backup/export of the entire ASI data directory
- No telemetry by default; no accounts on third-party servers

## 9. Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Home server downtime | Medium | Auto-restart service; clients show offline state gracefully |
| LLM cost/quality variance | Medium | Local/small models for simple intents; user-chosen providers |
| Remote access complexity | Medium | Tailscale-first; simple setup wizard |
| Single point of failure (your machine) | Medium | Documented backups; optional Postgres/remote replica later |
| Scope creep | Medium | Phase gating; PRD sign-off for new features |
| Hardware requirements | Low | Documented minimum specs; graceful degradation |

## 10. Open Questions

- [ ] Final platform priority order after macOS (Windows? iOS?)
- [ ] LLM provider defaults for non-technical users
- [ ] Pricing — free/open-source forever, or paid companion app?
- [ ] Should there be an optional hosted relay for users without VPN skills?
