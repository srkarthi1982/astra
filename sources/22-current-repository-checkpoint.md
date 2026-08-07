# Current Repository Checkpoint

Document Status: Recovery memory checkpoint.

Created: 2026-07-29.

Purpose: record verified knowledge found in the current `ansiversa` and
`ansiversa-api` repositories that is newer than, or missing from, the original
`astra/sources` source pack generated on 2026-07-18.

This file is a source-pack supplement. It does not replace the generated JSON
registries. Refresh generated registries separately when a task explicitly
authorizes a registry sync.

## ASTRA-AI-INTENT-001 Implementation Pending Review

On 2026-08-07, Product Owner/Astra authorized GitHub issue
`srkarthi1982/ansiversa-api#8` for backend implementation and controlled
non-production QA only. Codex implemented the governed natural-language intent
boundary from exact architecture certification-record base
`00102d6669ff9021e7301f689d74090d760a2a03` on branch
`feature/astra-ai-intent-001`. Backend implementation commit
`e51943e932ffe3b1b71b3ecbbdcadb3c1616b57b` adds the authenticated,
default-off, non-production-only `POST /api/v1/astra/agent/query` endpoint,
provider-independent exact mapping for all ten certified Subscription Manager
reads, a metadata-only projector over fresh app-owned `capability_catalog()`
output, strict untrusted candidate validation, and in-process handoff to the
unchanged certified `AstraChatGateway`.

The separate `OpenAIIntentProvider` uses the Responses API structured-output
mechanism with one bounded request, zero retries, no tools/functions, and
server-owned model/settings. Provider input contains only the current question,
allowed interpretation statuses, and eligible capability metadata with
parameter schema. It contains no records, identity, authorization, grants,
Runtime/Governance objects, DB/SQL material, secrets, writes, or final-answer
authority. Raw prompts and provider payloads are not persisted as evidence.

Focused validation passed 91 tests with one credential-gated real-provider
smoke skipped because `OPENAI_API_KEY` was absent. Full Astra validation passed
541 tests plus 33 subtests, with that same single credential-gated skip.
Authenticated agent HTTP provenance changed the primary owner's real DB-backed
`subscription.count_all` answer from 2 to 3 after a committed owner-scoped row;
a second authenticated user saw only their own count of 1. Compileall and
`git diff --check` passed. Backend PR #9 is open, draft, and unmerged against
`feature/astra-ai-intent-arch-001`.

ASTRA-AI-INTENT-001 is Implemented / Pending Astra Review. It is not certified.
Frontend agent integration is NOT AUTHORIZED. No merge, manual deployment,
production configuration, or production authorization occurred. Production
remains NOT APPROVED. Dedicated implementation memory is recorded in
`sources/32-astra-governed-natural-language-intent-implementation.md`.

## ASTRA-AI-INTENT-ARCH-001 Architecture Certification

On 2026-08-07, GitHub issue `srkarthi1982/ansiversa-api#5` was released by
Astra comment `5215395273` for architecture and documentation only. Codex
proposed a separate default-off non-production natural-language boundary at
`POST /api/v1/astra/agent/query`. Exact supported questions remain provider-
independent; unmatched current-turn language may produce only an untrusted
structured candidate from minimal app-owned certified capability metadata.
Deterministic validation must resolve one exact eligible Subscription Manager
capability and independently enforce parameters before constructing the
unchanged certified `AstraChatRequest`.

The provider is intent-only: no tools, DB access, writes, identity, authority,
grants, Runtime/Governance material, private records, final-answer generation,
persistent memory, or raw-prompt evidence persistence. Certified Runtime,
metadata activation, Read Authority, Read Execution, backend chat, frontend
chat, authentication, and Subscription Manager executable components remain
unchanged. The permanent GitHub-first delivery rule is in
`sources/30-astra-governed-ai-capability-delivery-workflow.md`; intent memory is
in `sources/31-astra-governed-natural-language-intent-architecture.md`.

ASTRA-AI-INTENT-ARCH-001 is Architecture Approved / Certified / Closed at
architecture commit `cc65502990e69c39bc542933d6d8d28aac5b0291` through Astra
architecture review `4881828844`. The backend documentation-only architecture
certification-record commit is
`00102d6669ff9021e7301f689d74090d760a2a03`; it is not a new architecture
target. PR #6 remains open, draft, and unmerged. Natural-language intent
implementation was later authorized only by separate GitHub issue #8 and is now
Implemented / Pending Astra Review at the commit recorded above. Architecture
certification itself did not authorize implementation, frontend, merge,
deployment, production configuration, or production action. Production remains
NOT APPROVED.

