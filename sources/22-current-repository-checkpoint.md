# Current Repository Checkpoint

Document Status: Recovery memory checkpoint.

Created: 2026-07-29.

Purpose: record verified knowledge found in the current `ansiversa` and
`ansiversa-api` repositories that is newer than, or missing from, the original
`astra/sources` source pack generated on 2026-07-18.

This file is a source-pack supplement. It does not replace the generated JSON
registries. Refresh generated registries separately when a task explicitly
authorizes a registry sync.

## Repository Baseline

Verified local repository heads:

```text
Frontend repository         ansiversa
Frontend HEAD               8786453d9d67416669d149614df0e179e47b88b2

Backend repository          ansiversa-api
Backend HEAD                4800e72d65aa592c6294be24e98492c9295db1b7
```

The workspace root is not itself a Git repository. `ansiversa` and
`ansiversa-api` are independent Git repositories inside the workspace.

## Source-Pack Gap Summary

The existing `astra/sources` pack still contains valuable platform memory, but
it is older than the current repositories.

Verified gaps:

```text
Original source-pack generated/refreshed     2026-07-18
Source-pack catalog state                    92 live / 8 comingSoon
Current backend overview export state        100 live / 0 comingSoon
```

The eight apps whose current backend overview export is live while
`astra/sources/05-ansiversa-catalog.json` still records them as comingSoon are:

```text
meeting-scheduler
work-log-tracker
savings-goal-planner
salary-breakdown-calculator
net-worth-tracker
errand-planner
local-services-finder
emergency-checklist
```

Each is now `launchStatus = live` and `version = 1.0.0` in
`ansiversa-api/app/modules/content/data/overview/apps.json`.

## Certified Astra Backend And Developer Stack

The original source pack does not fully capture the later Astra certification
milestones. Current repository documentation records this certified state:

```text
ASTRA-001 through ASTRA-010       Approved / Frozen
ASTRA-IR-001                      Approved / Frozen

ASTRA-IMP-001 through ASTRA-IMP-011
Certified / Approved

ASTRA-VAL-001                     Certified / Approved
ASTRA-VAL-002                     Certified / Approved

ASTRA-API-001                     Certified / Approved
ASTRA-API-001-COR-001             Certified / Approved
ASTRA-API-VAL-001                 Certified / Approved

ASTRA-UI-001                      Certified / Approved
```

Production authorization remains not approved. Production remains unchanged.

The certified stack is:

```text
Certified Astra Runtime
Governance, conversation, discovery, intent and planning
Read-access authorization
Diagnostic projection
Projection validation
Authenticated non-production diagnostics API
API security and contract validation
Administrator Developer Diagnostics Console
```

## Backend Astra Implementation Memory

The backend contains the certified Astra implementation under:

```text
ansiversa-api/app/modules/astra_ai/
```

Important certified modules include:

```text
constitutional_contracts.py
configuration.py
governance.py
evidence_sink.py
runtime.py
conversation_context.py
capability_discovery.py
planning.py
intent_resolution.py
read_access_authorization.py
diagnostic_projection.py
```

The diagnostics API is under:

```text
ansiversa-api/app/modules/astra_ai/api/
```

Authorized diagnostics route prefix:

```text
/internal/astra/diagnostics
```

Authorized diagnostics endpoints:

```text
GET  /internal/astra/diagnostics/health
POST /internal/astra/diagnostics/projections/runtime
POST /internal/astra/diagnostics/projections/request
POST /internal/astra/diagnostics/projections/evidence
POST /internal/astra/diagnostics/projections/components
```

Diagnostics API boundaries:

```text
Authentication              Required
Developer/admin authority   Required
Environment                 Non-production only
Default redaction           Strict
Projection authority        ASTRA-IMP-011 only
Runtime diagnostics         Dedicated runtime endpoint only
Component diagnostics       capability_discovery
                            intent_resolution
                            planning
                            read_access_authorization
Request diagnostics         Bounded unavailable until authoritative lookup exists
Evidence diagnostics        Explicit evidence references only
Rejected input echo         Prohibited
Validation errors           Sanitized only at exact diagnostics route boundary
Frontend integration        ASTRA-UI-001 only
Database / SQL              Not authorized by diagnostics API
Production authorization    Not approved
Production                  Unchanged
```

