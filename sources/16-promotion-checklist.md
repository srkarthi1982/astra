# Promotion Checklist

This checklist is for live promotion. It is separate from certification.

## Promotion Boundary

Live promotion requires Astra review and Partner approval. Codex may execute the steps after approval but does not approve the app.

## Pre-Approval Requirements

- App is workflow-ready.
- Certification has passed or approved exceptions are documented.
- Astra code review is complete.
- Partner manual browser acceptance is complete.
- `destination.md` is approved and contains current Journey Progress metadata.
- Known critical defects are fixed.

## Version Rule

Coming-soon apps keep `version` as `null`. Live promoted apps receive an approved version, usually `1.0.0` for first live release.

## Apps Row Update

Update the parent Apps table with approved values:

- `launchStatus = live`.
- `version`.
- `destination_progress`.
- `destination_status`.
- `destination_reviewed_at`.

Destination metadata must come only from approved `destination.md`.

## Production Migration

- Run the production-configured isolated migration for the app.
- Verify Alembic head.
- Verify expected tables exist.
- Verify required indexes exist.
- Verify starting row count or existing data expectations.
- Do not run unrelated app migrations unless approved.

## Metadata Sync

- Sync Apps API response.
- Sync `apps.json` or catalog export.
- Sync readiness/capability documentation.
- Sync Astra source pack registries when promotion changes source-of-truth metadata.

## Overview Sync

- Verify overview metadata.
- Verify `Explore` CTA label and route.
- Verify app visibility and pricing gate.
- Verify public catalog count.

## Catalog Counts

After promotion, verify live and coming-soon counts. The total solution app count must remain 100.

## Commit And Push

- Review diff.
- Commit intentional promotion changes.
- Push to the correct branch.
- Do not include secrets or private production artifacts.

## Production Verification

- Verify production overview route.
- Verify protected workflow route.
- Verify Apps API/catalog response.
- Verify no production console/network blockers in the promoted workflow.
- Verify destination metadata is visible through approved API/documentation surfaces when applicable.

## Final Promotion Report

Report approval source, version, migration head, Apps row values, destination metadata, catalog counts, commits, production verification result, and remaining known limitations.
