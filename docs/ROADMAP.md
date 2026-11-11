# Project Plan & Roadmap

This document describes the planned phases of development for ASI. Timelines are intentionally flexible — the focus is on delivering a solid foundation before expanding scope.

## Phase 1 — Core Assistant

**Goal:** A working conversational assistant you can talk to every day.

- [ ] Conversational chat interface (web app)
- [ ] Task management: create, complete, list, prioritize
- [ ] Reminders and scheduled notifications
- [ ] Notes and quick capture
- [ ] Basic memory of user preferences

**Deliverable:** A usable daily assistant for tasks and reminders.

## Phase 2 — Personal Context

**Goal:** ASI knows your world, not just your tasks.

- [ ] Persistent memory: routines, preferences, recurring events
- [ ] Calendar integration (read + write)
- [ ] Email integration (summaries, draft replies)
- [ ] Goal tracking with progress over time
- [ ] Weekly review summaries

**Deliverable:** An assistant that understands your schedule and habits.

## Phase 3 — Proactive Intelligence

**Goal:** ASI works for you, not just with you.

- [ ] Morning briefings: schedule, tasks, priorities
- [ ] Smart suggestions ("you have a meeting with X tomorrow — review the doc?")
- [ ] Automated follow-up reminders
- [ ] Insights and analytics on time usage and habits
- [ ] Natural-language automation rules ("every Friday, remind me to...")

**Deliverable:** A proactive companion that reduces mental load.

## Phase 4 — Extensions

**Goal:** ASI everywhere you are.

- [ ] Mobile apps (iOS / Android)
- [ ] Voice interface
- [ ] Third-party integrations marketplace (Slack, Notion, Todoist, etc.)
- [ ] Plugin/API for custom extensions
- [ ] Optional local/self-hosted mode for privacy

**Deliverable:** A platform, not just an app.

## Milestones

| Milestone | Description | Phase |
|-----------|-------------|-------|
| M1 | First chat + task demo | 1 |
| M2 | Daily-driver MVP | 1 |
| M3 | Calendar/email connected | 2 |
| M4 | Proactive briefings | 3 |
| M5 | Public beta | 3–4 |

## Risks & Open Questions

- **Privacy vs. capability** — deeper integrations mean more sensitive data access. Needs a clear privacy model early.
- **LLM costs** — frequent proactive features could be expensive; may need local models or smart caching.
- **Platform choice** — web-first vs. native mobile affects architecture; decide before Phase 2.
- **Scope creep** — the roadmap is deliberately staged; resist adding features ahead of their phase.
