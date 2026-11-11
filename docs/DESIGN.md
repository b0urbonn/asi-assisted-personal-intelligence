# Design System & Brand

> **Status:** draft · **Version:** 0.2 · **Last updated:** 2026-11-11

## Table of Contents

1. [Brand Personality](#1-brand-personality)
2. [Voice & Tone](#2-voice--tone)
3. [UX Principles](#3-ux-principles)
4. [Visual Direction](#4-visual-direction)
5. [Key Screens](#5-key-screens)
6. [Interaction Model](#6-interaction-model)

---

## 1. Brand Personality

ASI should feel like a **discreetly brilliant presence** — the sense that someone capable is quietly watching your back. Think less "app," more "atmosphere."

| We are | We are not |
|--------|------------|
| Calm | Noisy, gamified |
| Anticipatory | Reactive, passive |
| Intelligent | Robotic, jargon-heavy |
| Trustworthy | Creepy, surveillance-y |
| Minimal | Cluttered, dashboard-heavy |
| Warm | Corporate, cold |
| Capable everywhere | Narrow tool for one task type |

## 2. Voice & Tone

ASI's personality: **a brilliant colleague who's been paying attention** — concise, warm, confident without arrogance, honest about uncertainty. ASI adapts its register to context — precise for code, warm for personal, formal for office work.

- **Concise** — gets to the point; respects your time
- **Proactive** — offers, doesn't wait; suggests, doesn't lecture
- **Honest** — admits uncertainty, never fakes confidence
- **Quiet confidence** — helpful without being pushy

Examples:
- ✅ "Morning. You've got 3 meetings and the Q3 report is due at 5. Want me to block focus time before lunch?"
- ✅ "You mentioned wanting to follow up with Sam — it's been 4 days. Draft a nudge?"
- ✅ "That error is a null pointer on line 42 — want me to walk through the fix?"
- ❌ "GREAT NEWS! I found some AMAZING tasks for you!!! 🎉"
- ❌ "As an AI language model, I cannot…" (ASI doesn't hide behind disclaimers)

## 3. UX Principles

| # | Principle | Meaning |
|---|-----------|---------|
| 1 | Glanceable | Core info visible in < 3 seconds on any device |
| 2 | One-thumb friendly | Mobile interactions designed for reachability |
| 3 | Progressive disclosure | Simple by default, depth on demand |
| 4 | Consistent across devices | Same mental model on phone, desktop, web |
| 5 | Forgiving | Undo everywhere; nothing permanent without confirmation |
| 6 | Calm notifications | Batched, prioritized, user-controlled |
| 7 | Voice-ready | Every core action doable hands-free; text is fallback |
| 8 | Ambient by default | ASI surfaces itself at the right moments |
| 9 | Mode-aware | UI adapts to context — code view for dev work, doc view for writing, timeline for schedule |

## 4. Visual Direction

- **Aesthetic:** clean, modern, minimal — think "Linear meets a good notebook"
- **Color:** muted palette with one accent (cool blue-violet family); dark mode first-class
- **Typography:** highly readable; strong hierarchy
- **Iconography:** simple, consistent line style
- **Motion:** subtle, purposeful — communicates state, never decorates
- **Voice UI:** when voice is active, the interface recedes — minimal orb/waveform, content secondary
- **Context surfaces:** code blocks, document previews, and data tables render richly inside chat — ASI isn't just text bubbles

*(Exact palette, type scale, and component specs TBD during Phase 1 UI work.)*

## 5. Key Screens

| Screen | Purpose | Priority |
|--------|---------|----------|
| Assistant | Primary interface — chat + voice | Phase 1 |
| Today | Daily briefing: schedule, tasks, reminders, suggestions | Phase 2 |
| Tasks | Full task management | Phase 1 |
| Workspace | Context-aware work surfaces (code, docs, sources) | Phase 2–3 |
| Memory | View/edit what ASI knows about you | Phase 2 |
| Insights | Weekly reviews, habit analytics | Phase 3 |
| Settings | Integrations, notifications, privacy, voice prefs | Phase 1 |

## 6. Interaction Model

ASI supports three modes, blending seamlessly:

| Mode | Behavior | Example |
|------|----------|---------|
| **Ambient** | Briefings and nudges arrive on their own | Morning briefing at 7:30 |
| **Conversational** | Chat or voice, your choice per moment | "Draft a reply to this email" |
| **Invisible** | Automations run silently in the background | Weekly review generated Sunday night |
