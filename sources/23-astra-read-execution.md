# Astra Read Execution

Document Status: Current implementation memory.

Created: 2026-07-29.

Purpose: record ASTRA-READ-EXEC-001, the first governed bridge from certified
Astra read authorization into a certified app-owned read adapter.

## Status

```text
ASTRA-READ-EXEC-001          Certified / Approved
Implementation Scope         Governed Read Execution Bridge
Implementation Review        Approved
Validated By                 ASTRA-APP-VAL-001
Product Owner Approval       Approved
Certification                Passed
Implementation Commit        15c017b327635f29fe9ebc30132fb6a39a87d0ef
Validation Commit            19bc1e34feb4556f5dd7c4117536ba9d72ba8365

Initial Adapter              Subscription Manager only
ASTRA-APP-001                Certified / Approved
ASTRA-APP-VAL-001            Certified / Approved
ASTRA-CHAT-001               Not authorized

Production Authorization     Not approved
Production                   Unchanged
```

## Architecture Boundary

The bridge is Runtime-owned and backend-only. It does not add a public API
route, frontend chat, provider/model invocation, general tool execution,
dynamic import loading, persistent memory, database schema changes, migrations,
telemetry, deployment, or production configuration.

The existing certified Runtime component registry remains unchanged. Read
execution is exposed through a narrow Runtime interface, not as a new certified
health component.

## Execution Contract

The authorized flow is:

```text
Astra Runtime
      ↓
Runtime-registered read authorization decision
      ↓
Runtime-issued read execution request
      ↓
Governed read execution bridge
      ↓
Explicit app-owned adapter registry
      ↓
Subscription Manager one-time read grant
      ↓
Subscription Manager certified read capability
      ↓
Validated bounded read result
      ↓
Astra Runtime
```

The bridge requires:

- an exact Runtime-registered `AstraReadAuthorizationDecision`;
- `authorized_metadata_only` decision status;
- production read state `not_approved`;
- no Astra-owned database or SQL authorization;
- an exact Runtime-issued read execution request;
- an exact app-owned Subscription Manager read grant;
- authenticated subject, principal, request reference, result limit, app,
  capability, version, and execution-context match;
- an explicitly registered adapter;
- read-only operation.

## Adapter Registry

Only Subscription Manager is registered initially:

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

No other app, capability, dynamic import, cross-app read, write operation, or
mutation path is registered.

## Validation Evidence

Focused backend tests cover:

- successful Runtime-owned execution through Subscription Manager;
- copied request rejection;
- one-time grant reuse rejection;
- authenticated subject mismatch;
- capability mismatch;
- execution-context mismatch;
- unsupported app rejection;
- unregistered adapter rejection;
- non-read operation rejection;
- invalid adapter output rejection;
- redaction/privacy failure;
- Runtime shutdown invalidation.

ASTRA-APP-VAL-001 formally validates the Subscription Manager execution path.
Its certified validation records prove no SQL execution occurs before
registered Subscription Manager adapter entry, and Runtime results expose no
session, SQL, database handle, or private authority material.

## Unresolved Authorization Boundaries

These remain outside the implemented and certified scope until separately
authorized:

```text
ASTRA-CHAT-001               Not authorized
Provider / Model             Not authorized
General Tool Executor        Not authorized
Additional app adapters      Not authorized
Write / Mutation execution   Not authorized
Production read execution    Not approved
```

Production remains unchanged.
