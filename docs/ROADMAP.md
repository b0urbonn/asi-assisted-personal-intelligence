# Roadmap & Plan

> A phased plan for building ASI across mobile, desktop, and web. Phases are gated — each must deliver its core value before the next begins.

## Phase Overview

```
┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
│  Phase 1     │──▶│  Phase 2     │──▶│  Phase 3     │──▶│  Phase 4     │
│  Core        │   │  Personal    │   │  Proactive   │   │  Extensions  │
│  Assistant   │   │  Context     │   │  Intelligence│   │  & Platforms│
└──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘
 Web-first        Memory + sync      Briefings +        Native mobile,
 chat + tasks     Calendar + email   insights +        desktop apps,
                  + goals            automation        voice + plugins
```

---

## Phase 1 — Core Assistant

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
A user can run their day through ASI: capture → schedule → complete.

---

## Phase 2 — Personal Context

**Goal:** ASI knows your world — memory, calendar, email, goals. One mind across devices begins here.

### Deliverables
- [ ] Long-term memory store (preferences, routines, recurring facts)
- [ ] Memory transparency: view, edit, delete what ASI knows
- [ ] Cross-device sync becomes trivial — all devices read/write the same server (no sync conflicts, one source of truth)
- [ ] Calendar integration (read schedule, create events)
- [ ] Email integration (summaries, draft replies)
- [ ] Goal tracking with progress over time
- [ ] Morning briefing v1 (schedule + tasks + reminders)

### Milestone M3 — "It Knows My Day"
ASI briefs you each morning with real calendar + task context.

---

## Phase 3 — Proactive Intelligence

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
ASI proactively surfaces 3+ useful insights per week per user.

### Milestone M5 — Public Beta
Invite-only beta with mobile apps (Phase 4 work begins in parallel).

---

## Phase 4 — Everywhere

**Goal:** ASI installed on every device you own — native apps, ambient voice, and an ecosystem.

### Deliverables
- [ ] Native iOS app
- [ ] Native Android app
- [ ] Desktop apps (macOS, Windows — approach TBD: native vs web wrapper)
- [ ] Wake-word / ambient always-on voice
- [ ] Offline mode / local-first option
- [ ] Plugin & integration API (Slack, Notion, Todoist, GitHub…)
- [ ] Integration marketplace (if traction warrants)

### Milestone M6 — "ASI Everywhere"
Full platform parity across all devices with synced context.

---

## Timeline Philosophy

No fixed dates yet — ASI is pre-code. Instead:

- **Quality gates:** a phase ends when its milestone demo works end-to-end, not on a calendar.
- **Weekly reviews:** roadmap is revisited weekly once development starts.
- **Kill criteria:** if a feature doesn't serve the core loop (capture → organize → brief), it waits.

## Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|------------|
| LLM costs scale badly | High | Usage metering day one; caching; smaller models for simple intents |
| Cross-platform parity lag | Medium | Shared API + design system; web-first then port |
| Privacy backlash | High | Privacy-first architecture; transparent memory controls |
| Notification fatigue | Medium | "Calm tech" principle; user-controlled frequency |
| Scope creep | Medium | Phase gating; PRD sign-off before new features |

## Open Questions

- [ ] Native mobile (Swift/Kotlin) vs cross-platform (React Native/Flutter)?
- [ ] Desktop: native app vs Electron/Tauri wrapper vs web-only?
- [ ] Which LLM provider(s)? Cost vs capability tradeoff.
- [ ] Sync model: cloud-authoritative vs CRDT/local-first?
- [ ] Pricing model: free tier limits? subscription?