## Repository Baseline

Verified local repository heads:

```text
Frontend repository         ansiversa
Frontend HEAD               d6dc2b59a1dace03096d4359ededfbd1f082e9c5

Backend repository          ansiversa-api
Backend HEAD                615ef1b3ec375aacca9a9a9cb564832688a0d34c
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

## ASTRA-CHAT-001, Read Authority Binding, And Metadata Activation Binding Update

On 2026-08-06, Product Owner/Astra explicitly resumed ASTRA-CHAT-001 for
controlled non-production development and QA. The preserved chat history at
`681878d048c4b3229c312abfcaaa45b5e6a44459` was reconciled non-destructively
onto certified metadata prerequisite branch head
`06de785da513e04c19f1c59c1ec4a72ac0d42d28` in backend merge commit
`4d7d25fd1f95ef7fd3912a1cdc21ef43729e8646`. Parent conflicts were resolved in
favor of the certified metadata prerequisite, so the old chat-owned Capability
Discovery, Intent Resolution, Read Authority Binding, and fixture workarounds
do not survive. Chat now consumes
`runtime.issue_subscription_manager_governed_metadata_context(...)` and passes
the same exact context object through conversation-bound discovery and Intent
Resolution before certified read authority and execution.

The authenticated HTTP database-provenance test receives
`Subscriptions: 2.`, commits a third owner-scoped Subscription Manager row,
repeats the same governed request, and receives `Subscriptions: 3.`. Validation
passed with 27 chat tests, 264 focused tests plus 11 subtests, 450 full Astra
tests plus 33 subtests, compileall, and `git diff --check`. Astra certification
review `4876497721` approved ASTRA-CHAT-001 at certified executable
`4d7d25fd1f95ef7fd3912a1cdc21ef43729e8646`. ASTRA-CHAT-001 is Certified /
Approved. PR #3 remains open, draft, unmerged, and based on certified
ASTRA-META-ACT-BIND-001. The backend certification-record commit is
`615ef1b3ec375aacca9a9a9cb564832688a0d34c`, and production authorization
remains not approved.

## ASTRA-FE-CHAT-001 Frontend Update

On 2026-08-06, the approved governed Subscription Manager chat frontend was
implemented from exact frontend `main` base
`4681a23cc08240db8595941a2fee80989ad24825` on branch
`feature/astra-governed-subscription-chat`. The implementation commit is
`90c9a71581ec9145dc99363f12e276f5fbd227bf`. It reuses the existing shared
Astra panel and the existing authenticated frontend API boundary.

The panel provides a sealed deterministic mapping for the nine certified
Subscription Manager read capabilities and an explicit 1-366 day control for
`subscription.renewing_within_days`. Governed requests call only
`POST /api/v1/astra/chat`; unsupported input makes no request, and governed
failures never fall back to `/api/v1/assistant/query`. Requests use cookie
authentication, carry no user identity or authority fields, and keep the
backend conversation identifier only in component memory. Responses are
capability-checked and rendered as structured user-facing results without raw
JSON or backend internals. The feature is explicitly gated to recognized
non-production environments.

Astra review `4877041687` found that the frontend runtime allowlist included
`test`, while the certified backend supports only `local`, `development`, `qa`,
and `staging`, and that durable deployment language did not distinguish the
automatic non-production Vercel PR preview from a production deployment. The
narrow correction is frontend commit
`32930b69e8d296f383e2c9846bf5e69c231589a1`. The runtime allowlist now mirrors
the certified backend exactly. Tests prove local and development enablement,
optimized QA/staging enablement with an explicit application environment, and
fail-closed behavior for `test`, production, and a missing feature flag. The
Playwright web server uses the supported `development` application environment;
test convenience does not create another supported product environment.

Correction validation passed with frontend lint, typecheck, build, 14 focused
governed chat Playwright tests across Chromium and mobile Chromium, and
`git diff --check`. The existing Astra assistant suite passed 12 tests with one
credential-gated skip. Isolated live
browser QA used temporary migrated SQLite copies and the certified backend
branch: a primary user created two subscriptions through the normal UI and
received `Subscriptions: 2.`, created a third and received
`Subscriptions: 3.`, while a secondary user received `Subscriptions: 0.`.
Both governed calls used `/api/v1/astra/chat`, with zero legacy assistant-query
calls.

Astra certification review `4881607386` approved ASTRA-FE-CHAT-001 at certified
frontend implementation `32930b69e8d296f383e2c9846bf5e69c231589a1`, and the
Product Owner approved manual browser/product verification. The frontend
certification-record commit is `d6dc2b59a1dace03096d4359ededfbd1f082e9c5`
and changes documentation only; it is not the executable certification target.
ASTRA-FE-CHAT-001 is Certified / Approved / Closed. Frontend PR #1 is open,
draft, based on `main`, and unmerged. Backend PRs #3 and #4 remain open, draft,
and unmerged. No manual production deployment was performed or authorized.
GitHub/Vercel automatically created the normal non-production PR preview for
frontend PR #1. The preview does not authorize production; production remains
NOT APPROVED, and no additional deployment action is authorized. No production
configuration, authorization, or merge has occurred.

On 2026-08-02, ASTRA-CHAT-001 was implemented at backend commit
`d5c4c127c7c2fed254f7ee5463331306ca4d413b` after Product Owner/Astra
authorization to resume chat on top of the certified prerequisite chain. The
implementation adds a backend-only authenticated `/api/v1/astra/chat` route and
deterministic declared-intent chat gateway for certified Subscription Manager
read capabilities only. It routes through Conversation Context, declared Intent
Resolution, metadata-only Capability Discovery, ASTRA-READ-AUTH-BIND-001,
ASTRA-IMP-010 Read Access Authorization, ASTRA-READ-EXEC-001, and the
app-owned Subscription Manager adapter. This first implementation was later
reviewed as Changes Required. Production authorization remains not approved.

On 2026-08-02, Astra review `4838627730` found ASTRA-CHAT-001 Changes Required
at backend commit `d5c4c127c7c2fed254f7ee5463331306ca4d413b`. The first
correction was implemented at backend commit
`681878d048c4b3229c312abfcaaa45b5e6a44459`, but Astra re-review `4838708303`
found that it changed certified/frozen metadata parent contracts inside the chat
branch. ASTRA-CHAT-001 is paused on a new prerequisite and is not certified.
Production authorization remains not approved.

On 2026-08-02, Product Owner/Astra authorized ASTRA-META-ACT-BIND-001 as the
narrow prerequisite for exact governed metadata activation and capability
context binding. The backend implementation commit is
`7af01bb81a7bfa96d0e3b2d208ea9b4392b54517` on
`feature/astra-meta-act-bind-001`. It adds a Runtime-owned governed metadata
context issuer and exact context contract for
`app -> capability scope -> exact certified capability -> Conversation/Intent
metadata governance`, using certified ASTRA-RUNTIME-ACT-001 activation and
sealed Subscription Manager read-authority capability summaries as provenance.
It intentionally leaves ASTRA-READ-AUTH-BIND-001 executable behavior unchanged.
ASTRA-META-ACT-BIND-001 is implemented / pending Astra review and is not
certified. ASTRA-CHAT-001 remains paused until this prerequisite is reviewed and
certified.

On 2026-08-02, Astra review `4839027629` found ASTRA-META-ACT-BIND-001 Changes
Required at backend commit `7af01bb81a7bfa96d0e3b2d208ea9b4392b54517`. The
correction was implemented at backend commit
`ea8ff94d04dffd22c249de181c3145c2817f8e36`. Capability Discovery now validates
governed metadata contexts against the independently verified conversation
snapshot current turn and request reference, so old still-unexpired contexts
cannot govern a later turn and stale request references fail closed. Intent
Resolution now requires the same exact Runtime-issued metadata context object on
the intent request and Capability Discovery requester context, so two valid
contexts cannot be split across one metadata-governance lineage.
ASTRA-META-ACT-BIND-001 remains Changes Required / pending Astra re-review and
is not certified.

On 2026-08-02, Astra review `4839092431` found one remaining raw metadata
entry-point blocker at backend commit
`ea8ff94d04dffd22c249de181c3145c2817f8e36`. The final entry-point correction
was implemented at backend commit `c9d822a714e0d90f78e775096ddc737e4ed29f6e`.
Raw `discover_capabilities(...)` and `get_capability(...)` now reject governed
metadata contexts because they do not receive an independently certified
conversation snapshot. Governed metadata context can reach PRIVATE_READ metadata
Governance only through `discover_for_conversation(...)` after exact Runtime,
certified Conversation Context Engine, active current snapshot, current turn,
request reference, and exact Runtime-issued context validation. Generic
app-agnostic Capability Discovery without a governed context remains unchanged.

On 2026-08-02, Astra review `4839144244` found one remaining lifecycle-state
blocker at backend commit `c9d822a714e0d90f78e775096ddc737e4ed29f6e`. The final
lifecycle correction was implemented at backend commit
`0715483147d5a1a0ba6180d5a63e489f3b6fd982`. Governed conversation-bound
Capability Discovery now requires the independently verified owned conversation
snapshot lifecycle to be exactly ACTIVE before entering activation-backed
PRIVATE_READ metadata Governance. Still-unexpired governed contexts fail closed
after IDLE or CLOSING transitions. Generic non-governed Capability Discovery
lifecycle behavior remains unchanged.

On 2026-08-02, Astra certification review `4839188883` approved
ASTRA-META-ACT-BIND-001 at certified backend implementation
`0715483147d5a1a0ba6180d5a63e489f3b6fd982`. The backend certification-record
commit is `06de785da513e04c19f1c59c1ec4a72ac0d42d28` and changes documentation
only. ASTRA-META-ACT-BIND-001 is Certified / Approved and frozen at the
certified implementation. PR #4 remains open, draft, unmerged, and not
merge-authorized. ASTRA-CHAT-001 remains Changes Required / paused pending
explicit Product Owner/Astra resume and branch reconciliation onto this
certified prerequisite. Production authorization remains not approved.

ASTRA-RUNTIME-ACT-001 was Certified / Approved at backend commit
`a15b3192572cd5a1f3e265652e4778967755b787` after final Astra re-review approval
in PR #2 review `4837966223`. ASTRA-READ-AUTH-BIND-001 was Certified /
Approved at backend commit `6bf9e9e983711dbe65b18c98e6c47a45e117b02c` with
certification review `4838496452`. These prerequisites remain frozen.

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
ASTRA-READ-EXEC-001 behavior remains unchanged. ASTRA-META-ACT-BIND-001 is
Certified / Approved and frozen. ASTRA-CHAT-001 is Certified / Approved at
executable backend commit `4d7d25fd1f95ef7fd3912a1cdc21ef43729e8646`
through Astra certification review `4876497721`. Production authorization
remains not approved and production remains unchanged.

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
Frontend governed chat      Authorized for non-production implementation
Provider / Model            Not authorized
ASTRA-APP-VAL-001           Certified / Approved
ASTRA-READ-EXEC-001         Certified / Approved
ASTRA-CHAT-001              Certified / Approved
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

Still not authorized beyond the backend ASTRA-CHAT-001 orchestration route:

```text
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