The exact diagnostics validation boundary is:

```text
path == /internal/astra/diagnostics
or
path starts with /internal/astra/diagnostics/
```

Sibling routes such as `/internal/astra/diagnostics-other` and
`/internal/astra/diagnostics2` must retain normal FastAPI validation behavior.

## Backend Validation Memory

Certified local validation packages:

```text
validation/astra_val_001/
validation/astra_val_002/
validation/astra_api_val_001/
```

`ASTRA-VAL-001` verifies fail-closed integration behavior for the certified
backend Astra engine.

`ASTRA-VAL-002` verifies diagnostic projection integrity and privacy.

`ASTRA-API-VAL-001` verifies authenticated diagnostics API security and
contracts. It is observational only and does not modify Runtime, diagnostics
API implementation, projection engine, authentication, authorization,
configuration, routes, database, SQL, frontend, deployment, or production
configuration.

## Frontend Astra Diagnostics Console Memory

The frontend contains the certified Developer Diagnostics Console under:

```text
ansiversa/src/modules/astra-diagnostics/
ansiversa/docs/astra-ui-001-developer-diagnostics-console.md
```

Certified console route:

```text
/admin/astra-diagnostics
```

Route registration is disabled by default and requires:

```text
VITE_ASTRA_DIAGNOSTICS_UI_ENABLED=true
and
a non-production Vite environment
```

Accepted frontend non-production environments:

```text
development
local
qa
staging
test
```

ASTRA-UI-001 boundaries:

```text
Authentication                  Required
Administrator authorization     Required
Backend authority               ASTRA-API-001 only
Default redaction               Strict
Persistence                     Prohibited
Polling / SSE / WebSockets      None
Public navigation               Absent
Command palette                 Absent
Catalog                         Absent
Astra user chat                 Not authorized
Production diagnostics UI       Not authorized
Production authorization        Not approved
Production                      Unchanged
```

The UI reads the certified health field:

```text
operational_astra_status
```

It renders fail-closed and other non-operational states as warning-treated
semantic values without renaming the backend value.

The console stores diagnostics only in volatile Zustand memory. It resets on
route unmount or auth loss and uses generation plus panel request IDs so stale
in-flight requests cannot repopulate cleared state or overwrite newer panel
responses.

The frontend performs defensive rendering against prohibited diagnostic
keys/values, including rejected input, tracebacks, private module paths,
authority material, credentials, prompts, provider payloads, proof objects, and
Runtime handles.

## ASTRA-APP-001 Memory

The backend has a newer certified app-owned read capability milestone:

```text
ASTRA-APP-001               Certified / Approved
Implementation Scope        Subscription Manager Governed Read Capability
Implementation commit       c0bde31ddd8032ff21a0996787e6012068e7d3f9
Target App                  Subscription Manager / App #071
Mode                        Read-only
Ownership                   App-owned
```

Certified capability IDs:

```text
subscription.count_all
subscription.count_active
subscription.list_active
subscription.highest_cost
subscription.total_recurring_cost
subscription.monthly_cost_estimate
subscription.renewing_this_month
subscription.renewing_within_days
subscription.overdue_renewals
subscription.group_by_category
```

ASTRA-APP-001 boundaries:

```text
Frontend / Chat             Not authorized
Provider / Model            Not authorized
ASTRA-APP-VAL-001           Not authorized
ASTRA-READ-EXEC-001         Not authorized
ASTRA-CHAT-001              Not authorized
Production Authorization    Not approved
Production                  Unchanged
```

ASTRA-READ-EXEC-001 was later separately authorized and implemented as the
narrow Runtime-owned read execution bridge for this certified app-owned
adapter. ASTRA-APP-001 itself remains frozen.

## ASTRA-READ-EXEC-001 Memory

The backend contains a new implemented governed read execution bridge under:

```text
ansiversa-api/app/modules/astra_ai/read_execution.py
```

It exposes Runtime-owned read execution through:

