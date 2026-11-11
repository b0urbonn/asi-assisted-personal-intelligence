# Architecture

> Status: draft. The architecture will evolve during Phase 1; this document captures the current thinking.

## Overview

ASI is envisioned as a modular system with a conversational core, a memory layer, and pluggable integrations.

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Clients   │────▶│   API Layer  │────▶│   Core Engine   │
│ (web, voice)│     │  (REST/WS)   │     │ (orchestration) │
└─────────────┘     └──────────────┘     └────────┬────────┘
                                                  │
              ┌───────────────────────────────────┼───────────────┐
              ▼                   ▼               ▼               ▼
        ┌───────────┐     ┌────────────┐   ┌───────────┐   ┌────────────┐
        │  Memory   │     │  Task/Note │   │   LLM     │   │Integrations│
        │  Store    │     │   Store    │   │ Provider  │   │ (calendar, │
        └───────────┘     └────────────┘   └───────────┘   │  email...) │
                                                           └────────────┘
```

## Components

### API Layer

- REST/WebSocket API for clients
- Auth and per-user data isolation
- Rate limiting and request validation

### Core Engine

- Intent routing: decides whether a message is a question, task, reminder, etc.
- Orchestrates LLM calls, tool use, and memory retrieval
- Streaming responses for chat UX

### Memory Store

- Short-term: conversation context (session)
- Long-term: user preferences, routines, facts
- Episodic: past interactions for recall
- All user-deletable; designed for explainable recall ("why do you know this?")

### Task & Note Store

- Structured store for tasks, notes, goals
- Full-text search
- Sync-friendly data model

### LLM Provider

- Pluggable provider interface (initially a hosted LLM API)
- Prompt management and guardrails
- Cost tracking per user/feature

### Integrations

- OAuth-based connectors (calendar, email, etc.)
- Each integration is a plugin with scoped permissions
- Webhook/event ingestion where supported

## Key Decisions (to be finalized)

| Decision | Options | Leaning |
|----------|---------|---------|
| Backend language | TypeScript / Python / Go | TypeScript (shared types with frontend) |
| Database | Postgres / SQLite / vector DB | Postgres + pgvector for memory |
| LLM | Hosted API vs local model | Hosted API first; local option in Phase 4 |
| Deployment | Managed cloud vs self-hosted | Managed cloud MVP; self-host later |
| Client | Web app vs mobile-first | Web app first; mobile in Phase 4 |

## Non-Functional Requirements

- **Privacy:** user data encrypted at rest; per-user isolation; no training on user data
- **Latency:** chat responses streamed; p95 first-token < 2s
- **Reliability:** graceful degradation when integrations are down
- **Cost:** per-user usage metering from day one
