# Ansiversa Quality Process

## Official Release Flow

Development -> Automated validation -> Codex exploratory E2E -> Defect fixing -> Playwright regression -> Production smoke -> Karthik manual acceptance -> Live promotion.

## Automated Validation

Expected checks scale by change, but mini-app certification normally includes backend unit or service tests, backend compileall, frontend typecheck, lint, build, generated API compatibility where applicable, and Playwright regression.

## Test-Account Strategy

Use QA/test accounts only. Credentials must come from local environment files or approved secret stores. Never print credentials, cookies, JWTs, database URLs, or private user data.

## Ownership Testing

Certification should cover primary account workflows and secondary account isolation when records are user-owned. Cross-account reads, updates, and deletes must fail or return not found.

## Localhost Versus Production Gates

Localhost validation proves workflow behavior before push. Production smoke verifies deployed behavior after push. Production smoke does not equal live promotion.

## Artifact Policy

Keep useful Playwright reports and screenshots only when they support certification evidence. Do not store private test artifacts, secrets, cookies, or production user data.

## Credential Policy

Use variable names in docs and registries. Do not store actual values. Root `.env.local` may be used locally but must not be copied into source packs.

## Cleanup Policy

E2E tests should clean their own records where possible. Cleanup must respect product rules and should not bypass public API ownership constraints unless a test helper is explicitly approved.

## Console And Network Requirements

Certification should watch for visible UI errors, blocking console errors, failed network calls, auth leakage, and unexpected redirects. Known external noise should be documented, not ignored silently.

## Responsive Matrix

At minimum, certification should inspect desktop, tablet, and mobile layouts for core workflows. Text must not overlap or overflow controls.

## Accessibility Baseline

Interactive controls require accessible labels where visual text is insufficient. Icon-only record actions must include aria labels or equivalent supported labels.

## Certification Failure Conditions

Fail certification for data loss, incorrect ownership, broken create/edit/delete workflow, invalid Explore CTA, missing protected workflow, production-only breakage, secret exposure, major responsive failure, or unhandled API errors in core flows.
