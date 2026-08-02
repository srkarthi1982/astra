# Astra App Validation

Document Status: Current validation memory.

Created: 2026-07-29.

Purpose: record ASTRA-APP-VAL-001, the validation milestone for Subscription
Manager governed read execution through ASTRA-READ-EXEC-001.

## Status

```text
ASTRA-APP-VAL-001            Certified / Approved
Implementation Scope         Subscription Manager Governed Read Execution Validation
Astra Source Review          Approved
Security Review              Approved
Partner Review               Approved
Product Owner Approval       Approved
Certification                Passed
Backend Commit               19bc1e34feb4556f5dd7c4117536ba9d72ba8365

Validated Parent             ASTRA-READ-EXEC-001 Certified / Approved
Validated App Adapter        ASTRA-APP-001 Certified / Approved
Initial Adapter              Subscription Manager only

ASTRA-CHAT-001               Backend implemented / pending Astra review
Provider / Model             Not authorized
Production Authorization     Not approved
Production                   Unchanged
```

## Validation Coverage

ASTRA-APP-VAL-001 validates:

- Runtime-produced read execution requests;
- read authorization enforcement at execution registration/request boundaries;
- explicit Subscription Manager adapter selection;
- app-owned read execution;
- structured result validation;
- redaction and forbidden-material absence;
- fail-closed handling for copied, reused, malformed, non-read, and
  subject-mismatched requests;
- unchanged production and mutation boundaries;
- database-session ownership proof.

## Database-Session Boundary Proof

The validation runner uses a tracking SQLAlchemy session. The registered
adapter wrapper observes that no SQL execution has occurred before adapter
entry. The app-owned Subscription Manager adapter then uses the session for its
own read. The Runtime result does not expose the session, database handle, SQL,
or private adapter authority.

This records the current bridge as opaque session transport only. A future
stronger design may replace this with an app-owned callable/service boundary,
but that is outside ASTRA-APP-VAL-001.

## Not Authorized

```text
Frontend chat
Provider / Model
General Tool Executor
Additional app adapters
Write / Mutation execution
Production read execution
Production configuration
Database schema or migration changes
```
