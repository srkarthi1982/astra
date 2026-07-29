# Backend Contracts

This file is the backend source of truth for Ansiversa module architecture and API behavior.

## Module Layout

Mini-app backend modules live under `ansiversa-api/app/modules/<app_module>`. Standard files include:

- `models.py` for SQLAlchemy models.
- `schemas.py` for request and response DTOs.
- `service.py` for business logic.
- `repository.py` when persistence logic is large enough to separate.
- `router.py` or `routes.py` for FastAPI routes.
- `db.py` for isolated database binding where the app has its own database.
- `constants.py` for stable module constants such as version table names.
- `story.md`, `destination.md`, `market-study.md`, and `marketing.md` where required.

Follow the module's existing pattern before adding new files.

## Router Contract

Routers should stay thin. They validate request shape, resolve authenticated user context, call service functions, and return response DTOs. Business rules belong in service/repository code, not in route handlers.

## Service Contract

Services own product behavior: ownership checks, validation, duplicate policy, status transitions, calculations, soft-delete/archive rules, pagination decisions, and response assembly.

## Repository Contract

Repositories are optional and should be added when they remove real persistence complexity. Do not introduce repository layers only for style consistency if a module is intentionally small.

## Response Contract

APIs must return only frontend-required fields.

List endpoints return lightweight summaries. Dashboard endpoints return summaries only. Detail endpoints return complete records required for view/edit. Create and update endpoints return the fields needed by the current frontend workflow.

Do not rely on accidental ORM properties or oversized response models.

## Exception Handling

Use consistent HTTP exceptions and user-safe messages. Do not expose stack traces, database URLs, raw SQL errors, secret values, JWTs, cookies, or private infrastructure details.

## Ownership Validation

Every user-owned record must be scoped by the authenticated user. Detail, update, delete, archive, restore, and child-record operations must verify ownership through the parent record or direct owner field.

Cross-account access should return a safe not-found or forbidden response according to established module behavior.

## Duplicate Validation Policy

Duplicate rules should match product intent. When names are user-facing identifiers, validate duplicates within the owner scope, usually case-insensitively. Do not add global uniqueness unless the product requires global uniqueness.

## Create/Update DTO Policy

Create and update schemas must be reviewed independently. Create-only parent IDs should not appear in update payloads unless moving a record between parents is explicitly supported and validated.

## Archive And Soft Delete Rules

Archive is a reversible status transition. Archived records should usually be read-only except for restore unless the product explicitly supports editing archived records.

Soft delete preserves data and usually hides records from default lists. Hard delete removes records and must respect cascade/restrict rules.

## Delete Rules

Delete behavior must match data ownership and relationship safety. Parent deletes may cascade only when child records are fully owned and safe to remove. Otherwise restrict and return a clear user-safe message.

## Pagination Policy

List endpoints should support stable `page` and `pageSize` values where lists can grow. Return total count and current page metadata when the frontend needs pagination.

## Naming Conventions

Frontend slugs use kebab case. Backend modules use snake case. Database environment variable names use uppercase snake case plus `_DATABASE_URL`. API routes use `/api/v1/<app-slug>/...`.

## Database Index Policy

Indexes must come from user-facing query patterns: owner lists, created/updated sorting, parent lookups, dashboard/status filters, timeline/history queries, detail navigation, and frequent ordering columns. Avoid speculative indexes and indexes on large text/blob/json fields unless explicitly required.

## Migration Contract

Persistent tables require Alembic migrations. Production migration verification is separate from local migration success. Migration heads and version table names should be recorded in `07-ansiversa-database-registry.json`.

## Security Contract

Never store or log passwords, API keys, database URLs, JWTs, cookies, Stripe secrets, production user lists, or personal user data in docs, generated registries, test artifacts, or source-pack files.

## Astra Governed Read Execution

ASTRA-READ-EXEC-001 introduces a backend-only Runtime-owned read execution
bridge. The bridge may execute only an explicitly registered app-owned adapter
after a certified read authorization decision and exact app-owned read grant
match the authenticated subject, app, capability, operation, request reference,
result limit, and execution context.

Initial scope is Subscription Manager only. Astra-owned SQL, direct Astra app
database access, dynamic imports, cross-app execution, write/mutation
execution, public API routes, frontend chat, provider/model calls, persistent
memory, deployment, and production configuration remain outside the contract.