## ASTRA-META-ACT-BIND-001 Memory

The backend contains a new implemented governed metadata activation binding
under:

```text
ansiversa-api/app/modules/astra_ai/metadata_activation_binding.py
```

Current state:

```text
ASTRA-META-ACT-BIND-001     Certified / Approved
Implementation Scope        Governed Metadata Activation & Capability Context Binding
Initial App                 Subscription Manager only
Initial Capability Scope    subscription_manager:private_read
Initial Backend Commit      7af01bb81a7bfa96d0e3b2d208ea9b4392b54517
First Astra Review          4839027629
Correction Backend Commit   ea8ff94d04dffd22c249de181c3145c2817f8e36
Second Astra Review         4839092431
Final Correction Commit     c9d822a714e0d90f78e775096ddc737e4ed29f6e
Third Astra Review          4839144244
Lifecycle Correction Commit 0715483147d5a1a0ba6180d5a63e489f3b6fd982
Certification Review        4839188883
Certified Implementation    0715483147d5a1a0ba6180d5a63e489f3b6fd982
Backend Certification Record 06de785da513e04c19f1c59c1ec4a72ac0d42d28
```

The binding creates a Runtime-owned, exact-object governed metadata context that
binds Runtime startup identity, Runtime-owned issuer authority, certified
non-production activation reference/digest, conversation ID, current turn
reference, request reference, Subscription Manager app ID, private-read
capability scope, exact certified adapter capability ID/version, bounded
expiration, and production-not-approved state.

