# Astra Read Authority Binding

Document Status: Durable memory supplement.

Created: 2026-08-02.

Implementation State: ASTRA-READ-AUTH-BIND-001 implemented / pending Astra
review and certification.

Backend Implementation Commit:
b9dfceefc3352233e474eb91a04861431b4e5731.

## Purpose

ASTRA-READ-AUTH-BIND-001 exists because ASTRA-CHAT-001 preflight found a real
certified-contract gap. The Runtime had Conversation Context, Intent
Resolution, Read Access Authorization, Governed Read Execution, and a certified
Subscription Manager app-owned read adapter, but normal Runtime-owned
application code could not yet bind app-owned read capability metadata and
Runtime-owned proof issuers into ASTRA-IMP-010 without validation-only private
mutation.

ASTRA-CHAT-001 remains authorized but paused until this prerequisite is
reviewed, approved, and certified.

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
    -> app-owned Subscription Manager read grant
    -> ASTRA-IMP-010 Read Access Authorization
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

Owner acceptance is derived from an exact app-owned Subscription Manager read
grant. The binding component validates the grant through the app-owned grant
issuer and does not fabricate app authority.

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
