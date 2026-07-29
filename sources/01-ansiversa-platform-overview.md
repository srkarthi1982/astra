# Ansiversa Platform Overview

## Vision

Ansiversa is one platform, not a collection of disconnected websites. Users should experience one login, one navigation system, one shell, one ecosystem, and one consistent product language across the parent platform and all solution apps.

## Brand Meaning

Ansiversa is the parent product and ecosystem identity. The platform exists to provide focused everyday software solutions inside a single authenticated workspace.

## Platform Rule

Ansiversa is permanently limited to 101 total products: 1 parent platform plus 100 solution apps. There is no App #101 by default. After 100 solution apps, work shifts to maturity, retention, quality, performance, replacements, and usability improvements.

## Technology Stack

Frontend: React, TypeScript, React Router, Zustand, Tailwind CSS.

Backend: FastAPI, SQLAlchemy, Alembic, PostgreSQL.

Infrastructure: Vercel, GitHub, GitHub Packages.

## Repository Model

Current working repositories:

- `ansiversa`: React parent shell and mini-app frontend modules.
- `ansiversa-api`: FastAPI parent backend and mini-app backend modules.

The platform contract also supports package-level repositories such as `ansiversa-react-shell`, `ansiversa-react-components`, `ansiversa-auth`, and one package per mini app.

## Hosting And Domains

Production domain: `ansiversa.com`.

Development domain: `qa.ansiversa.com`.

All development happens on QA first. Production remains untouched until approved.

## Authentication Model

The shell owns authentication and user context. Mini apps consume authenticated user context and must not own login, global routing, global layout, or global navigation.

## Database Strategy

The parent platform and many mini apps use isolated Alembic migration areas and per-app database environment variable names. This pack stores only variable names, never URL values.

## Shared Metadata Strategy

The Apps table and overview catalog provide canonical public app metadata. Destination metadata is governed by approved `destination.md` files and must not be guessed from code size or feature count.

## Deployment Architecture

Frontend deployment is hosted through Vercel. Backend deployment uses FastAPI services with PostgreSQL databases and Alembic migrations. Production migration and live promotion are separate approval gates.

## Payment Roadmap

Payment gateway work is planned after the certification and manual acceptance campaign. Until approved, pricing gates remain metadata and UX scaffolding, not a production billing commitment.

## AI-Agent Roadmap

AI agents are planned after certification and manual acceptance foundations. AI implementation must follow approved architecture and may not be added opportunistically inside mini apps.

## AI SEO Roadmap

AI SEO documentation precedes implementation. AI SEO coverage should be tracked per app through documentation registry fields and implemented only after approval.

## Marketing Roadmap

Marketing work follows product readiness. Confirmed direction includes 101-product storytelling, app-level marketing pages or docs, and video support after product quality gates are complete.
