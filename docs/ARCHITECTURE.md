# Architecture

> Status: draft v0.2 — pre-development. Captures current thinking for a cross-platform (mobile + desktop + web) product. Will evolve during Phase 1.

## Overview

ASI is a cloud-backed, cross-platform personal assistant:

- **Clients:** web app, iOS, Android, macOS, Windows — all thin clients over a shared API
- **Backend:** API gateway + core orchestration engine + data stores
- **Sync:** single source of truth in the cloud; clients stay in sync via realtime channels
- **AI:** pluggable LLM providers with a prompt/tool orchestration layer

```
┌────────────────────────────────────────────────────────────┐
│                        CLIENTS                             │
│   ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│   │   Web    │  │  iOS /   │  │ Android  │  │ Desktop  │  │
│   │   App    │  │  Mobile  │  │          │  │ macOS/Win│  │
│   └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘  │
│        └──────────────┴───────┬────┴──────────────┘        │
│                          HTTPS / WSS                        │
└────────────────────────────┬───────────────────────────────┘
                             ▼
┌────────────────────────────────────────────────────────────┐
│                      API GATEWAY                           │
│         Auth · Rate limits · Routing · Versioning          │
└────────────────────────────┬───────────────────────────────┘
                             ▼
┌────────────────────────────────────────────────────────────┐
│                     CORE ENGINE                            │
│   Intent routing · Orchestration · Tool use · Streaming    │
└──┬──────────┬──────────┬──────────┬──────────┬─────────────┘
   ▼          ▼          ▼          ▼          ▼
┌───────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌───────────┐
│Memory │ │ Tasks/ │ │  LLM   │ │Integr- │ │  Notify/  │
│Store  │ │ Notes  │ │Provider│ │ations  │ │ Scheduler │
└───────┘ └────────┘ └────────┘ └────────┘ └───────────┘
```

## Components

### Clients

All clients are thin — they render UI, capture input, and consume the API. Shared business logic lives server-side so behavior is identical across devices.

| Client | Tech (leaning) | Notes |
|--------|----------------|-------|
| Web | React / Next.js | Fast iteration; also the desktop fallback via PWA |
| iOS / Android | React Native (Expo) or native | Single codebase preferred; decide in Phase 4 |
| Desktop | Tauri wrapper of web app, or Electron | Tauri preferred for size/perf; revisit later |

**Offline strategy (Phase 4):** local cache for tasks/notes + queued actions; sync on reconnect. Full local-first (CRDT) is an open question.

### API Gateway

- REST for CRUD operations; WebSocket (or SSE) for chat streaming
- AuthN/AuthZ (JWT + refresh); per-user data isolation
- Rate limiting, request validation, API versioning
- Push notification dispatch (APNs / FCM)

### Core Engine

- **Intent routing:** classifies messages → question / task / reminder / note / automation
- **Orchestration:** calls LLM with tools (task store, calendar, memory), streams responses
- **Session management:** conversation state, cross-device session continuity
- **Proactive jobs:** scheduled briefings, follow-up checks, suggestion generation

### Data Stores

| Store | Tech (leaning) | Contents |
|-------|----------------|----------|
| Primary DB | PostgreSQL | Users, tasks, notes, goals, sessions |
| Vector memory | pgvector (or dedicated) | Long-term memory embeddings, recall |
| Cache/queue | Redis | Sessions, rate limits, job queues |
| Object storage | S3-compatible | Attachments, exports |

### LLM Provider

- Pluggable interface — swap providers without client changes
- Model routing: cheap model for intent classification, frontier model for complex reasoning
- Prompt registry + versioning; per-user cost metering
- Candidates: hosted frontier APIs first; local models evaluated in Phase 4

### Integrations

- OAuth connectors (Google Calendar, Gmail, Outlook, etc.)
- Webhook/event ingestion where supported
- Each integration is a plugin with scoped permissions — ASI can only access what the user grants

### Voice Pipeline

- Speech-to-text / text-to-speech via provider APIs (Phase 1: push-to-talk)
- Low-latency turn-taking design; streaming STT/TTS
- Wake-word / always-on mode evaluated in Phase 4 (on-device vs cloud tradeoffs)

### Notification & Scheduler

- Push (APNs/FCM), email digests, in-app inbox
- "Calm tech" delivery: batched, priority-aware, user-tunable
- Cron-like scheduler for briefings, reminders, follow-ups

## Key Decisions (open)

| Decision | Options | Leaning |
|----------|---------|---------|
| Mobile stack | React Native / Flutter / native | React Native (Expo) for velocity |
| Desktop | Tauri / Electron / web-only | Tauri wrapping web app |
| Backend | TypeScript (NestJS) / Python (FastAPI) | TypeScript — shared types with web |
| Database | Postgres + pgvector | Postgres |
| Sync model | Cloud-authoritative / CRDT | Cloud-authoritative first |
| LLM | Hosted API / local | Hosted API first |

## Non-Functional Requirements

- **Privacy:** encrypted at rest/in transit; per-user isolation; no training on user data; export/delete support
- **Latency:** streamed chat, p95 first token < 2s; task CRUD p95 < 300ms
- **Reliability:** graceful degradation when integrations/LLM are down (queue + retry)
- **Cost:** per-user usage metering from day one
- **Accessibility:** WCAG 2.1 AA on web; platform accessibility standards on mobile/desktop
