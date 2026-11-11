# Getting Started

> **Status:** living · **Version:** 0.2 · **Last updated:** 2026-11-11
> ASI is pre-code — this guide covers the repo today and will grow setup instructions once Phase 1 begins.

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Clone the Repo](#2-clone-the-repo)
3. [Project Layout](#3-project-layout)
4. [Documentation Map](#4-documentation-map)
5. [Development Workflow (planned)](#5-development-workflow-planned)
6. [Contributing](#6-contributing)
7. [License](#7-license)

---

## 1. Prerequisites

- Git
- Node.js 20+ (planned stack — subject to change)
- A GitHub account

## 2. Clone the Repo

```bash
git clone https://github.com/b0urbonn/asi-assisted-personal-intelligence.git
cd asi-assisted-personal-intelligence
```

## 3. Project Layout

```
.
├── README.md          # Project overview & doc index
├── assets/            # Images, logo, banner
│   ├── asi-logo.svg
│   └── banner.svg
├── docs/              # Detailed documentation (see docs/README.md)
│   ├── README.md          # Documentation index & conventions
│   ├── VISION.md          # Why ASI exists
│   ├── PRD.md             # Product requirements & user stories
│   ├── ROADMAP.md         # Phased development plan
│   ├── FEATURES.md        # Feature catalog (P0/P1/P2)
│   ├── ARCHITECTURE.md    # System design & data model
│   ├── DESIGN.md          # Brand & UX direction
│   └── GETTING_STARTED.md # This file
└── (code coming soon)
```

## 4. Documentation Map

Start at [`docs/README.md`](README.md) for the reading order and conventions. Quick map:

| If you want to… | Read |
|-----------------|------|
| Understand the vision | `docs/VISION.md` |
| See requirements & user stories | `docs/PRD.md` |
| Know what gets built when | `docs/ROADMAP.md` |
| See the feature checklist | `docs/FEATURES.md` |
| Understand the tech design | `docs/ARCHITECTURE.md` |
| See brand & UX direction | `docs/DESIGN.md` |

## 5. Development Workflow (planned)

- `main` — stable, releasable state
- Feature branches → PR → review → merge
- Docs live in `docs/` and are updated alongside code changes
- Every doc has a status header (`draft → review → approved → living`)

## 6. Contributing

Contributions are welcome once the project has code. Until then, open [GitHub issues](https://github.com/b0urbonn/asi-assisted-personal-intelligence/issues) to discuss ideas, features, or the roadmap.

Areas where feedback is especially valuable right now:

- Platform priorities (which device first after macOS?)
- Feature priorities within each phase
- Which work domains matter most (coding, teaching, research…)
- Privacy & data-handling expectations
- Integrations you wish existed

## 7. License

To be determined.
