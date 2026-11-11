# Product Requirements Document (PRD)

> Status: draft v0.2 — pre-development. Defines what we're building, for whom, and why.

## 1. Overview

**Assisted Personal Intelligence (ASI)** is an always-available AI companion for iOS, Android, macOS, Windows, and web. It combines persistent memory, conversational and voice interaction, task management, and proactive assistance to reduce mental overhead.

**One presence. Every device. Ready before you ask.**

## 2. Problem Statement

People juggle tasks, calendars, email, and notes across disconnected tools — relying on memory to hold it together:

- Missed follow-ups and forgotten commitments
- Constant context-switching between apps and devices
- Mental overhead of tracking "what needs doing"
- No single place that understands the full picture
- Different context on phone vs desktop — you re-explain yourself

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
| Cross-device session continuity | > 80% of users sync |
| Retention (D30) | > 40% |

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
- On-device LLM inference
- Hardware integrations (smart home, wearables)

## 7. Platforms

| Platform | Strategy | Priority |
|----------|----------|----------|
| Web | Responsive web app — the fast iteration platform | Phase 1 |
| iOS | Native or React Native — TBD | Phase 4 (beta earlier) |
| Android | Same stack as iOS | Phase 4 |
| macOS / Windows | Desktop app or web wrapper — TBD | Phase 4 |

See [ARCHITECTURE.md](ARCHITECTURE.md) for the technical approach.

## 8. Privacy & Data

- Encryption at rest and in transit
- Per-user isolation; **no training on user data**
- Full memory transparency: view, export, delete
- Per-integration opt-in consent
- Local-first / on-device mode explored in Phase 4
- Data residency options under evaluation

## 9. Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| LLM cost at scale | High | Usage metering, caching, model routing |
| Cross-platform parity lag | Medium | Shared API + design system; web-first |
| Privacy concerns | High | Privacy-first design; transparent controls |
| Notification fatigue | Medium | Calm-tech principle; user-controlled frequency |
| Scope creep | Medium | Phase gating; PRD sign-off for new features |
| App store policy (AI features) | Low-Med | Review guidelines early; web fallback |
