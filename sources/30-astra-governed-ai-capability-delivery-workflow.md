# Astra Governed AI Capability Delivery Workflow

Document Status: Permanent governance source.

Created: 2026-08-07.

Owner: Karthikeyan Ramalingam, Product Owner.

Scope: All future Astra AI capability work across Ansiversa applications.

## Permanent Rule

```text
Applications own capabilities. Astra owns orchestration.
```

GitHub is the canonical task, review, certification, and audit record. Chat is
only a decision-summary and coordination surface.

## Required Workflow

1. Product Owner defines the user-visible target.
2. Astra defines architecture, security boundaries, acceptance proof, and the
   GitHub Codex task.
3. All Codex tasks are created directly in GitHub; chat is only a summary and
   orchestration surface. GitHub is the canonical task and audit record.
4. Backend capability and orchestration are implemented first.
5. Codex stops.
6. Astra independently reviews live GitHub. Codex completion reports are
   evidence, not certification.
7. Corrections repeat until the backend is certified.
8. Certification records and the Astra source pack are closed and synchronized.
9. Only then is frontend integration authorized.
10. Frontend consumes only the certified backend contract.
11. Codex stops.
12. Astra independently reviews live frontend source and PR.
13. Real browser, API, application, and database provenance is proven.
14. Owner isolation and negative paths are proven.
15. Corrections repeat until frontend is certified.
16. Certification never implies merge.
17. Certification never implies deployment.
18. Certification never implies production authorization.
19. Merge, QA promotion, deployment, and production remain separate Product
    Owner decisions.
20. Applications own capabilities. Astra owns orchestration.
21. Every durable architecture or governance change is synchronized to the
    Astra source pack.
22. PR and issue metadata must remain accurate; automatic preview deployments
    must be recorded distinctly from manual or production deployment.

## Gate Semantics

Each gate authorizes only its recorded scope. Architecture approval does not
authorize implementation. Backend certification does not authorize frontend.
Frontend certification does not authorize merge, deployment, production
configuration, or production use.

At every Codex stop point, Astra reviews the actual live branch, commits, diff,
PR metadata, issue record, evidence, and source-pack synchronization. A Codex
report cannot self-certify the work.

## Repository Memory Rule

Durable decisions must be recorded in the canonical GitHub issue/PR and
relevant Astra source files. Source memory must contain no credentials, tokens,
cookies, DB URLs, private prompts, raw provider payloads, or user data.
