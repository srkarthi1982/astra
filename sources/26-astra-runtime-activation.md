# Astra Runtime Activation

Document Status: Durable memory supplement.

Created: 2026-08-02.

Implementation State: ASTRA-RUNTIME-ACT-001 implemented / pending Astra review
and certification.

Backend Implementation Commit:
fd61ee1071227549500785e0c8a663cf5e2f8082.

## Purpose

ASTRA-RUNTIME-ACT-001 exists because ASTRA-READ-AUTH-BIND-001 review exposed a
real activation prerequisite. Stage-0 Astra configuration intentionally remains
globally disabled, and the Governance Kernel fails closed while that global
configuration is disabled. A real non-production governed private-read path
therefore needs a separate, bounded activation contract rather than an in-place
semantic rewrite of Stage-0 configuration.

## Implemented Boundary

Backend module:

```text
ansiversa-api/app/modules/astra_ai/activation.py
```

Server setting:

```text
ASTRA_NONPROD_READ_ENABLED
```

The setting defaults to `false`. Unknown values fail closed. Production
activation is prohibited even if the setting is true.

## Activation Scope

The first activation covers only:

```text
app: subscription_manager
capability scope: subscription_manager:private_read
authority: advisory / read_only
safety: private_read
environment: local / development / qa / staging
production authorization: not_approved
provider: disabled
memory: disabled
adaptation: disabled
writes: disabled
```

## Runtime Ownership

Runtime loads activation during startup and owns the immutable activation state.
Runtime injects its own activation context into Governance evaluation and does
not trust caller-supplied activation context in normal Runtime evaluation.

The read-only Runtime projection is metadata-only:

```text
runtime.activation
runtime.health(...).activation
```

## Governance Role

Activation is one necessary condition for the first non-production operational
Astra read capability. It is not read authorization, app owner acceptance, read
execution, or production authorization.

When Stage-0 remains disabled, Governance can allow only if a Runtime-owned
activation context covers the exact runtime instance, non-production
environment, app, capability scope, authority class, safety class, and disabled
provider/memory/adaptation/execution-handoff flags.

All other Governance fail-closed, approval, consent, owner-authority,
production, and constitutional checks remain active.

## Downstream State

```text
ASTRA-READ-AUTH-BIND-001    Changes Required / Paused
ASTRA-CHAT-001              Authorized / Paused
Production                  NOT APPROVED
```