```text
runtime.read_execution.issue_request(...)
runtime.read_execution.execute(...)
```

Current state:

```text
ASTRA-READ-EXEC-001          Implemented
Implementation Scope         Governed Read Execution Bridge
Initial Adapter              Subscription Manager only
Implementation Review        Approved with follow-up findings
Product Owner Approval       Pending
Certification                Pending
```

The bridge requires exact Runtime-registered read authorization, exact
Runtime-issued execution requests, exact Subscription Manager one-time read
grants, authenticated subject match, app/capability/version/request/limit and
execution-context match, explicit adapter registry resolution, and read-only
operation. It returns bounded structured read results and records
metadata-only execution evidence through existing Runtime evidence mechanisms.

Still not authorized:

```text
ASTRA-APP-VAL-001
ASTRA-CHAT-001
frontend chat
provider/model integration
general tool execution
additional app adapters
write/mutation execution
production read execution
```

Production authorization is not approved. Production remains unchanged.

## ASTRA-APP-VAL-001 Memory

The backend contains a new implemented validation package under:

```text
ansiversa-api/validation/astra_app_val_001/
```

It validates Subscription Manager governed read execution through
ASTRA-READ-EXEC-001.

Current state:

```text
ASTRA-APP-VAL-001            Implemented
Implementation Scope         Subscription Manager Governed Read Execution Validation
Astra Source Review          Pending
Security Review              Pending
Product Owner Approval       Pending
Certification                Pending
```

The validation proves Runtime-owned execution request issuance, read
authorization enforcement, explicit Subscription Manager adapter selection,
app-owned read execution, bounded/redacted Runtime result contracts,
fail-closed unauthorized/malformed request behavior, unchanged production
boundaries, and the database-session boundary proof requested during
ASTRA-READ-EXEC-001 review.

The database-session proof uses a tracking SQLAlchemy session to verify central
Astra performs no session method calls before adapter entry. The registered
Subscription Manager adapter then performs the app-owned read, and the returned
Runtime result excludes session, database, SQL, and private authority material.

## Other Newer Repository Memory

The frontend repository contains post-source-pack platform work, including:

```text
Astra AI Assistant naming and shell integration
Global Command Search
Personal Dashboard updates
Favorites and Recent Apps
Notifications Center
Universal Activity Timeline
Intent-Based App Prefetching Phase 1
PWA install support
Navigation ownership cleanup
Production Vercel rewrites for public AI knowledge artifacts
```

The backend repository contains post-source-pack architecture and implementation
work, including:

```text
AI SEO architecture and implementation phases
Astra operational readiness specification
Astra AI implementation readiness planning
Subscription Manager app-owned Astra read capability
```

These areas should be read from the live repositories before new work. This
checkpoint records their existence and high-level boundaries only.

## Recovery Guidance For A New Account

When using a new ChatGPT or Codex account, load this source pack plus the live
repository files. Treat this file as the bridge between the 2026-07-18 source
pack and the current repository state.

Minimum files to load for current Astra work:

```text
astra/sources/00-README.md
astra/sources/01-ansiversa-platform-overview.md
astra/sources/02-ansiversa-governance.md
astra/sources/12-ui-contracts.md
astra/sources/13-backend-contracts.md
astra/sources/14-coding-standards.md
astra/sources/21-ansiversa-repositories.md
astra/sources/22-current-repository-checkpoint.md
astra/sources/23-astra-read-execution.md
astra/sources/24-astra-app-validation.md
ansiversa/AGENTS.md
ansiversa-api/AGENTS.md
ansiversa-api/docs/iterations/index.md
ansiversa-api/docs/iterations/2026-08-astra-imp/00-iteration-overview.md
ansiversa-api/docs/iterations/2026-08-astra-val/00-iteration-overview.md
ansiversa-api/docs/iterations/2026-08-astra-api/00-iteration-overview.md
ansiversa/docs/astra-ui-001-developer-diagnostics-console.md
```

The source pack intentionally does not contain secrets, API keys, database URLs,
JWTs, cookies, production user data, provider credentials, private prompt
payloads, or raw diagnostic payloads.