Capability Discovery remains generic metadata-only and app-agnostic by default.
Without a valid Runtime-owned governed metadata context, internal metadata
governance remains public and fails closed under Stage-0 disabled Governance. A
valid context may authorize only the exact Subscription Manager private-read
metadata evaluation it was issued for, after Capability Discovery checks the
context against the independently verified current turn and request reference
from the certified conversation snapshot. Raw generic discovery and lookup entry
points fail closed when a governed metadata context is supplied. Governed
conversation-bound discovery also requires the owned conversation snapshot
lifecycle to be exactly ACTIVE.

Intent Resolution remains declared-intent only. It may resolve an exact
Subscription Manager capability from the trusted governed metadata context only
when the declared target exactly matches that context and the Capability
Discovery requester context carries the same exact Runtime-issued object.
Request-declared capability tuples are not treated as authority.

ASTRA-META-ACT-BIND-001 adds no chat endpoint, frontend, provider/model
integration, natural-language inference, RAG, embeddings, memory, adaptation,
writes, SQL/database execution, generic Tool Executor, additional app adapters,
schema changes, migrations, production configuration, deployment, production
authorization, or merge. ASTRA-READ-AUTH-BIND-001 executable contract and tests
remain unchanged.

Latest backend validation for lifecycle correction commit
`0715483147d5a1a0ba6180d5a63e489f3b6fd982`:

