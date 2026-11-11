# Product Requirements Document (PRD)

> Status: draft v0.2 — pre-development. Defines what we're building, for whom, and why.

## 1. Overview

**Assisted Personal Intelligence (ASI)** is a self-hosted AI companion you install across your own devices — iOS, Android, macOS, Windows — all connected to a private ASI core running on hardware you control (your Mac, PC, or home server). It combines persistent memory, conversational and voice interaction, task management, and proactive assistance to reduce mental overhead.

**One private brain. Every device. Ready before you ask.**

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

- Morning routine under 2 minutes (open app → briefed → done)
- Task/reminder capture in under 5 seconds via natural language
- >70% positive feedback on proactive suggestions
- Daily active use by week 4 post-launch

### Success Metrics

| Metric | Target (MVP) |
|--------|--------------|
| Task capture time (p50) | < 5s |
| Morning briefing open rate | > 60% |
| Suggestion acceptance rate | > 30% |
| Device sync reliability | > 99% uptime when server is on |
| Time-to-install (fresh machine → first conversation) | < 30 min |

## 4. Personas

### 🧑‍💼 The Overwhelmed Professional
- Knowledge worker, 25–45; heavy calendar + email load
- Needs: meeting prep, follow-up tracking, daily prioritization
- Pain: things fall through cracks between tools; re-explains context on each device

### 🎓 The Student / Lifelong Learner
- Manages coursework, deadlines, personal projects
- Needs: deadline tracking, study reminders, goal progress
- Pain: scattered deadlines across syllabi, apps, and emails

### 👨‍👩‍👧 The Busy Parent / Caregiver
- Juggles family schedules, appointments, household tasks
- Needs: quick capture, never-miss reminders, shared context
- Pain: mental load of coordinating everyone else's schedules

### 🧘 The Wellness-Focused User
- Tracks habits, goals, and routines alongside work
- Needs: gentle accountability, weekly reviews, habit insights
- Pain: self-tracking tools are either too complex or too shallow

## 5. User Stories by Phase

### Phase 1 — Core Assistant
- As a user, I can chat with ASI in natural language to create tasks and set reminders.
- As a user, I can see today's tasks and mark them complete.
- As a user, I can dictate or type quick notes.
- As a user, I can talk to ASI via voice and hear it respond.
- As a user, my conversation context carries across messages and devices.
- As a user, I can access ASI from both my phone and desktop with the same account.

### Phase 2 — Personal Context
- As a user, ASI remembers my preferences, routines, and recurring commitments.
- As a user, I can view, edit, or delete anything ASI remembers about me.
- As a user, I can connect my calendar and see my schedule inside ASI.
- As a user, I receive a morning briefing combining schedule, tasks, and reminders.
- As a user, ASI tracks my goals and shows progress over time.

### Phase 3 — Proactive Intelligence
- As a user, ASI briefs me each morning before I even open the app.
- As a user, I get smart suggestions based on my context and schedule.
- As a user, ASI reminds me to follow up on things I said I'd do.
- As a user, I get a weekly review of how I spent my time and what I accomplished.
- As a user, I can set natural-language automations ("every Friday, remind me to…").
- As a user, I can have a hands-free voice conversation while driving or cooking.

### Phase 4 — Extensions
- As a user, I can use ASI on iOS, Android, macOS, and Windows with fully synced data.
- As a user, I can wake ASI by voice for ambient, always-on interaction.
- As a user, I can use ASI offline for core features.
- As a developer, I can build integrations via a public API and plugin system.

## 6. Scope

### In Scope (MVP)
- Chat + voice interface (web + mobile shells)
- Task CRUD + reminders + quick notes
- Session memory + basic preferences
- Auth, sync foundation, cross-device continuity
- Ambient morning briefing groundwork

### Out of Scope (for now)
- Social/sharing features between users
- Team/enterprise collaboration
- Third-party plugin marketplace (API first, marketplace later)
- Local LLM inference (Phase 4+ — hosted/user-key APIs first)
- Hardware integrations (smart home, wearables)
- Multi-user / team features (single-user personal system first)

## 7. Platforms & Deployment

ASI is **self-hosted**: a single-user core server runs on your own hardware; every device connects to it.

| Component | Platform | Strategy | Priority |
|-----------|----------|----------|----------|
| Core server | macOS / Windows / Linux | Always-on service (menu bar app or daemon) | Phase 1 |
| Desktop client | macOS, Windows | Native app or menu-bar companion | Phase 1–2 |
| Mobile client | iOS, Android | App connecting to your server over LAN/VPN | Phase 2–4 |
| Web client | Any browser | Thin client to your server (LAN or tunnel) | Phase 1 |

Remote access (phone away from home) via Tailscale/WireGuard or user-configured tunnel — never an open port by default.

See [ARCHITECTURE.md](ARCHITECTURE.md) for the technical approach.

## 8. Privacy & Data

- **Self-hosted by default** — all personal data (memory, tasks, notes, logs) lives on your hardware
- Encryption at rest and in transit; per-device auth tokens
- Full memory transparency: view, export, delete — it's just files on your disk
- Per-integration opt-in consent
- LLM calls: configurable — local models, your own API keys, or provider APIs you choose; nothing is sent anywhere you didn't configure
- Easy backup/export of the entire ASI data directory

## 9. Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Home server downtime | Medium | Auto-restart service; clients show offline state gracefully |
| LLM cost at scale | Medium | Local/small models for simple intents; user-chosen providers |
| Remote access complexity | Medium | Tailscale-first; simple setup wizard |
| Privacy concerns | Low | Self-hosted = data never leaves your network |
| Scope creep | Medium | Phase gating; PRD sign-off for new features |
| Hardware requirements | Low | Documented minimum specs; graceful degradation |
