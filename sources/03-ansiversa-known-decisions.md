# Ansiversa Known Decisions

## 2026-07-18 - Astra Source Pack

Decision: Maintain a small canonical source pack under `astra/sources` for Astra planning, review, and Codex task generation.

Rationale: Structured files make product state, certification state, routes, databases, documentation, and governance easier to diff and refresh.

## 2026-07-18 - Playwright Certification Baseline

Decision: Use the existing Playwright foundation for exploratory E2E and regression certification.

Rationale: A single test foundation prevents parallel framework drift and supports local plus production smoke validation.

## 2026-07-05 - Parent Plus 100 Solution Apps

Decision: Ansiversa is capped at 1 parent platform plus 100 solution apps.

Rationale: The ecosystem should maintain the best 100 everyday software solutions rather than expand indefinitely.

## 2026-07-05 - Market Study Requirement

Decision: Every new mini app requires backend `market-study.md` during initial development.

Rationale: Ansiversa should learn from public market patterns before building while keeping product commitments separate in `destination.md`.

## 2026-07-03 - Destination Metadata Governance

Decision: Destination Progress, status, and reviewed date come only from approved `destination.md` files.

Rationale: Product maturity must be governed by approved destination alignment, not implementation size or feature count.

## 2026-07-03 - Destination-First Development

Decision: New mini apps create `destination.md` during initial development.

Rationale: `story.md` explains current implementation; `destination.md` explains intended mature product direction.

## 2026-06-28 - Playwright Adoption

Decision: Browser validation should use the repository's Playwright setup.

Rationale: Repeatable browser automation is required for the certification campaign.

## 2026-06 - Per-App Database Isolation

Decision: Persistent mini apps use isolated database modules and Alembic migration areas where implemented.

Rationale: Isolation limits migration blast radius and clarifies ownership.

## 2026-06 - Shared Forms And Confirmation Contracts

Decision: Use shared form drawers, record actions, confirmation dialogs, pagination, and feedback components where established.

Rationale: Users should experience consistent mini-app CRUD behavior inside one platform.

## 2026-06 - Lazy Loading

Decision: Mini-app modules load lazily through the parent shell route registry.

Rationale: The shell remains mounted while solution apps load on demand.

## 2026-06 - One Account Across Ecosystem

Decision: The parent shell owns authentication and mini apps operate within that user context.

Rationale: Ansiversa should feel like one application, not unrelated sites.

## 2026-06 - React And FastAPI Stack

Decision: Use React, TypeScript, React Router, Zustand, Tailwind CSS, FastAPI, SQLAlchemy, Alembic, and PostgreSQL.

Rationale: This stack supports the approved shell plus mini-app architecture.

## 2026-07 - AI SEO Documentation Before Implementation

Decision: AI SEO documentation is planned before AI SEO implementation.

Rationale: Coverage and strategy should be deliberate before adding implementation surface area.
