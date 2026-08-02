# Astra Runtime Activation

Document Status: Durable memory supplement.

Created: 2026-08-02.

Implementation State: ASTRA-RUNTIME-ACT-001 implemented / changes required /
pending Astra re-review and certification.

Backend Implementation Commit:
fd61ee1071227549500785e0c8a663cf5e2f8082.

Backend Correction Commit:
f1af573917b93f0ebe15e133a46f49a33cf1541f.

Backend Final Correction Commit:
942fae7473be5267d7b5218ea8e3977f28fbd058.

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

Activation authority is exact-object Runtime ownership, not matching metadata.
Runtime creates an activation issuer for the startup instance through a
module-private Runtime activation issuer root-of-trust. Caller-created issuer
construction with caller-owned `_runtime_authority=object()` is rejected. The
issuer stores exact issuer identity and exact issued activation object identity
in a Runtime-owned registry. Copied, reconstructed, tampered, foreign-Runtime,
and post-shutdown activation objects cannot establish activation authority.

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

Governance also requires safe activation provenance:

```text
activation_reference
activation_digest
```

These are populated by Runtime from the exact activation object. The serialized
Governance input and resulting evidence digest cover them, and evidence
provenance records the activation reference. Private Runtime issuer authority is
not serialized.

Activation is lifecycle-bound to the Runtime startup instance. It does not use a
short startup TTL. Runtime shutdown invalidates the issuer registry, making the
previous activation unusable.

All other Governance fail-closed, approval, consent, owner-authority,
production, and constitutional checks remain active.

## Final Correction Evidence

Backend final correction commit `942fae7473be5267d7b5218ea8e3977f28fbd058`
addresses the remaining Astra blocker from correction commit `f1af573...` by
making issuer ownership itself Runtime-authoritative.

The required negative is enforced:

```text
AstraRuntimeActivationIssuer(
    runtime_instance_id=RUNTIME_ID,
    issuer_reference="caller",
    _runtime_authority=object(),
)
```

This construction raises `AstraRuntimeActivationError`; it never produces a
self-consistent activation that direct Governance can allow.

The required positive uses a real `AstraRuntime` startup path with the
Runtime-created activation issuer, exact live Runtime-issued activation, and the
real Governance Kernel. No governance monkeypatch is used.

Focused tests prove:

```text
directly constructed activation -> FAIL_CLOSED
copied activation -> FAIL_CLOSED
caller-created issuer activation -> construction rejected
foreign Runtime activation -> FAIL_CLOSED
tampered activation reference -> FAIL_CLOSED
tampered activation digest -> FAIL_CLOSED
post-shutdown activation -> FAIL_CLOSED
exact live Runtime activation -> ALLOW when all governed scope checks match
```

## Downstream State

```text
ASTRA-READ-AUTH-BIND-001    Changes Required / Paused
ASTRA-CHAT-001              Authorized / Paused
Production                  NOT APPROVED
```
