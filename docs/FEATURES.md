# Features

> **Status:** living · **Version:** 0.3 · **Last updated:** 2026-11-11
> Legend: `[P0]` = must-have for phase exit · `[P1]` = should-have · `[P2]` = nice-to-have

## Table of Contents

1. [Phase 1 — Core Assistant](#1-phase-1--core-assistant)
2. [Phase 2 — Personal Context](#2-phase-2--personal-context)
3. [Phase 3 — Proactive Intelligence](#3-phase-3--proactive-intelligence)
4. [Work-Domain Capabilities](#35-work-domain-capabilities-cross-phase)
5. [Phase 4 — Everywhere](#4-phase-4--everywhere)
6. [Cross-Cutting](#5-cross-cutting)

---

## 1. Phase 1 — Core Assistant

### Conversation `[P0]`

- [ ] Natural-language chat with streaming responses `[P0]`
- [ ] Voice conversation — push-to-talk input, spoken responses `[P0]`
- [ ] Session memory — follow-up questions with context `[P0]`
- [ ] Quick capture: type or dictate tasks, notes, reminders `[P0]`
- [ ] Cross-device conversation continuity `[P1]`

### Tasks & Reminders `[P0]`

- [ ] Create, edit, complete, delete tasks `[P0]`
- [ ] Due dates, priorities, recurring tasks `[P0]`
- [ ] "Today" view — what needs doing now `[P0]`
- [ ] Reminder scheduling with local notifications `[P0]`
- [ ] Push notification groundwork `[P1]`

### Notes `[P1]`

- [ ] Quick notes linked to tasks/context `[P1]`
- [ ] Full-text search `[P1]`

### Platform Basics `[P0]`

- [ ] Account-free setup: ASI core service on your machine, data in `~/.asi/` `[P0]`
- [ ] Settings: notification preferences, LLM provider config, device pairing `[P0]`
- [ ] One server, all devices — every client reads/writes the same instance `[P0]`
- [ ] Setup wizard: install → API key → first conversation `[P0]`
- [ ] Remote access over Tailscale/WireGuard `[P1]`

---

## 2. Phase 2 — Personal Context

### Memory `[P0]`

- [ ] Long-term memory: preferences, routines, recurring facts `[P0]`
- [ ] Memory transparency screen — view, edit, delete anything ASI knows `[P0]`
- [ ] Memory explanations — "why do you know this?" `[P1]`

### Integrations `[P0]`

- [ ] Calendar (Google/Outlook): read schedule, create events `[P0]`
- [ ] Email (Gmail/Outlook): summaries, draft replies `[P1]`
- [ ] Goals: set, track, progress over time `[P1]`

### Briefings `[P0]`

- [ ] Morning briefing: schedule + tasks + reminders + suggestions `[P0]`
- [ ] Configurable briefing time and format `[P1]`
- [ ] Briefing delivered to phone before you wake / first open `[P2]`

### Desktop Presence `[P1]`

- [ ] Menu bar / tray companion on macOS & Windows `[P1]`
- [ ] Quick-capture hotkey `[P1]`

---

## 3. Phase 3 — Proactive Intelligence

- [ ] Ambient morning briefing — ASI surfaces your day before you ask `[P0]`
- [ ] Context-aware suggestions ("meeting with X at 2 — review the doc?") `[P0]`
- [ ] Follow-up tracking ("you said you'd send the report — done?") `[P0]`
- [ ] Weekly review: time usage, accomplishments, patterns `[P1]`
- [ ] Natural-language automation rules `[P1]`
- [ ] Smart notification delivery (batched, prioritized) `[P0]`
- [ ] Meeting prep nudges `[P1]`
- [ ] Hands-free voice conversations for on-the-go use `[P1]`

---

## 3.5 Work-Domain Capabilities (cross-phase)

ASI is a general work companion, not just a task manager. These capabilities layer onto the core over time:

### 💻 Coding `[P2 → grows each phase]`
- [ ] Code Q&A: paste code, ask questions, get explanations `[P1]`
- [ ] Debugging help: paste errors/logs, get hypotheses `[P1]`
- [ ] Repo awareness: index a codebase, answer questions about it `[P2]`
- [ ] Draft implementations from natural language `[P2]`
- [ ] PR/diff summaries `[P2]`
- [ ] Remember project conventions & preferences `[P1]`

### 🎓 Education / Teaching `[P2]`
- [ ] Lesson plan drafting from a topic `[P2]`
- [ ] Quiz / worksheet generation `[P2]`
- [ ] Student progress notes & report drafts `[P2]`
- [ ] Resource curation (find/summarize materials) `[P2]`
- [ ] Grading assistance `[P2]`

### 🧑‍💼 Office Work `[P1]`
- [ ] Email drafting & reply suggestions `[P1]`
- [ ] Meeting prep briefs & notes `[P1]`
- [ ] Document summarization `[P1]`
- [ ] Report / proposal writing help `[P2]`
- [ ] Calendar-aware scheduling help `[P1]`

### 🔬 Research `[P2]`
- [ ] Source saving & organization `[P2]`
- [ ] Paper/article summarization `[P2]`
- [ ] Citation tracking `[P2]`
- [ ] Synthesis across multiple sources `[P2]`

### 📱 Social / Personal `[P1]`
- [ ] Message drafting (tone-matched) `[P1]`
- [ ] Plan coordination help `[P1]`
- [ ] Occasion/gift reminders `[P2]`
- [ ] Quick replies and status updates `[P1]`

---

## 4. Phase 4 — Everywhere

### Platforms `[P0]`

- [ ] Native iOS app `[P0]`
- [ ] Native Android app `[P0]`
- [ ] Desktop apps (macOS, Windows) `[P0]`
- [ ] Wake-word / always-on ambient voice mode `[P1]`
- [ ] Offline mode for core features `[P1]`
- [ ] Remote access hardening (VPN pairing, TLS) `[P0]`

### Ecosystem `[P2]`

- [ ] Public API for integrations `[P1]`
- [ ] Plugin system `[P2]`
- [ ] Third-party integrations: Slack, Notion, Todoist, GitHub, etc. `[P2]`
- [ ] Integration marketplace (if warranted) `[P2]`
- [ ] Local LLM support for fully-offline operation `[P1]`

---

## 5. Cross-Cutting

### Privacy & Control `[P0]`

- [ ] View/export/delete all stored data `[P0]`
- [ ] Per-integration opt-in/opt-out `[P0]`
- [ ] Configurable LLM provider (keys or local) `[P0]`
- [ ] Transparent AI explanations `[P1]`
- [ ] Backup/restore of `~/.asi/` `[P1]`

### Quality `[P0]`

- [ ] Accessibility (WCAG 2.1 AA on web) `[P1]`
- [ ] Dark mode, responsive design `[P1]`
- [ ] Usage analytics (privacy-preserving, off by default) `[P2]`
- [ ] Cost/usage metering `[P1]`
