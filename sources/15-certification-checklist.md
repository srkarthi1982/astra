# Certification Checklist

This checklist is for certification, not live promotion.

## Scope Boundary

Certification verifies workflow readiness, automated checks, exploratory browser behavior, regression coverage, production smoke, and defect closure. It does not grant final approval or live promotion.

## Preflight

- Read root `AGENTS.md`.
- Read frontend/backend `AGENTS.md` files when touching those repositories.
- Read the assigned Astra task.
- Confirm the app number, canonical name, slug, backend module, and current `launchStatus`.
- Confirm the app remains `comingSoon` unless live promotion is explicitly requested and approved.
- Confirm credentials come only from approved local environment sources.

## Code And Documentation Review

- Review frontend module under `ansiversa/src/modules/<app-slug>`.
- Review backend module under `ansiversa-api/app/modules/<app_module>`.
- Review `story.md`, `destination.md`, `market-study.md`, and `marketing.md`.
- Review route registry and overview CTA behavior.
- Review create/edit/delete support for long-lived user-created records.
- Review list/detail API payload separation.
- Review ownership validation and update payloads.
- Review database indexes and migration head.

## Required Automated Checks

- Backend focused tests for the app when present or added.
- Backend compileall: `python -m compileall app tests`.
- Frontend typecheck.
- Frontend lint.
- Frontend build.
- Overview CTA validation.
- OpenAPI/generated client validation when backend contracts changed.
- `git diff --check` for touched repos.

## Exploratory E2E Coverage

Cover the core user journey:

- Overview route and `Explore` CTA.
- Protected workflow gating.
- Create, view, edit, delete for long-lived user records.
- Empty, loading, success, and error states.
- Duplicate validation where product rules require it.
- Archive/restore or soft-delete behavior where supported.
- Filters, search, sorting, and pagination where supported.
- Ownership isolation with a secondary account when records are user-owned.
- Responsive desktop, tablet, and mobile layouts.

## Playwright Local

- Use the existing Playwright foundation.
- Do not introduce a parallel browser test framework.
- Start local API according to the app/task instructions.
- Run app-specific Playwright specs in Chromium.
- Run app-specific Playwright specs in Chrome when available.
- Run Edge only when Microsoft Edge is installed.
- Save useful local report/evidence when requested by the task.

## Playwright Production Smoke

- Run production smoke only after the required push/deploy wait when the task requests it.
- Use production base URLs and API URLs.
- Keep smoke tests non-destructive or self-cleaning.
- Save production report/evidence when requested by the task.

## Browser Matrix

Required by default:

- Chromium.
- Chrome.
- Desktop screenshot/inspection.
- Tablet screenshot/inspection.
- Mobile screenshot/inspection.

Deferred when unavailable:

- Edge, if the browser is not installed.

## Certification Status Update

After certification, update `astra/sources/09-ansiversa-certification-status.json` and `astra/sources/10-certification-history.json` with:

- App number and slug.
- Local E2E result.
- Playwright result.
- Production smoke result.
- Bugs found/fixed.
- Frontend/backend commits when pushed.
- Certification date.
- Known environment deferrals.

## Failure Conditions

Fail certification for broken core workflow, ownership leakage, invalid CTA, missing protected route, unhandled production error, secret exposure, major responsive breakage, data loss, or unresolved critical defect.

## Final Report

Report result, changed files, checks run, browser matrix, evidence paths, commits, known deferrals, and whether the app is eligible for manual acceptance. Do not state that the app is approved unless Partner approval happened.
