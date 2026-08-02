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
Backend HEAD                a15b3192572cd5a1f3e265652e4778967755b787
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
read_authority_binding.py
```

## ASTRA-CHAT-001 And Read Authority Binding Update

On 2026-08-02, ASTRA-RUNTIME-ACT-001 was Certified / Approved at backend commit
`a15b3192572cd5a1f3e265652e4778967755b787` after final Astra re-review approval
in PR #2 review `4837966223`. PR #2 remained open, draft, unmerged, and
mergeable at certification. The certified activation prerequisite preserves
nominal `AstraRuntime` owner binding, matching startup instance ID, exact
Runtime-owned activation authority, exact issuer/activation identity,
server-flag gating, reference/digest binding, Governance evidence provenance,
shutdown invalidation, Subscription Manager private-read scope only, Stage-0
disabled semantics, production prohibition, and provider/memory/adaptation/write
prohibition. ASTRA-READ-AUTH-BIND-001 has now resumed from the preserved stash
and has a corrected backend implementation pending Astra re-review and
certification. ASTRA-CHAT-001 remains authorized / paused until read-binding
certification. Production authorization remains not approved.

On 2026-08-02, ASTRA-RUNTIME-ACT-001 final Astra review correction was
implemented at backend commit `942fae7473be5267d7b5218ea8e3977f28fbd058`.
Activation issuer ownership is now Runtime-authoritative through a
module-private Runtime activation issuer root-of-trust, exact activation object
identity, issuer registration, activation reference, and activation digest.
This correction was superseded by the later live Runtime binding correction
after Astra identified that the trusted issuer factory itself was still
caller-accessible.

On 2026-08-02, ASTRA-RUNTIME-ACT-001 live Runtime binding correction was
implemented at backend commit `9804b1db1956cd6d5bad5b670f0385a12bea2bbc`.
The caller-accessible trusted issuer factory was removed. Issuer construction
now requires the exact opaque activation issuer authority owned by the supplied
`AstraRuntime` owner, direct issuer issuance also requires that authority, and
issuer validation requires the exact issuer to be registered on the live Runtime
with a loaded activation. This preserves the server-owned
`ASTRA_NONPROD_READ_ENABLED` gate as an effective prerequisite; server-flag
disabled issuer minting cannot produce an activation accepted by Governance.
This correction was superseded by the later exact Runtime owner binding
correction and certification.

On 2026-08-02, ASTRA-RUNTIME-ACT-001 exact Runtime owner binding correction was
implemented at backend commit `a15b3192572cd5a1f3e265652e4778967755b787`.
Activation issuer ownership is now bound to an actual nominal `AstraRuntime`
trust root and cannot be satisfied by an owner-shaped caller object or callback.
Issuer construction validates the Runtime owner type, matching startup instance
id, and exact Runtime-owned activation issuer authority before registration.
The explicit fake-owner negative proves matching `_activation_issuer_authority`
and `_validates_activation_issuer(...)` attributes are insufficient.
ASTRA-RUNTIME-ACT-001 was later Certified / Approved at this backend commit.

On 2026-08-02, ASTRA-CHAT-001 remained authorized but paused after preflight
confirmed a prerequisite gap: normal Runtime-owned application code did not yet
have a certified way to bind Subscription Manager read capability declarations
and Runtime-owned proof issuers into ASTRA-IMP-010 without validation fixture
mutation.

ASTRA-READ-AUTH-BIND-001 was implemented as the prerequisite, then resumed
after ASTRA-RUNTIME-ACT-001 certification, corrected, and Certified /
Approved at backend commit `6bf9e9e983711dbe65b18c98e6c47a45e117b02c` with
certification review `4838496452`. It adds a Runtime-owned read authority
binding component under:

```text
ansiversa-api/app/modules/astra_ai/read_authority_binding.py
```

The implemented scope is backend-only. It binds the app-owned certified
Subscription Manager read declarations into a sealed Runtime-owned read
capability registry, creates Runtime-owned proof issuers for ASTRA-IMP-010, and
supports normal Runtime-owned Subscription Manager metadata-only read
authorization without chat, frontend, provider/model integration,
natural-language inference, SQL/database execution in the binding component,
schema/migration, writes, additional app adapters, production configuration, or
deployment.

Capability Discovery remains metadata-only. Planning remains metadata-only.
ASTRA-READ-EXEC-001 behavior remains unchanged. ASTRA-CHAT-001 remains
authorized / paused until explicitly resumed. Production authorization remains
not approved and production remains unchanged.

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
ASTRA-APP-VAL-001           Certified / Approved
ASTRA-READ-EXEC-001         Certified / Approved
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
ASTRA-READ-EXEC-001          Certified / Approved
Implementation Scope         Governed Read Execution Bridge
Initial Adapter              Subscription Manager only
Implementation Review        Approved
Validation                   ASTRA-APP-VAL-001 Certified / Approved
Product Owner Approval       Approved
Certification                Passed
Implementation Commit        15c017b327635f29fe9ebc30132fb6a39a87d0ef
Validation Commit            19bc1e34feb4556f5dd7c4117536ba9d72ba8365
```

