# Ansiversa Repositories

## Purpose

This document records the primary GitHub repositories Astra should remember
when planning, reviewing, or assigning Codex work for Ansiversa.

It stores repository identity only. It must not store tokens, deploy keys,
secrets, database URLs, credentials, private user data, or environment values.

## Primary Repositories

| Repository | URL | Role |
|---|---|---|
| `ansiversa` | `https://github.com/srkarthi1982/ansiversa.git` | React parent shell and frontend modules for the Ansiversa platform and solution apps. |
| `ansiversa-api` | `https://github.com/srkarthi1982/ansiversa-api.git` | FastAPI backend for parent platform APIs, shared services, Knowledge, AI SEO, Astra AI architecture/foundation, and mini-app backend modules. |
| `astra` | `https://github.com/srkarthi1982/astra.git` | Standalone Astra recovery/source-pack repository containing safe durable platform, governance, repository, registry, certification, and checkpoint memory. |

## Working Repository Roles

### `ansiversa`

Owns frontend concerns:

- React parent shell;
- frontend routing and persistent platform layout;
- frontend app overview and workflow modules;
- shared UI components;
- generated API client usage;
- browser/E2E user verification surfaces.

Frontend changes must preserve the one-shell platform model:

```text
One login
One navigation
One ecosystem
One shell
One consistent experience
```

### `ansiversa-api`

Owns backend concerns:

- FastAPI parent platform services;
- authentication APIs and backend identity handling;
- app catalog APIs;
- Knowledge registry and public Knowledge artifacts;
- AI SEO architecture and compiler foundations;
- Astra AI architecture and platform foundation;
- shared Assistant, tool registry, user context, activity, notifications, and
  other platform services;
- mini-app backend modules, services, schemas, models, and migrations.

Backend changes must preserve app data ownership:

```text
Applications own their records and business rules.
Astra owns orchestration.
Knowledge owns governed platform truth.
AI SEO owns public-truth publishing architecture.
```

### `astra`

Owns safe durable memory for future Astra/Codex sessions:

- canonical source-pack files under `sources/`;
- platform and repository recovery checkpoints;
- governance, certification, validation, promotion, route, database,
  documentation, and repository memory;
- safe summaries of certified Astra/backend/frontend milestones.

The Astra repository must not contain secrets, tokens, credentials, production
user data, raw diagnostic payloads, private prompts, provider payloads, cookies,
database URLs, or environment values.

## Repository Boundary Rules

- Do not treat frontend and backend as interchangeable ownership areas.
- Do not move app business logic into Astra AI or the parent shell.
- Do not access app databases from central Astra AI code.
- Do not duplicate Knowledge or AI SEO publishing in the frontend.
- Do not store repository secrets in this source pack.
- Production changes remain separate from development, review, certification,
  and approval.
- When `ansiversa` or `ansiversa-api` changes durable Astra/Ansiversa knowledge,
  update the relevant `astra/sources` file and commit/push the standalone
  `astra` repository with or immediately after the product repository change.

## Current GitHub Remote Memory

```text
Frontend: https://github.com/srkarthi1982/ansiversa.git
Backend:  https://github.com/srkarthi1982/ansiversa-api.git
Astra:    https://github.com/srkarthi1982/astra.git
```
