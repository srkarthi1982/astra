# Ansiversa Governance

## Source Of Truth Hierarchy

1. Partner approval.
2. Astra architecture and standards validation.
3. Root `AGENTS.md` platform contract.
4. Approved `destination.md` files for mature app direction and Journey Progress.
5. `story.md` files for current implementation memory.
6. Code, migrations, tests, and generated API contracts.
7. This Astra source pack as a structured operational index.

## App Naming Rules

Use canonical app names and slugs from `05-ansiversa-catalog.json`. Routes follow `/<app-slug>`. Do not use subdomain-based mini-app architecture for new solution apps.

## Development Lifecycle

Requirements -> Codex Development -> Astra Code Review -> Fix Issues -> Database Migration -> Push -> Manual Browser Verification -> Partner Approval.

Developed does not mean approved.

## Documentation Lifecycle

New mini apps require backend `market-study.md`, backend and frontend `story.md`, backend `destination.md`, and app marketing documentation where established. Documentation must describe the current product state, not historical diary entries.

## Promotion Rules

Coming-soon apps can be workflow-ready without live promotion. Live promotion requires Astra review, Partner approval, production migration verification, Apps table update, destination metadata sync, overview sync, and readiness/catalog updates.

## Version Rules

Live promoted apps use explicit versions such as `1.0.0`. Coming-soon workflow-ready apps keep `version` as `null` unless separately approved.

## ComingSoon Versus Live

`comingSoon` means not promoted and not approved for production user availability, even when workflow-ready. `live` means approved and promoted through the production process.

## Destination Approval Requirements

Journey Progress values come only from approved `destination.md` files. Do not infer, estimate, or recalculate destination metadata from implementation size.

## Production Migration Requirements

Each persistent mini app table requires index review based on actual query patterns. Production migration must be verified before live promotion and documented separately from local migration success.

## Manual Approval Rules

Codex may build, test, migrate, and push. Codex is not the approver. Final approval belongs to Partner after Astra review and manual browser verification.

## Shared Component Requirements

Shared resources are discovered through repetition. Follow the Rule of 4: one occurrence stays local, two to three are observed, four is a candidate, five should move shared when it reduces real duplication.

## Refuse To Store What You Do Not Own

Do not store secrets, external private data, production user lists, cookies, JWTs, API keys, database URLs, payment secrets, or personal user data in source packs, docs, logs, or test artifacts.

## Expansion Limit

No unapproved expansion beyond 100 solution apps. After all 100 exist, a new app idea must answer which existing app it replaces.

## Replacement-App Process

Replacement requires explicit Partner/Astra approval, evidence that the existing app no longer earns its place, and a migration/retirement plan for catalog, routes, data, docs, and user communication.
