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
- `23-astra-read-execution.md`: ASTRA-READ-EXEC-001 governed read execution bridge memory, current boundaries, adapter contract, validation evidence, and unresolved authorization boundaries.
- `24-astra-app-validation.md`: ASTRA-APP-VAL-001 Subscription Manager governed read execution validation memory, scenario coverage, database-session proof, and unresolved authorization boundaries.
- `25-astra-read-authority-binding.md`: certified Subscription Manager read authority and capability binding memory.
- `26-astra-runtime-activation.md`: certified governed non-production Runtime activation memory.
- `27-astra-chat-orchestration.md`: certified governed backend chat orchestration memory.
- `28-astra-metadata-activation-binding.md`: certified governed metadata activation and capability-context binding memory.
- `29-astra-frontend-governed-subscription-chat.md`: ASTRA-FE-CHAT-001 frontend implementation, review state, and isolated browser evidence.
- `30-astra-governed-ai-capability-delivery-workflow.md`: permanent GitHub-first governed Astra capability delivery workflow.
- `31-astra-governed-natural-language-intent-architecture.md`: certified governed natural-language intent architecture.
- `32-astra-governed-natural-language-intent-implementation.md`: certified backend governed intent implementation and evidence.
- `33-astra-frontend-governed-natural-language-agent.md`: frontend governed Subscription Manager agent implementation evidence.
- `34-astra-frontend-governed-natural-language-agent-certification.md`: certified frontend governed Subscription Manager agent boundary.
- `35-astra-real-provider-qa-preparation.md`: ASTRA-FE-AGENT-QA-PREP-001 review, correction, and prepared/pending-review evidence.

## Exclusions

This pack must never contain passwords, API keys, database URLs, JWTs, cookies, production user lists, personal user data, Stripe secrets, or private test artifacts. Use safe variable names only.

## Update Rule

Refresh these files after app promotion, certification, migration changes, route changes, documentation lifecycle changes, or governance decisions.
