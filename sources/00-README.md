# Astra Sources

This folder is Astra's canonical source pack for Ansiversa platform review, planning, and Codex task creation.

Generated or refreshed: 2026-07-18

## Files

- `01-ansiversa-platform-overview.md`: concise architecture and product overview.
- `02-ansiversa-governance.md`: frozen operating rules and promotion gates.
- `03-ansiversa-known-decisions.md`: permanent architectural and product decisions.
- `04-glossary.md`: short definitions for Ansiversa governance and delivery terms.
- `05-ansiversa-catalog.json`: canonical platform plus 100 solution app index.
- `06-ansiversa-route-registry.json`: parent and mini-app route map.
- `07-ansiversa-database-registry.json`: per-app database and migration registry.
- `08-ansiversa-documentation-registry.json`: app documentation coverage index.
- `09-ansiversa-certification-status.json`: E2E/manual acceptance campaign tracker.
- `10-certification-history.json`: compact campaign history with known certified products and commits.
- `11-ansiversa-shared-resources.md`: reusable frontend/backend resource catalog.
- `12-ui-contracts.md`: frontend component, layout, CRUD, drawer, feedback, and responsive contracts.
- `13-backend-contracts.md`: backend module, API, validation, ownership, archive, pagination, and migration contracts.
- `14-coding-standards.md`: implementation standards for scoped, typed, pattern-aligned changes.
- `15-certification-checklist.md`: repeatable certification playbook for app review and E2E validation.
- `16-promotion-checklist.md`: approved live-promotion workflow, separate from certification.
- `17-ansiversa-quality-process.md`: official validation and release flow.
- `18-ansiversa-business-rules.md`: cross-app business-rule memory.
- `19-ansiversa-roadmap.md`: confirmed roadmap decisions only.
- `20-app-template.md`: canonical blueprint for new mini-app structure and required assets.
- `21-ansiversa-repositories.md`: primary GitHub repository memory and repository ownership boundaries.
- `22-current-repository-checkpoint.md`: recovery checkpoint for repository facts newer than the original source pack, including the certified Astra backend/API/UI stack and current catalog delta.

## Exclusions

This pack must never contain passwords, API keys, database URLs, JWTs, cookies, production user lists, personal user data, Stripe secrets, or private test artifacts. Use safe variable names only.

## Update Rule

Refresh these files after app promotion, certification, migration changes, route changes, documentation lifecycle changes, or governance decisions.