The bridge requires exact Runtime-registered read authorization, exact
Runtime-issued execution requests, exact Subscription Manager one-time read
grants, authenticated subject match, app/capability/version/request/limit and
execution-context match, explicit adapter registry resolution, and read-only
operation. It returns bounded structured read results and records
metadata-only execution evidence through existing Runtime evidence mechanisms.

Still not authorized:

```text
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
ASTRA-APP-VAL-001            Certified / Approved
Implementation Scope         Subscription Manager Governed Read Execution Validation
Astra Source Review          Approved
Security Review              Approved
Partner Review               Approved
Product Owner Approval       Approved
Certification                Passed
Backend Commit               19bc1e34feb4556f5dd7c4117536ba9d72ba8365
```

The validation proves Runtime-owned execution request issuance, read
authorization enforcement, explicit Subscription Manager adapter selection,
app-owned read execution, bounded/redacted Runtime result contracts,
fail-closed unauthorized/malformed request behavior, unchanged production
boundaries, and the database-session boundary proof requested during
ASTRA-READ-EXEC-001 review.

The database-session proof uses a tracking SQLAlchemy session to verify no SQL
execution occurs before registered adapter entry. The registered Subscription
Manager adapter then performs the app-owned read, and the returned Runtime
result excludes session, database, SQL, and private authority material.

## ASTRA-READ-AUTH-BIND-001 Memory

The backend contains a new implemented governed read authority binding under:

```text
ansiversa-api/app/modules/astra_ai/read_authority_binding.py
```

Current state:

```text
ASTRA-READ-AUTH-BIND-001     Certified / Approved
Implementation Scope         Governed Read Authority & Capability Binding
Initial App                  Subscription Manager only
Initial Backend Commit       b9dfceefc3352233e474eb91a04861431b4e5731
Correction Backend Commit    6bf9e9e983711dbe65b18c98e6c47a45e117b02c
Certification Review         4838496452
```

The binding exposes a narrow Runtime-owned surface through
`runtime.read_authority.capabilities()` and
`runtime.read_authority.authorize_subscription_manager_read(...)`. It binds
Subscription Manager app-owned read declarations, Runtime-owned proof issuers,
app-owned Subscription Manager owner acceptance, real ASTRA-IMP-010 Read Access
Authorization, and a post-authorization app-owned execution grant containing
the actual read authorization decision identity and the actual Governance
decision reference. It does not predict or manufacture Governance decision IDs.

Read authorization now binds the certified ASTRA-RUNTIME-ACT-001 activation
scope into Governance through `requested_app_id=subscription_manager`,
`requested_capability_scope=subscription_manager:private_read`, and verified
owner authority from the app-owned acceptance.

The corrected implementation requires a sealed backend-auth-owned
`AuthenticatedUserContext` issued only by the existing authenticated backend
request boundary. The issuer requires bearer token or auth cookie resolution,
access-token decoding, token expiration binding, existing DB user lookup by
token subject/email, login-status validation, auth-owned SQLAlchemy persistence
validation, timing user binding, and a module-private
authenticated-request-boundary authority. It rejects persistent DB users
presented outside an authenticated request, transient caller-created `User(...)`
objects, caller-constructed contexts, copied/tampered/foreign auth contexts,
expired/stale auth contexts, disabled/inactive/suspended users, owner-shaped
fake context objects, copied/expired/foreign/tampered owner acceptance,
different request reference/capability/version/parameters/result limit,
app/record/field/purpose escalation, copied/tampered read decisions, and
private fixture mutation. The auth-owned context registry is bounded and removes
expired contexts during issuance and expiration validation.

