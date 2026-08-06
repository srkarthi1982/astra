# Astra Frontend Governed Subscription Chat

## Document Status

```text
Work Item: ASTRA-FE-CHAT-001
Status: Implemented / Pending Astra Review
Date: 2026-08-06
Frontend Repository: ansiversa
Frontend Base: 4681a23cc08240db8595941a2fee80989ad24825
Frontend Branch: feature/astra-governed-subscription-chat
Frontend Commit: 90c9a71581ec9145dc99363f12e276f5fbd227bf
Frontend PR: #1, open, draft, unmerged
Certified Backend Executable: 4d7d25fd1f95ef7fd3912a1cdc21ef43729e8646
Backend Certification Review: 4876497721
Backend Certification Record: 615ef1b3ec375aacca9a9a9cb564832688a0d34c
Production Authorization: Not approved
```

## Purpose

ASTRA-FE-CHAT-001 exposes the certified ASTRA-CHAT-001 governed read contract
through Ansiversa's existing shared Astra assistant panel. It does not add a
second assistant surface, change backend architecture, introduce natural
language inference, or grant frontend authority.

## Frontend Contract

The Astra panel has Platform and Subscription Manager modes. Subscription
Manager mode accepts only sealed, exact question mappings for these certified
capabilities:

```text
subscription.count_all
subscription.count_active
subscription.list_active
subscription.highest_cost
subscription.total_recurring_cost
subscription.monthly_cost_estimate
subscription.renewing_this_month
subscription.overdue_renewals
subscription.group_by_category
subscription.renewing_within_days
```

The first nine capabilities use exact supported questions. The
`subscription.renewing_within_days` capability uses an explicit numeric control
and accepts integers from 1 through 366. Unsupported free text does not execute
an API request.

## Request And Authentication

Governed requests call only:

```text
POST /api/v1/astra/chat
```

They use the existing cookie-authenticated API client with credentials included.
The request supplies the exact app, action, subject, capability, and approved
parameters. It does not send a user ID, owner ID, role, permission, authority,
or any other client-asserted authorization context.

The legacy `/api/v1/assistant/query` endpoint remains available only for the
existing Platform mode. A governed Subscription Manager request never falls
back to it after denial, unavailability, network failure, or malformed output.

## Conversation And Rendering

The backend conversation ID is scoped to the mounted Astra component. It is
cleared on reset and when the authenticated user changes, and it is not stored
in browser persistence.

Before rendering, the frontend verifies that the response capability matches
the requested capability. Successful results are displayed as structured
answers rather than raw JSON. Authentication failures, endpoint unavailability,
network failures, malformed results, clarification requests, unavailable
capabilities, and governance denials use bounded user-facing messages without
exposing backend internals.

## Environment Boundary

The governed frontend is disabled unless
`VITE_ASTRA_GOVERNED_CHAT_ENABLED=true` and the frontend is running in a
recognized non-production environment such as development, local, QA, staging,
or test. Production enablement is not part of this work item.

## Automated Evidence

The following validation passed at frontend commit
`90c9a71581ec9145dc99363f12e276f5fbd227bf`:

```text
npm run lint
npm run typecheck
npm run build

Focused governed chat Playwright suite:
14 passed across Chromium and mobile Chromium

Existing Astra assistant Playwright suite:
12 passed, 1 credential-gated skip

git diff --check
passed
```

The focused suite covers question-to-capability mapping, exact endpoint and
payload behavior, unsupported-input non-execution, structured rendering, day
parameter validation, authentication and denial responses, absence of legacy
fallback, endpoint/network/clarification/capability-unavailable handling,
conversation reset, and the production gate.

## Isolated Browser Proof

Live browser QA ran against the certified backend branch using temporary,
migrated SQLite copies for the parent and Subscription Manager databases. No
production or Turso database was used.

A primary authenticated user created a category and two subscriptions through
the normal Subscription Manager UI. The exact governed question returned:

```text
Subscriptions: 2.
```

After the same user created a third subscription through the normal UI, the
same governed question returned:

```text
Subscriptions: 3.
```

A secondary authenticated user received:

```text
Subscriptions: 0.
```

The proof recorded two governed `/api/v1/astra/chat` calls and zero
`/api/v1/assistant/query` calls, demonstrating database provenance, fresh reads,
owner isolation, and absence of legacy fallback.

## Current Boundary

ASTRA-FE-CHAT-001 is implemented but not certified or approved. Frontend PR #1
and backend PRs #3 and #4 remain draft and unmerged. No production
configuration, migration, deployment, authorization, or merge is included.
