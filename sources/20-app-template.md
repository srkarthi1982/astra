# App Template

This is the canonical blueprint for a new Ansiversa mini app.

## Identity

- App number.
- Canonical name.
- Slug.
- Category.
- Backend module name.
- Database environment variable name.
- First workflow route.
- Overview route.
- Explore route.

## Backend

Expected location:

```text
ansiversa-api/app/modules/<app_module>/
```

Expected files when the app is persistent:

```text
__init__.py
constants.py
db.py
models.py
schemas.py
service.py
router.py or routes.py
market-study.md
destination.md
story.md
marketing.md
```

Expected migration location:

```text
ansiversa-api/migrations/<app-slug>/
```

Backend requirements:

- User ownership validation.
- Lightweight list/dashboard responses.
- Detail responses for view/edit.
- Independent create/update schemas.
- Index review based on query patterns.
- Clear duplicate validation policy.
- Archive/restore policy where applicable.
- User-safe exception handling.

## Frontend

Expected location:

```text
ansiversa/src/modules/<app-slug>/
```

Expected structure:

```text
index.tsx
pages/
services/
stores/
content/ or module content file when needed
story.md
```

Frontend requirements:

- Overview page with `Explore` CTA.
- Protected first workflow route.
- CRUD for long-lived user-created records.
- Shared forms, feedback, pagination, and record actions where applicable.
- Responsive desktop, tablet, and mobile layouts.
- Generated API types instead of hand-rolled DTO guesses.

## Documentation

Required during initial development:

- Backend `market-study.md`.
- Backend `destination.md`.
- Backend `story.md`.
- Frontend `story.md`.
- Backend `marketing.md` where established.

Future or campaign-specific:

- `ai-seo.md` when AI SEO documentation is approved for the app.

## Tests

Backend:

- Focused service/API tests for business rules.
- Ownership validation tests.
- Duplicate validation tests where applicable.
- Compileall.

Frontend:

- Typecheck.
- Lint.
- Build.
- Playwright coverage for core workflow.
- Responsive evidence for certification.

## Playwright

Use the existing repository Playwright foundation. Add:

- App API helper when needed.
- Page object when workflow is complex.
- Fixtures/support helpers.
- Specs for overview, CRUD, validation, ownership, filters/pagination, and responsive behavior.

## Catalog And Registries

Update only when approved by the task:

- Apps table/catalog metadata.
- Overview metadata.
- Route registry.
- Database registry.
- Documentation registry.
- Certification status/history.
- Readiness/capability docs.

## Initial Status

New apps start as `comingSoon` with `version: null` unless explicitly approved for live promotion.
