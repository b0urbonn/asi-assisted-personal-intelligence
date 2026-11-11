# Design System & Brand

> Status: draft v0.1 — direction, not final specs. Will be formalized once UI work begins.

## Brand Personality

ASI should feel like a **discreetly brilliant presence** — the sense that someone capable is quietly watching your back. Think less "app," more "atmosphere."

| We are | We are not |
|--------|------------|
| Calm | Noisy, gamified |
| Anticipatory | Reactive, passive |
| Intelligent | Robotic, jargon-heavy |
| Trustworthy | Creepy, surveillance-y |
| Minimal | Cluttered, dashboard-heavy |
| Warm | Corporate, cold |

## Voice & Tone

ASI's personality: **a brilliant colleague who's been paying attention** — concise, warm, confident without arrogance, honest about uncertainty.

- **Concise** — gets to the point; respects your time
- **Proactive** — offers, doesn't wait; suggests, doesn't lecture
- **Honest** — admits uncertainty, never fakes confidence
- **Quiet confidence** — helpful without being pushy

Examples:
- ✅ "Morning. You've got 3 meetings and the Q3 report is due at 5. Want me to block focus time before lunch?"
- ✅ "You mentioned wanting to follow up with Sam — it's been 4 days. Draft a nudge?"
- ❌ "GREAT NEWS! I found some AMAZING tasks for you!!! 🎉"
- ❌ "As an AI language model, I cannot…" (ASI doesn't hide behind disclaimers)

## UX Principles

1. **Glanceable** — core info visible in < 3 seconds on any device
2. **One-thumb friendly** — mobile interactions designed for reachability
3. **Progressive disclosure** — simple by default, depth on demand
4. **Consistent across devices** — same mental model on phone, desktop, web
5. **Forgiving** — undo everywhere; nothing is permanent without confirmation
6. **Calm notifications** — batched, prioritized, user-controlled
7. **Voice-ready** — every core action should be doable hands-free; text is the fallback, not the primary
8. **Ambient by default** — ASI surfaces itself at the right moments; doesn't demand attention

## Visual Direction

- **Aesthetic:** clean, modern, minimal — think "Linear meets a good notebook"
- **Color:** muted palette with one accent; dark mode first-class
- **Typography:** highly readable; strong hierarchy
- **Iconography:** simple, consistent line style
- **Motion:** subtle, purposeful — communicates state, never decorates
- **Voice UI:** when voice is active, the interface recedes — minimal orb/waveform, content secondary

*(Exact palette, type scale, and component specs TBD during Phase 1 UI work.)*

## Key Screens (planned)

| Screen | Purpose | Priority |
|--------|---------|----------|
| Assistant | Primary interface — chat + voice | Phase 1 |
| Today | Daily briefing: schedule, tasks, reminders, suggestions | Phase 2 |
| Tasks | Full task management | Phase 1 |
| Memory | View/edit what ASI knows about you | Phase 2 |
| Insights | Weekly reviews, habit analytics | Phase 3 |
| Settings | Integrations, notifications, privacy, voice prefs | Phase 1 |

## Interaction Model

ASI supports three modes, blending seamlessly:

- **Ambient** — briefings and nudges arrive on their own
- **Conversational** — chat or voice, your choice per moment
- **Invisible** — automations run silently in the background
