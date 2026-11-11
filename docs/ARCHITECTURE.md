# Architecture

> Status: draft v0.2 — pre-development. Self-hosted, single-user, cross-device design for macOS, Windows, iOS, Android, and web clients. Will evolve during Phase 1.

## Deployment Model

ASI is a **self-hosted personal system** — one core server on your hardware, every device as a client.

```
YOUR HARDWARE                                    YOUR DEVICES
┌─────────────────────────────────┐
│  ASI Core Server                │
│  (Mac mini / desktop / home     │
│   server — always on)           │
│                                 │
│  ┌───────────────────────────┐  │
│  │ ~/.asi/                   │  │
│  │  data/   (tasks, memory,  │  │
│  │          notes, sessions) │  │
│  │  config/ (settings, keys) │  │
│  │  logs/                    │  │
│  └───────────────────────────┘  │
└──────────────┬──────────────────┘
               │  LAN direct · or Tailscale/WireGuard for remote
               ▼
     ┌──────────────────────────────────┐
     │  iPhone · Android · Mac · Windows│
     │  · Web — all thin clients        │
     └──────────────────────────────────┘
```

- **One instance, one user** — no multi-tenancy, no accounts on someone else's cloud
- **Server:** runs as an always-on service — launchd (macOS), systemd/NSSM (Windows/Linux), or a menu-bar companion app
- **Remote access:** Tailscale or WireGuard mesh VPN recommended; no port forwarding required
- **Data dir:** everything lives under `~/.asi/` — inspectable, backable-up, portable
- **External calls:** only what you configure — LLM API keys you provide, calendar/email OAuth you grant

## Overview

- **Core server:** the brain — API, engine, stores, scheduler. Single process (or small process set) on your machine.
- **Clients:** web app, iOS, Android, macOS, Windows — thin clients over the local/remote API
- **Sync:** not "cloud sync" — your devices all read/write the same server, so there's literally one copy of your data

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

All clients are thin — they render UI, capture input, and consume the API served by your ASI core. They can live on the same machine as the server (localhost) or connect remotely.

| Client | Tech (leaning) | Notes |
|--------|----------------|-------|
| macOS | Menu-bar app (Electron/Tauri) + web UI | Can double as the server host |
| Windows | Desktop app (Tauri/Electron) or web UI | Same |
| iOS / Android | React Native (Expo) or native | Connects to server over LAN/VPN |
| Web | React / Next.js served by the core | Works in any browser, local or tunneled |

**Offline strategy:** when the server is unreachable, clients show read-only cached data and queue actions; core features degrade gracefully.

### API Layer

- REST for CRUD; WebSocket (or SSE) for chat streaming
- Single-user auth: pairing tokens per device (like how you pair a phone to a server)
- Localhost-first — zero config works out of the box on the host machine

### Core Engine

- **Intent routing:** classifies messages → question / task / reminder / note / automation
- **Orchestration:** calls LLM with tools (task store, calendar, memory), streams responses
- **Session management:** conversation state, cross-device session continuity
- **Proactive jobs:** scheduled briefings, follow-up checks, suggestion generation

### Data Stores

| Store | Tech (leaning) | Contents |
|-------|----------------|----------|
| Primary DB | SQLite (default) / Postgres (optional) | Tasks, notes, goals, sessions, settings |
| Vector memory | sqlite-vec / pgvector | Long-term memory embeddings, recall |
| Queue | Built-in job runner (SQLite-backed) | Reminders, scheduled jobs |
| Files | `~/.asi/data/` | Attachments, exports, backups |

SQLite-first keeps install trivial (zero external services); Postgres optional for power users.

### LLM Provider

- Pluggable interface — swap providers without client changes
- **User-configured:** bring your own API keys (OpenAI, Anthropic, etc.) or point at a local model (Ollama/LM Studio)
- Model routing: cheap/local model for intent classification, stronger model for complex reasoning
- Prompt registry + versioning; optional cost metering
- Fully offline mode possible if a capable local model is configured

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
| Server runtime | Node/TypeScript vs Python | TypeScript (shared types with web) |
| Primary DB | SQLite vs Postgres | SQLite default; Postgres optional |
| Mobile stack | React Native / Flutter / native | React Native (Expo) for velocity |
| Desktop | Tauri / Electron / native | Tauri wrapping web UI |
| Remote access | Tailscale / WireGuard / tunnel | Tailscale-first |
| LLM | User API keys / local model / both | Pluggable; local-friendly |

## Non-Functional Requirements

- **Privacy:** self-hosted by design — data lives in `~/.asi/` on your machine; encrypted at rest; no telemetry by default
- **Latency:** local network calls are fast; LLM latency dominated by provider (streaming masks it)
- **Reliability:** server auto-restarts; clients degrade gracefully offline; single point of failure = your machine (backups recommended)
- **Portability:** entire state is files — rsync/backup the data dir to migrate or restore
- **Accessibility:** WCAG 2.1 AA on web; platform accessibility standards on mobile/desktop
