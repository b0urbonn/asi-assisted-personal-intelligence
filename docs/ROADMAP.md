# Roadmap & Plan

> **Status:** draft · **Version:** 0.3 · **Last updated:** 2026-11-11

## Table of Contents

1. [Phase Overview](#1-phase-overview)
2. [Phase 1 — Core Assistant](#2-phase-1--core-assistant)
3. [Phase 2 — Personal Context](#3-phase-2--personal-context)
4. [Phase 3 — Proactive Intelligence](#4-phase-3--proactive-intelligence)
5. [Phase 4 — Everywhere](#5-phase-4--everywhere)
6. [Milestones](#6-milestones)
7. [Timeline Philosophy](#7-timeline-philosophy)
8. [Risks & Mitigations](#8-risks--mitigations)
9. [Open Questions](#9-open-questions)

---

## 1. Phase Overview

```
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│  Phase 1     │──▶│  Phase 2     │──▶│  Phase 3     │──▶│  Phase 4     │
│  Core        │   │  Personal    │   │  Proactive   │   │  Everywhere  │
│  Assistant   │   │  Context     │   │  Intelligence│   │              │
└──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘
 Self-hosted       Memory + cal +     Briefings +        Native mobile,
 server + chat     email + goals      insights +        desktop apps,
 + voice + tasks   + morning brief    automation        wake-word, plugins
```

| Phase | Theme | Gate to exit |
|-------|-------|--------------|
| 1 | Core Assistant | Daily-driver MVP works end-to-end |
| 2 | Personal Context | ASI knows your day (memory + calendar + briefings) |
| 3 | Proactive Intelligence | ASI surfaces useful things unprompted |
| 4 | Everywhere | Installed on all your devices, ambient voice |

---

## 2. Phase 1 — Core Assistant

**Goal:** A working AI assistant you can talk to daily — tasks, reminders, notes — running on your own hardware.

**Strategy:** Single-user, self-hosted from day one. The ASI core runs as a local service on your Mac/PC; the web UI and clients connect to it. Iteration is fast because there's no cloud infrastructure to manage — just your machine.

### Deliverables

- [ ] Web chat interface with streaming responses
- [ ] Voice input/output (push-to-talk → hands-free conversation)
- [ ] ASI core server: single-process service, auto-start, `~/.asi/` data dir
- [ ] One-command install / setup wizard (API key config, device pairing)
- [ ] Task management: create, list, complete, prioritize, due dates
- [ ] Reminders with local + push notification groundwork
- [ ] Quick-capture notes
- [ ] Session-level conversation memory
- [ ] Device pairing auth (localhost + LAN/VPN clients)
- [ ] Local API (REST + WebSocket for chat)

### Milestone M1 — "First Conversation"
Chat that can create a task from natural language and confirm it.

### Milestone M2 — "Daily Driver MVP"
A user can run their day through ASI: install → capture → schedule → complete → voice.

---

## 3. Phase 2 — Personal Context

**Goal:** ASI knows your world — memory, calendar, email, goals. One mind across devices becomes real.

### Deliverables

- [ ] Long-term memory store (preferences, routines, recurring facts)
- [ ] Memory transparency: view, edit, delete what ASI knows
- [ ] All devices read/write the same server — one source of truth, no sync conflicts
- [ ] Calendar integration (read schedule, create events)
- [ ] Email integration (summaries, draft replies)
- [ ] Goal tracking with progress over time
- [ ] Morning briefing v1 (schedule + tasks + reminders)
- [ ] Desktop companion app (menu bar / tray presence)

### Milestone M3 — "It Knows My Day"
ASI briefs you each morning with real calendar + task context.

---

## 4. Phase 3 — Proactive Intelligence

**Goal:** ASI works *for* you — surfacing what matters before you ask.

### Deliverables

- [ ] Proactive suggestions engine (context-aware nudges)
- [ ] Follow-up tracking ("you said you'd send X — done?")
- [ ] Weekly review: time usage + habit insights
- [ ] Natural-language automation rules
- [ ] Smart notification delivery (right time, right channel, batched)
- [ ] Ambient briefing mode — ASI surfaces itself at the right moments
- [ ] Cost optimization: caching, smart model routing

### Milestone M4 — "It Works While I Sleep"
ASI proactively surfaces 3+ useful insights per week.

### Milestone M5 — Public Preview
First public release: installers + docs for the curious.

---

## 5. Phase 4 — Everywhere

**Goal:** ASI installed on every device you own — native apps, ambient voice, and an ecosystem.

### Deliverables

- [ ] Native iOS app
- [ ] Native Android app
- [ ] Desktop apps (macOS, Windows — approach TBD: native vs web wrapper)
- [ ] Wake-word / ambient always-on voice
- [ ] Offline mode / local-first option
- [ ] Remote access hardening (VPN pairing, TLS)
- [ ] Plugin & integration API (Slack, Notion, Todoist, GitHub…)
- [ ] Integration marketplace (if traction warrants)
- [ ] Local LLM support for fully-offline operation

### Milestone M6 — "ASI Everywhere"
Full platform parity across all devices with synced context.

---

## 6. Milestones

| ID | Name | Phase | Demo criteria |
|----|------|-------|---------------|
| M1 | First Conversation | 1 | NL → task created → confirmed |
| M2 | Daily Driver MVP | 1 | Full daily loop: capture→schedule→complete, voice works |
| M3 | It Knows My Day | 2 | Morning briefing with real calendar data |
| M4 | It Works While I Sleep | 3 | 3+ proactive insights/week |
| M5 | Public Preview | 3–4 | Installable release + docs |
| M6 | ASI Everywhere | 4 | All devices, ambient voice, plugins |

## 7. Timeline Philosophy

No fixed dates yet — ASI is pre-code. Instead:

- **Quality gates:** a phase ends when its milestone demo works end-to-end, not on a calendar.
- **Weekly reviews:** roadmap is revisited weekly once development starts.
- **Kill criteria:** if a feature doesn't serve the core loop (capture → organize → brief), it waits.

## 8. Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|------------|
| LLM costs/quality | High | Model routing; local models for simple intents; user-chosen providers |
| Home server downtime | Medium | Auto-restart; graceful offline states; documented backups |
| Remote access complexity | Medium | Tailscale-first; setup wizard |
| Notification fatigue | Medium | "Calm tech" principle; user-controlled frequency |
| Scope creep | Medium | Phase gating; PRD sign-off before new features |

## 9. Open Questions

- [ ] Native mobile (Swift/Kotlin) vs cross-platform (React Native/Flutter)?
- [ ] Desktop: native app vs Tauri/Electron wrapper vs web-only?
- [ ] Which LLM providers first — hosted APIs, local models, or both?
- [ ] Minimum hardware spec for the core server?
- [ ] Pricing model: free/open-source forever, or paid companion app?
