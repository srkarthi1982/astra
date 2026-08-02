# Astra Chat Orchestration

Document Status: Durable memory supplement.

Created: 2026-08-02.

Implementation State: ASTRA-CHAT-001 Changes Required / Pending Astra Re-Review.

Backend Implementation Commit:
d5c4c127c7c2fed254f7ee5463331306ca4d413b.

Backend Correction Commit:
681878d048c4b3229c312abfcaaa45b5e6a44459.

Astra Re-Review:
4838627730.

Certification:
Pending Astra source/security/architecture review.

Production Authorization:
Not approved.

## Purpose

ASTRA-CHAT-001 adds the first backend-only governed chat orchestration path.
It exists only after the certified prerequisite chain was completed:

```text
ASTRA-RUNTIME-ACT-001
    -> ASTRA-READ-AUTH-BIND-001
    -> ASTRA-READ-EXEC-001
    -> ASTRA-APP-001 Subscription Manager read adapter
```

The goal is a narrow authenticated backend route that can turn an explicit
declared intent into a governed Subscription Manager read and a bounded
deterministic chat response.

## Backend Surface

Route:

```text
POST /api/v1/astra/chat
```

Backend modules:

```text
ansiversa-api/app/modules/astra_ai/api/chat.py
ansiversa-api/app/modules/astra_ai/chat_gateway.py
```

The route is registered only for known non-production environments. It still
fails closed unless Runtime startup and non-production read activation are
valid. Production remains unavailable and not approved.

## Request Contract

The request contract is explicit and bounded:

```text
conversation_id optional
declared_intent optional
declared_intent.app_id
declared_intent.declared_action
declared_intent.declared_subject
declared_intent.capability_id
declared_intent.parameters
requested_field_references optional
requested_row_limit optional
client_request_reference optional
```

The gateway requires the existing backend authenticated request boundary through
`get_authenticated_user_context`. Normal callers do not receive or provide
private Runtime authority, read decisions, app grants, owner acceptance objects,
or user/owner IDs as authority.

## Supported Initial Intent

The only successful initial app scope is Subscription Manager:

```text
app_id = subscription_manager
declared_action = get_information
declared_subject = subscription
capability_id = certified Subscription Manager read capability
```

Supported adapter capabilities:

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

Missing declared intent returns a clarification response. Unsupported apps or
capabilities return bounded unavailable responses. No natural-language
inference, provider/model call, prompt processing, RAG, embeddings, memory, or
adaptation exists in this implementation.

## Governed Execution Chain

The positive path is:

```text
get_authenticated_user_context
    -> AstraChatGateway
    -> AstraConversationContextEngine
    -> AstraIntentResolutionEngine
    -> AstraCapabilityDiscoveryEngine metadata-only governance
    -> runtime.read_authority.authorize_subscription_manager_read(...)
    -> ASTRA-IMP-010 Read Access Authorization
    -> app-owned Subscription Manager read grant
    -> runtime.read_execution.issue_request(...)
    -> runtime.read_execution.execute(...)
    -> Subscription Manager registered adapter
    -> bounded deterministic chat response
```

Planning remains metadata-only and may be absent:

```text
plan_reference = None
plan = None
```

Capability Discovery remains metadata-only. It does not receive executable app
read capabilities. Generic Runtime-internal Capability Discovery no longer
receives ambient Subscription Manager private-read activation merely because the
caller is Runtime-owned. Chat supplies explicit per-request orchestration
context for the exact app, capability scope, and declared Subscription Manager
capability.

Intent Resolution remains declared-intent only. It no longer infers
Subscription Manager activation from `get_information` plus
subscription-looking subject strings. Chat binds the declared Subscription
Manager capability into:

```text
declared-intent binding target
AstraIntentRequest declared_target
AstraIntentRequest declared_capability_ids
AstraIntentResolution.resolved_capability_ids
Read Authority adapter_capability_id
Read Execution adapter_capability_id
```

Mismatched, changed, or reused capability lineage fails closed.

## Security Boundary

The chat gateway binds each conversation to the exact authenticated principal.
A different principal cannot reuse the conversation ID. Caller-supplied owner
or user fields are rejected by the request contract, and a caller cannot change
ownership through Subscription Manager records.

The chat gateway does not import SQLAlchemy, create or own a database session,
call Subscription Manager repositories, or execute SQL. The API route passes the
Subscription Manager database dependency only into the certified Read Execution
bridge, where the app-owned adapter remains the first SQL boundary.

The response contract is bounded through structural projection. Chat projects
Subscription Manager summaries and records through allowlisted fields and
rejects unsupported private metadata keys. It does not keyword-scan app-owned
business values, so legitimate values such as `1Password` and `SQL Server`
remain returnable when the governed capability authorizes those fields.
Projection failures return bounded non-success chat responses rather than
unhandled server errors.

## Explicit Non-Goals

ASTRA-CHAT-001 does not implement:

```text
frontend chat UI
provider/model/OpenAI integration
LLM calls
natural-language inference
RAG or embeddings
persistent memory or adaptation
writes or mutations
generic Tool Executor
additional app adapters
schema changes
migrations
production configuration
deployment
production authorization
merge
```

## Validation Evidence

Latest backend validation for correction commit
`681878d048c4b3229c312abfcaaa45b5e6a44459`:

```text
.venv/bin/python -m compileall app/modules/astra_ai/chat_gateway.py app/modules/astra_ai/api/chat.py app/main.py
passed

.venv/bin/python -m pytest tests/test_astra_chat_gateway.py -q
21 passed, 1 warning

.venv/bin/python -m pytest tests/test_astra_intent_resolution_engine.py tests/test_astra_capability_discovery_engine.py -q
48 passed

.venv/bin/python -m pytest tests/test_astra_runtime_activation.py tests/test_astra_read_authority_binding.py tests/test_astra_read_execution_bridge.py tests/test_astra_read_access_authorization_engine.py tests/test_astra_app_val_001_read_execution_validation.py tests/test_subscription_manager_astra_read_capabilities.py tests/test_astra_conversation_context_engine.py tests/test_astra_intent_resolution_engine.py tests/test_astra_capability_discovery_engine.py tests/test_astra_planning_engine.py tests/test_astra_governance_kernel.py tests/test_astra_runtime_core.py tests/test_astra_chat_gateway.py -q
270 passed, 1 warning, 11 subtests passed

.venv/bin/python -m compileall app/modules/astra_ai app/modules/auth app/modules/subscription_manager validation/astra_app_001 validation/astra_app_val_001 tests/test_astra_chat_gateway.py
passed

.venv/bin/python -m pytest tests/test_astra*.py -q
426 passed, 147 warnings, 33 subtests passed in 463.16s
```

ASTRA-CHAT-001 remains Changes Required / pending Astra re-review. It is not
certified. Production authorization remains not approved.
