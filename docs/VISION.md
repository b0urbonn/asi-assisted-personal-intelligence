# Vision & Goals

## What is ASI?

**Assisted Personal Intelligence (ASI)** is a personal AI companion you install on your own devices — your Mac, your Windows PC, your iPhone, your Android — all connected to one private brain running on hardware you control.

Not a chatbot you visit. Not a cloud service holding your life. A presence that's *already there* — aware of your context, attentive to what matters, and ready before you think to ask.

## The Model: One Private Brain, All Your Devices

```
        ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
        │   iPhone │  │ Android  │  │   Mac    │  │ Windows  │
        │  (app)   │  │  (app)   │  │ (app or  │  │  (app)   │
        └────┬─────┘  └────┬─────┘  │  menu bar│  └────┬─────┘
             └─────────────┴────┬───┴──────────┘       │
                          secure sync                  │
                             ▼                         │
                  ┌─────────────────────┐              │
                  │   ASI Core Server   │◀─────────────┘
                  │  (your Mac / PC /   │
                  │   home server)      │
                  │  memory · tasks ·   │
                  │  schedules · AI     │
                  └─────────────────────┘
```

- **The brain lives on your hardware** — a Mac mini, your desktop, a home server. Your data never leaves your network unless you say so.
- **Every device is a window** — apps on iOS, Android, macOS, and Windows all connect to the same instance. Same memory, same tasks, same context.
- **Centralized and unified by design** — one source of truth, not five apps with five partial copies of your life.

## The Shift

Most AI tools wait for you to show up and ask — and store everything on *their* servers. ASI inverts both:

| Traditional assistant | ASI |
|----------------------|-----|
| You open it → it responds | It's aware → it surfaces what matters |
| Session-based memory | Persistent understanding of your life |
| One device at a time | One private brain, every device |
| Your data on their cloud | Your data on your hardware |
| You manage the tool | It quietly manages the noise |
| Answers questions | Anticipates needs |

The goal is the feeling of **a capable presence handling your backlog** — briefing you, tracking commitments, and nudging you at the right moment — so your attention stays on what only you can do.

## The Problem

Your life is scattered across tools that don't talk to each other:

- 📱 Phone has reminders, messages, and quick capture
- 💻 Desktop has deep work, documents, and meetings
- 🗓️ Calendar knows *when*, task apps know *what*, email knows *who*
- 🧠 Your head knows *why* — and it's overloaded
- ☁️ And every "smart" tool wants your data in *their* cloud

You become the integration layer. Things slip. You context-switch constantly. Your most personal data sits on servers you don't control.

## The Vision

ASI becomes a quiet, ever-present intelligence layer — running on your machines, following you everywhere:

| Capability | What it means |
|------------|---------------|
| **Remembers** | Preferences, routines, commitments, goals — persistent across all devices |
| **Understands** | Context across tasks, calendar, email, notes — and across devices |
| **Anticipates** | Knows what's coming: briefings, prep nudges, follow-ups — before you ask |
| **Acts** | Drafts, schedules, organizes — always with your approval |
| **Speaks** | Voice-first interaction when you want it; text when you don't |
| **Follows you** | Same assistant, same memory, same context — phone ↔ desktop ↔ everywhere |
| **Stays home** | Runs on your hardware; you decide what (if anything) goes to external AI APIs |

## Design Principles

1. **Presence, not noise** — available always, interrupting never. Proactive but calm.
2. **Privacy by architecture** — self-hosted by default. Your memory lives on your disk, not a vendor's.
3. **Assist, don't replace** — ASI augments your judgment; never acts without your approval.
4. **One mind, every device** — seamless sync is the whole point, not an afterthought.
5. **Invisible when idle** — the best interface is the one you don't notice until you need it.
6. **Open and extensible** — integrations and plugins so ASI grows with you.
7. **Yours to keep** — no account on someone else's server, no subscription gate on your own data.

## Success Looks Like

- 🌅 You wake up, glance at your phone → ASI already briefed you: today's schedule, top priorities, anything needing attention.
- 🎙️ Driving or cooking → "ASI, what's on my plate today?" — a voice answer, hands-free.
- 💻 At your desk → the desktop app picks up exactly where your phone left off.
- 🔒 You check Activity Monitor and see ASI's memory, tasks, and logs sitting in `~/.asi/` on your own Mac — fully inspectable, fully yours.
- 🔔 Reminders arrive at the right time, in the right context — not as noise.
- 📊 Weekly reviews happen automatically with insights into where your time went.
- 🤝 You trust ASI enough to let it handle routine follow-ups — and to tell it when it's wrong.

## Non-Goals (for now)

- ASI is **not** a social network or content platform.
- ASI is **not** trying to replace your judgment or decision-making.
- ASI is **not** a general-purpose AI playground — it's focused on personal organization and life management.
- ASI is **not** surveillance — it helps you, it doesn't watch you.
- ASI is **not** (initially) a multi-tenant SaaS — it's a personal system first. Sharing/team features may come later, but the core is single-user, self-hosted.
