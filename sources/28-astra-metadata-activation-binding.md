# Astra Metadata Activation Binding

Document Status: Durable memory supplement.

Created: 2026-08-02.

Implementation State: ASTRA-META-ACT-BIND-001 Implemented / Pending Astra Review.

Backend Branch:
feature/astra-meta-act-bind-001.

Backend Base Commit:
e6ba6a662d4cc8b88ff237a993efed59495baa7a.

Backend Implementation Commit:
7af01bb81a7bfa96d0e3b2d208ea9b4392b54517.

Certification:
Pending Astra source/security/architecture review.

Production Authorization:
Not approved.

## Purpose

ASTRA-META-ACT-BIND-001 is the narrow prerequisite created after the
ASTRA-CHAT-001 re-review found that chat could not safely extend certified
metadata parent contracts inside the chat branch.

Its job is to provide a Runtime-owned, exact, bounded metadata context for:

```text
app -> capability scope -> exact certified capability -> Conversation/Intent metadata governance
```

It adds no execution authority. It exists only to bind certified non-production
activation and certified Subscription Manager read capability provenance into
metadata-only Capability Discovery and declared-intent-only Intent Resolution.

## Backend Surface

New module:

```text
ansiversa-api/app/modules/astra_ai/metadata_activation_binding.py
```

Integrated modules:

```text
ansiversa-api/app/modules/astra_ai/runtime.py
ansiversa-api/app/modules/astra_ai/capability_discovery.py
ansiversa-api/app/modules/astra_ai/intent_resolution.py
```

Focused tests:

```text
ansiversa-api/tests/test_astra_metadata_activation_binding.py
```

ASTRA-READ-AUTH-BIND-001 executable code and tests are unchanged by this branch.

## Context Contract

`AstraGovernedMetadataContext` is a frozen exact-object contract. It binds:

```text
Runtime startup instance ID
Runtime-owned metadata issuer authority
exact context object identity
certified activation reference
certified activation digest
conversation ID
current turn reference
request reference
Subscription Manager app ID
subscription_manager:private_read capability scope
exact certified adapter capability ID
exact certified adapter capability version
bounded issuance/expiration window
production-not-approved state
```

Caller-created, copied, tampered, expired, wrong Runtime, wrong conversation,
wrong turn, wrong request, wrong app, wrong scope, wrong capability, and wrong
version contexts fail closed.

## Runtime Issuance And Validation

Only `AstraRuntime` creates the governed metadata context issuer. Issuer
construction requires the actual Runtime owner, the matching Runtime startup
instance ID, and the exact Runtime-owned metadata issuer authority.

Runtime issues contexts only through
`issue_subscription_manager_governed_metadata_context(...)`, after validating:

```text
Runtime is started and ready
certified ASTRA-RUNTIME-ACT-001 activation is loaded
activation covers Subscription Manager READ_ONLY and ADVISORY private-read scope
conversation engine is Runtime-owned
conversation snapshot is exact and active
current turn exists
adapter capability comes from sealed read-authority capability summaries
```

Runtime validates contexts only through
`validates_governed_metadata_context(...)`, which delegates exact-object checks
to the issuer registry and exact request identity checks.

## Metadata Components

Capability Discovery remains metadata-only. Generic internal requests without a
governed metadata context continue to evaluate as public metadata and fail closed
under Stage-0 disabled Governance. A valid context may scope Governance evidence
to Subscription Manager private-read metadata only.

Intent Resolution remains declared-intent only. It may resolve the exact
capability from the trusted governed metadata context only when
`declared_target` exactly matches the context capability ID. Structural request
tuples are not capability authority.

## Boundaries

ASTRA-META-ACT-BIND-001 does not implement:

```text
chat endpoint or chat service
frontend
provider/model/OpenAI integration
LLM calls
natural-language inference
RAG or embeddings
persistent memory or adaptation
writes or mutations
generic Tool Executor
additional app adapters
direct SQL/database access
schema changes
migrations
production configuration
deployment
production authorization
merge
```

Certified ASTRA-RUNTIME-ACT-001 activation semantics remain frozen.
ASTRA-READ-AUTH-BIND-001 executable authorization behavior remains frozen.
ASTRA-READ-EXEC-001 behavior remains unchanged.

## Validation Evidence

Latest backend validation for implementation commit
`7af01bb81a7bfa96d0e3b2d208ea9b4392b54517`:

```text
.venv/bin/python -m compileall app/modules/astra_ai/metadata_activation_binding.py app/modules/astra_ai/capability_discovery.py app/modules/astra_ai/intent_resolution.py app/modules/astra_ai/runtime.py tests/test_astra_metadata_activation_binding.py
passed

.venv/bin/python -m pytest tests/test_astra_metadata_activation_binding.py -q
9 passed

.venv/bin/python -m pytest tests/test_astra_metadata_activation_binding.py tests/test_astra_runtime_activation.py tests/test_astra_capability_discovery_engine.py tests/test_astra_intent_resolution_engine.py tests/test_astra_conversation_context_engine.py tests/test_astra_governance_kernel.py tests/test_astra_runtime_core.py -q
164 passed, 11 subtests passed

.venv/bin/python -m pytest tests/test_astra_read_authority_binding.py tests/test_astra_read_execution_bridge.py tests/test_astra_read_access_authorization_engine.py tests/test_astra_app_val_001_read_execution_validation.py tests/test_subscription_manager_astra_read_capabilities.py -q
64 passed

.venv/bin/python -m pytest tests/test_astra_metadata_activation_binding.py tests/test_astra_runtime_activation.py tests/test_astra_capability_discovery_engine.py tests/test_astra_intent_resolution_engine.py tests/test_astra_conversation_context_engine.py tests/test_astra_governance_kernel.py tests/test_astra_runtime_core.py tests/test_astra_planning_engine.py tests/test_astra_read_authority_binding.py tests/test_astra_read_execution_bridge.py tests/test_astra_read_access_authorization_engine.py tests/test_astra_app_val_001_read_execution_validation.py tests/test_subscription_manager_astra_read_capabilities.py -q
258 passed, 11 subtests passed

.venv/bin/python -m compileall app/modules/astra_ai app/modules/auth app/modules/subscription_manager validation/astra_app_001 validation/astra_app_val_001 tests/test_astra_metadata_activation_binding.py
passed

git diff --check
passed

.venv/bin/python -m pytest tests/test_astra*.py -q
414 passed, 147 warnings, 33 subtests passed
```

ASTRA-META-ACT-BIND-001 remains implemented / pending Astra review. It is not
certified. ASTRA-CHAT-001 remains paused. Production authorization remains not
approved.
