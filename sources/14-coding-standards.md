# Coding Standards

## General Rule

Read existing code before editing. Follow established patterns. Do not invent architecture. If product intent or ownership is unclear, stop and ask Partner/Astra.

## Scope Control

Keep edits inside the requested mini-app boundary unless the task explicitly approves shared or platform changes. Avoid unrelated refactors, formatting churn, and metadata changes.

## TypeScript Standards

- Use strict typing from generated API schemas where available.
- Avoid `any` unless the surrounding code already requires it and there is no reasonable typed alternative.
- Keep DTO conversion explicit at the service/store boundary.
- Do not rely on accidental backend fields that are not in the response contract.

## React Standards

- Use existing hooks, stores, and shared components.
- Keep pages focused on composition and interaction.
- Keep domain state in Zustand stores where the module pattern uses stores.
- Avoid duplicating shared components.
- Avoid inline styles unless the local pattern already requires a tiny dynamic value.

## Store Standards

- Use `initialize()`, `refresh()`, and `reset()` where established.
- Prefer route loader -> store initialize -> render page when practical.
- Use shared store helpers such as `withStoreBusy`, `throwApiResponseError`, and `requireStoreData`.
- Clear stale feedback intentionally.

## API Standards

- Use the shared generated API client.
- Keep frontend payloads aligned with backend schemas.
- Do not send create-only parent IDs during updates.
- Keep list calls lightweight and load detail data from detail endpoints when needed.

## Route Standards

- Mini-app routes live under `/<app-slug>`.
- Overview route is `/<app-slug>`.
- First workflow route should be stable and used by `Explore`.
- Detail routes should use clear parameter names.
- Do not introduce subdomain mini-app routing.

## Folder Naming

- Frontend modules use kebab case: `src/modules/net-worth-tracker`.
- Backend modules use snake case: `app/modules/net_worth_tracker`.
- Migration folders use app slug style where established.

## UI Standards

- Buttons describe actions, not objects.
- Use icon-only record actions where practical.
- Use shared confirmation for destructive actions.
- Use shared feedback for user-visible results.
- Keep responsive layouts stable and text contained.

## Backend Standards

- Keep routers thin.
- Keep business rules in service/repository code.
- Validate ownership on every user-owned record operation.
- Use separate create/update schemas when behavior differs.
- Keep exception messages user-safe.

## Documentation Standards

- `story.md` describes current implementation, not history.
- `destination.md` describes the intended mature destination.
- `market-study.md` is external research, not a backlog.
- Update docs when workflow, database, API, UI, status, or major behavior changes.

## Testing Standards

- Add focused tests for changed behavior.
- Scale tests with risk and blast radius.
- Use existing Playwright infrastructure for browser coverage.
- Prefer deterministic test data and self-cleaning E2E records.

## Security Standards

Never commit or print passwords, API keys, database URLs, JWTs, cookies, Stripe secrets, production user lists, personal user data, or private test artifacts.
