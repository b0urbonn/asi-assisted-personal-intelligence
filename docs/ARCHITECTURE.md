# Architecture

> **Status:** draft · **Version:** 0.3 · **Last updated:** 2026-11-11
> Self-hosted, single-user, cross-device design for macOS, Windows, iOS, Android, and web clients.

## Table of Contents

1. [Deployment Model](#1-deployment-model)
2. [System Overview](#2-system-overview)
3. [Components](#3-components)
4. [Data Model](#4-data-model)
5. [API Surface](#5-api-surface)
6. [Voice Pipeline](#6-voice-pipeline)
7. [Security](#7-security)
8. [Key Decisions](#8-key-decisions)
9. [Non-Functional Requirements](#9-non-functional-requirements)

---

## 1. Deployment Model

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

## 2. System Overview

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
│                      API LAYER                             │
│      Auth · Rate limits · Routing · Validation             │
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

## 3. Components

### 3.1 Clients

All clients are thin — they render UI, capture input, and consume the API served by your ASI core. They can live on the same machine as the server (localhost) or connect remotely.

| Client | Tech (leaning) | Notes |
|--------|----------------|-------|
| macOS | Menu-bar app (Electron/Tauri) + web UI | Can double as the server host |
| Windows | Desktop app (Tauri/Electron) or web UI | Same |
| iOS / Android | React Native (Expo) or native | Connects to server over LAN/VPN |
| Web | React / Next.js served by the core | Works in any browser, local or tunneled |

**Offline strategy:** when the server is unreachable, clients show read-only cached data and queue actions; core features degrade gracefully.

### 3.2 API Layer

- REST for CRUD; WebSocket (or SSE) for chat streaming
- Single-user auth: pairing tokens per device (like how you pair a phone to a server)
- Localhost-first — zero config works out of the box on the host machine
- Request validation + rate limiting (protects against runaway clients)

### 3.3 Core Engine

- **Intent routing:** classifies messages → question / task / reminder / note / automation
- **Orchestration:** calls LLM with tools (task store, calendar, memory), streams responses
- **Session management:** conversation state, cross-device session continuity
- **Proactive jobs:** scheduled briefings, follow-up checks, suggestion generation

### 3.4 Data Stores

| Store | Tech (leaning) | Contents |
|-------|----------------|----------|
| Primary DB | SQLite (default) / Postgres (optional) | Tasks, notes, goals, sessions, settings |
| Vector memory | sqlite-vec / pgvector | Long-term memory embeddings, recall |
| Queue | Built-in job runner (SQLite-backed) | Reminders, scheduled jobs |
| Files | `~/.asi/data/` | Attachments, exports, backups |

SQLite-first keeps install trivial (zero external services); Postgres optional for power users.

### 3.5 LLM Provider

- Pluggable interface — swap providers without client changes
- **User-configured:** bring your own API keys (OpenAI, Anthropic, etc.) or point at a local model (Ollama/LM Studio)
- Model routing: cheap/local model for intent classification, stronger model for complex reasoning
- Prompt registry + versioning; optional cost metering
- Fully offline mode possible if a capable local model is configured

### 3.6 Integrations

- OAuth connectors (Google Calendar, Gmail, Outlook, etc.)
- Webhook/event ingestion where supported
- Each integration is a plugin with scoped permissions — ASI can only access what the user grants

### 3.7 Voice Pipeline

- Speech-to-text / text-to-speech via provider APIs (Phase 1: push-to-talk)
- Low-latency turn-taking design; streaming STT/TTS
- Wake-word / always-on mode evaluated in Phase 4 (on-device vs cloud tradeoffs)

### 3.8 Notification & Scheduler

- Push (APNs/FCM), email digests, in-app inbox, local notifications
- "Calm tech" delivery: batched, priority-aware, user-tunable
- Cron-like scheduler for briefings, reminders, follow-ups

## 4. Data Model

Core entities (SQLite schema sketch):

```
users          — single row in practice (device tokens reference it)
devices        — paired clients: name, platform, token hash, last_seen
tasks          — title, notes, due_at, priority, status, recurrence, source_msg_id
notes          — body, tags, linked_task_id, created_at
memory_items   — kind (pref/routine/fact), content, embedding, confidence, source, expires_at?
sessions       — conversation threads: device, title, created_at
messages       — session_id, role, content, ts, metadata (tool calls)
goals          — title, target, progress, milestones, review_cadence
reminders      — task_id?, fire_at, channel, payload, delivered_at
integrations   — provider, oauth tokens (encrypted), scopes, status
jobs           — scheduler queue: type, payload, run_at, status, retries
settings       — key/value: llm provider, voice prefs, briefing config
```

Design rules:

- **Everything is a file under `~/.asi/`** — backup = copy the directory
- **Soft deletes** on memory/tasks so users can recover and ASI can explain changes
- **Provenance on memory** — every memory item records where it came from ("you told me on Tuesday")
- **Embeddings optional** — keyword search works first; vector recall layers on top

## 5. API Surface

Versioned under `/api/v1/`:

| Group | Endpoints (sketch) |
|-------|--------------------|
| Auth | `POST /pair` (device pairing), `POST /token/refresh` |
| Chat | `WS /chat` (streaming), `GET /sessions`, `GET /sessions/:id/messages` |
| Tasks | `GET/POST /tasks`, `PATCH/DELETE /tasks/:id`, `POST /tasks/:id/complete` |
| Notes | `GET/POST /notes`, `GET /notes/search?q=` |
| Memory | `GET/POST/DELETE /memory`, `GET /memory/:id/explain` |
| Briefing | `GET /briefing/today`, `PUT /briefing/config` |
| Voice | `WS /voice` (streaming STT/TTS session) |
| Integrations | `GET/POST /integrations`, OAuth callbacks |
| System | `GET /health`, `GET /version`, `GET /backup` |

## 6. Voice Pipeline

```
mic ──▶ VAD ──▶ STT ──▶ Core Engine ──▶ LLM ──▶ TTS ──▶ speaker
                  ▲                          │
                  └────── barge-in ───────────┘
```

- **Phase 1:** push-to-talk — hold button, speak, release. STT/TTS via provider APIs.
- **Phase 3:** conversational turn-taking, barge-in support.
- **Phase 4:** wake-word evaluation — on-device wake word + cloud STT is the likely split (privacy + latency).

## 7. Security

- TLS everywhere except localhost (which needs none)
- Per-device pairing tokens; revocable; hashed at rest
- OAuth tokens encrypted at rest (key in `~/.asi/config/`, user-protected)
- No inbound ports by default — outbound-only for remote access via VPN/tunnel
- Rate limiting + input validation on all endpoints
- Secrets never logged; LLM prompts scrubbed of tokens before storage

## 8. Key Decisions

| Decision | Options | Leaning |
|----------|---------|---------|
| Server runtime | Node/TypeScript vs Python | TypeScript (shared types with web) |
| Primary DB | SQLite vs Postgres | SQLite default; Postgres optional |
| Mobile stack | React Native / Flutter / native | React Native (Expo) for velocity |
| Desktop | Tauri / Electron / native | Tauri wrapping web UI |
| Remote access | Tailscale / WireGuard / tunnel | Tailscale-first |
| LLM | User API keys / local model / both | Pluggable; local-friendly |
| Voice STT/TTS | Provider APIs / on-device | Provider APIs first; on-device in P4 |

## 9. Non-Functional Requirements

| Requirement | Target |
|-------------|--------|
| **Privacy** | Self-hosted; data in `~/.asi/`; encrypted at rest; no telemetry by default |
| **Latency** | Chat stream first-token p95 < 2s; local API calls p95 < 100ms |
| **Reliability** | Server auto-restarts; clients degrade gracefully offline |
| **Portability** | Entire state is files — rsync/backup the data dir to migrate or restore |
| **Accessibility** | WCAG 2.1 AA on web; platform standards on mobile/desktop |
| **Install size** | Server + web UI < 200MB; no external services required |