```text
.venv/bin/python -m compileall app/modules/astra_ai/metadata_activation_binding.py app/modules/astra_ai/capability_discovery.py app/modules/astra_ai/intent_resolution.py app/modules/astra_ai/runtime.py tests/test_astra_metadata_activation_binding.py
passed

.venv/bin/python -m pytest tests/test_astra_metadata_activation_binding.py -q
18 passed

.venv/bin/python -m pytest tests/test_astra_metadata_activation_binding.py tests/test_astra_runtime_activation.py tests/test_astra_capability_discovery_engine.py tests/test_astra_intent_resolution_engine.py tests/test_astra_conversation_context_engine.py tests/test_astra_governance_kernel.py tests/test_astra_runtime_core.py -q
173 passed, 11 subtests passed

.venv/bin/python -m pytest tests/test_astra_read_authority_binding.py tests/test_astra_read_execution_bridge.py tests/test_astra_read_access_authorization_engine.py tests/test_astra_app_val_001_read_execution_validation.py tests/test_subscription_manager_astra_read_capabilities.py -q
64 passed

.venv/bin/python -m pytest tests/test_astra_metadata_activation_binding.py tests/test_astra_runtime_activation.py tests/test_astra_capability_discovery_engine.py tests/test_astra_intent_resolution_engine.py tests/test_astra_conversation_context_engine.py tests/test_astra_governance_kernel.py tests/test_astra_runtime_core.py tests/test_astra_planning_engine.py tests/test_astra_read_authority_binding.py tests/test_astra_read_execution_bridge.py tests/test_astra_read_access_authorization_engine.py tests/test_astra_app_val_001_read_execution_validation.py tests/test_subscription_manager_astra_read_capabilities.py -q
267 passed, 11 subtests passed

.venv/bin/python -m compileall app/modules/astra_ai app/modules/auth app/modules/subscription_manager validation/astra_app_001 validation/astra_app_val_001 tests/test_astra_metadata_activation_binding.py
passed

git diff --check
passed

.venv/bin/python -m pytest tests/test_astra*.py -q
423 passed, 147 warnings, 33 subtests passed
```

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

ASTRA-READ-AUTH-BIND-001 is Certified / Approved. ASTRA-META-ACT-BIND-001 is
Certified / Approved and frozen at backend implementation
`0715483147d5a1a0ba6180d5a63e489f3b6fd982`. ASTRA-CHAT-001 is Certified /
Approved at executable backend commit
`4d7d25fd1f95ef7fd3912a1cdc21ef43729e8646` through Astra certification review
`4876497721`. Production authorization remains not approved.

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
astra/sources/27-astra-chat-orchestration.md
astra/sources/28-astra-metadata-activation-binding.md
astra/sources/29-astra-frontend-governed-subscription-chat.md
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