Subscription Manager has no tenant or organization authority model in this
repository. Read capability tenant scope is represented explicitly as
`tenant:not_applicable`, not as a fabricated platform tenant.

It adds no chat, frontend, provider/model integration, natural-language
inference, RAG, embeddings, memory, adaptation, writes, SQL/database execution
in the binding component, schema changes, migrations, production configuration,
generic Tool Executor, or additional app adapters.

Latest backend validation for correction commit
`6bf9e9e983711dbe65b18c98e6c47a45e117b02c`:

```text
.venv/bin/python -m pytest tests/test_astra_read_authority_binding.py -q
23 passed

.venv/bin/python -m pytest tests/test_subscription_manager_astra_read_capabilities.py -q
20 passed

.venv/bin/python -m pytest tests/test_astra_runtime_activation.py tests/test_astra_read_authority_binding.py tests/test_astra_read_access_authorization_engine.py tests/test_astra_read_execution_bridge.py tests/test_astra_app_val_001_read_execution_validation.py tests/test_subscription_manager_astra_read_capabilities.py tests/test_astra_governance_kernel.py tests/test_astra_runtime_core.py tests/test_astra_configuration_foundation.py tests/test_astra_evidence_sink.py tests/test_astra_conversation_context_engine.py tests/test_astra_intent_resolution_engine.py tests/test_astra_planning_engine.py -q
259 passed, 25 subtests passed

.venv/bin/python -m compileall app/modules/auth app/modules/astra_ai app/modules/subscription_manager validation/astra_app_001 validation/astra_app_val_001 tests/test_astra_read_authority_binding.py tests/test_astra_runtime_activation.py tests/test_astra_read_execution_bridge.py tests/test_subscription_manager_astra_read_capabilities.py
passed

.venv/bin/python -m pytest tests/test_astra*.py -q
405 passed, 147 warnings, 33 subtests passed
```

ASTRA-READ-AUTH-BIND-001 is Certified / Approved at backend commit
`6bf9e9e983711dbe65b18c98e6c47a45e117b02c` with certification review
`4838496452`.

## ASTRA-RUNTIME-ACT-001 Memory

The backend contains a new implemented governed non-production activation layer
under:

```text
ansiversa-api/app/modules/astra_ai/activation.py
```

Current state:

```text
ASTRA-RUNTIME-ACT-001        Certified / Approved
Implementation Scope         Governed Non-Production Runtime Activation
Initial App                  Subscription Manager only
Initial Capability Scope     subscription_manager:private_read
Initial Backend Commit        fd61ee1071227549500785e0c8a663cf5e2f8082
Correction Backend Commit     f1af573917b93f0ebe15e133a46f49a33cf1541f
Final Certified Commit        a15b3192572cd5a1f3e265652e4778967755b787
```

The activation layer preserves Stage-0 `feature_enabled=False` semantics and
adds a separate exact Runtime-owned activation contract loaded from server
configuration. The server setting defaults disabled, rejects malformed values,
prohibits production, and only permits local/development/QA/staging
Subscription Manager private-read advisory/read-only governance scope.

Activation authority is established by a Runtime-owned activation issuer and
exact-object registry. Matching metadata alone cannot activate Governance. Safe
`activation_reference` and `activation_digest` are bound into Governance input
and evidence provenance, while private Runtime issuer authority is not
serialized. Activation is lifecycle-bound to the Runtime startup instance and is
invalidated by Runtime shutdown.

Activation is not read authorization, app owner acceptance, read execution,
production approval, chat, provider/model integration, memory, adaptation,
writes, general tool execution, frontend behavior, persistence, migration, or
deployment.

ASTRA-READ-AUTH-BIND-001 is Certified / Approved. ASTRA-CHAT-001 remains
authorized / paused until explicitly resumed. Production authorization remains
not approved.

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
astra/sources/25-astra-read-authority-binding.md
astra/sources/26-astra-runtime-activation.md
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
