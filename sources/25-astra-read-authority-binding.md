# Astra Read Authority Binding

Document Status: Durable memory supplement.

Created: 2026-08-02.

Implementation State: ASTRA-READ-AUTH-BIND-001 Certified / Approved.

Backend Implementation Commit:
b9dfceefc3352233e474eb91a04861431b4e5731.

Backend Correction Commit:
6bf9e9e983711dbe65b18c98e6c47a45e117b02c.

Certification Review:
4838496452.

Certification closure records approval only. PR #1 remains open, draft,
unmerged, and mergeable at certification time. No merge or production
authorization is included.

## Purpose

ASTRA-READ-AUTH-BIND-001 exists because ASTRA-CHAT-001 preflight found a real
certified-contract gap. The Runtime had Conversation Context, Intent
Resolution, Read Access Authorization, Governed Read Execution, and a certified
Subscription Manager app-owned read adapter, but normal Runtime-owned
application code could not yet bind app-owned read capability metadata and
Runtime-owned proof issuers into ASTRA-IMP-010 without validation-only private
mutation.

ASTRA-CHAT-001 is now Changes Required / pending Astra re-review.

## Implemented Boundary

Backend module:

```text
ansiversa-api/app/modules/astra_ai/read_authority_binding.py
```

Runtime surface:

```text
runtime.read_authority.capabilities()
runtime.read_authority.authorize_subscription_manager_read(...)
```

The surface is narrow. It does not expose private issuer tokens, registration
authority, mutable registries, SQLAlchemy sessions, database handles, SQL,
private Runtime objects, or execution authority material.

## Architecture

The implemented path is:

```text
Subscription Manager app-owned read declarations
    -> sealed Runtime read capability registry
    -> Runtime-owned proof issuers
    -> existing backend auth-owned user context
    -> app-owned Subscription Manager owner acceptance
    -> ASTRA-IMP-010 Read Access Authorization
    -> app-owned Subscription Manager read grant with actual read and
       Governance decision identity
    -> Runtime registration with ASTRA-READ-EXEC-001
```

Planning may remain absent for non-planning read-only information requests:

```text
plan_reference = None
plan = None
```

Capability Discovery remains metadata-only and does not receive executable
Subscription Manager read capabilities. Planning remains metadata-only and does
not become an execution engine. ASTRA-READ-EXEC-001 remains the only governed
read execution bridge.

## Subscription Manager Scope

Only Subscription Manager / App #071 is in scope. The certified capability
family remains:

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

Subscription Manager owns the declarations through its backend module. Astra
registers those explicit declarations but does not duplicate Subscription
Manager business logic.

## Authority Model

Runtime-owned issuers cover:

```text
principal
user
tenant
app
record
field
purpose
owner_acceptance
```

Owner acceptance is derived from an exact app-owned Subscription Manager owner
acceptance before Runtime proof issuance. The binding component validates that
acceptance through the app-owned Subscription Manager authority and does not
fabricate app authority.

The app-owned execution grant is issued only after real Runtime/Governance read
authorization returns `AUTHORIZED_METADATA_ONLY`. The grant contains the actual
read authorization decision identity and the actual Governance decision
reference. ASTRA-READ-AUTH-BIND-001 does not predict or manufacture Governance
decision IDs.

Read authorization binds into the certified ASTRA-RUNTIME-ACT-001 activation
scope through:

```text
requested_app_id = subscription_manager
requested_capability_scope = subscription_manager:private_read
owner_authority_status = verified
```

The binding requires a sealed backend-auth-owned `AuthenticatedUserContext`
issued only by the existing authenticated backend request boundary. The issuer
requires bearer token or auth cookie resolution, access-token decoding, token
expiration binding, existing DB user lookup by token subject/email,
login-status validation, auth-owned SQLAlchemy persistence validation, timing
user binding, and a module-private authenticated-request-boundary authority.
Persistent users obtained directly from `db.get(...)`, transient
caller-created `User(...)` objects, caller-constructed contexts,
copied/tampered/foreign contexts, expired/stale contexts, and
disabled/inactive/suspended users cannot establish or preserve principal/user
read authority. The auth-owned context registry is bounded and removes expired
contexts during issuance and expiration validation.

Subscription Manager has no tenant or organization authority model in this
repository. Read capability tenant scope is therefore represented explicitly as
`tenant:not_applicable`, not as a fabricated platform tenant.

Owner acceptance is validated against the complete current request: app
identity/scope, adapter capability/version, read capability, principal, request
reference, subject, tenant-not-applicable semantics, record scope, fields,
purpose, parameters, and result limit.

## Explicit Non-Goals

ASTRA-READ-AUTH-BIND-001 does not implement:

```text
chat
frontend
provider/model integration
natural-language inference
SQL/database execution in the binding component
schema or migration changes
writes/mutations
additional app adapters
generic plugin registration
production configuration
deployment
```

Production authorization remains not approved. Production remains unchanged.

## Validation Evidence

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
`4838496452`. ASTRA-CHAT-001 is Changes Required / pending Astra re-review at
backend correction commit `681878d048c4b3229c312abfcaaa45b5e6a44459`.
Production authorization remains not approved.
