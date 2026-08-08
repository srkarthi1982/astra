# Astra Real-Provider QA Preparation

Document Status: QA Preparation Approved / Certified / Closed.

Created: 2026-08-08.

Canonical frontend preparation task: `srkarthi1982/ansiversa#6`.

Frontend certified prerequisite:
`eceab9c26516ff859c86899a23bd79a553304e2b` on `feature/astra-fe-agent-001`.

Frontend certification review: `4888398174`.

Initial Codex Cloud PR: `srkarthi1982/ansiversa#7`.

Initial PR head reviewed:
`1ec2109ff22b4ebcc4f6f2517b35846027e77c43`.

Astra initial QA-preparation review: `4888630816`.

Issue #6 correction gate: `5225687507`.

Branch-recovery comment: `5225710139`.

Corrected frontend branch: `feature/astra-fe-agent-qa-prep-001`.

Certified frontend preparation target:
`3ffd8c6cf07287d516de06989b601dc8f6e9f8a5`.

Corrected draft stacked PR: `srkarthi1982/ansiversa#8`, targeting
`feature/astra-fe-agent-001`.

Astra preparation certification review: `4889413022`.

Issue #6 certification closure comment: `5227501139`.

Production authorization: NOT APPROVED.

## Authorized Objective

Issue #6 authorized preparation only for a later Partner-controlled non-production Mac/browser real-provider smoke of the certified Subscription Manager Astra natural-language flow. The preparation task itself authorized no real OpenAI/provider execution, credential persistence, merge, deployment, production change, backend semantic change, or MCP work.

The later controlled smoke is intended to prove:

```text
authenticated browser
  -> Astra AI Subscription Manager mode
  -> natural-language question
  -> POST /api/v1/astra/agent/query
  -> configured real intent provider
  -> deterministic candidate validation
  -> certified governance/read chain
  -> owner-scoped Subscription Manager DB
  -> bounded browser response
```

## Initial Review Findings

Astra independently reviewed PR #7 after the Codex Cloud workspace was manually published to GitHub.

### Wrong certified lineage

PR #7 was created against `main` at `4681a23cc08240db8595941a2fee80989ad24825` instead of the required certified frontend branch. GitHub comparison against `feature/astra-fe-agent-001` showed the branch was one commit ahead and four commits behind the certified frontend, with merge base still at the old main baseline.

Changing PR metadata alone was not sufficient. The QA-preparation changes had to be recreated on the exact certified frontend head.

### Wrong smoke target

The initial harness observed `/api/v1/assistant/query` and used platform-assistant prompts and response-mode assertions. That was a different product flow from Issue #6.

The corrected preparation therefore had to exercise the Subscription Manager agent boundary `/api/v1/astra/agent/query` through the existing Subscription Manager mode and prove sealed request keys, zero fallback, bounded rendering, conversation reset, and a later second-owner isolation stage.

## Corrected Preparation Evidence

PR #7 remains open, draft, unmerged historical wrong-base evidence and is not a certification target.

The corrected branch starts exactly from certified frontend executable
`eceab9c26516ff859c86899a23bd79a553304e2b`. GitHub comparison shows certified preparation target
`3ffd8c6cf07287d516de06989b601dc8f6e9f8a5` is exactly one commit ahead and zero commits behind the certified base.

The six-file preparation scope adds only:

- frontend task record;
- operator runbook;
- explicit opt-in Playwright smoke harness;
- QA target/test command configuration; and
- test documentation.

No frontend product-runtime source changed.

The harness opens the existing Astra panel, selects Subscription Manager, and observes the real `POST /api/v1/astra/agent/query` response without intercepting or mocking that response. It validates:

- request keys are only `question` plus optional server-issued `conversationId`;
- bounded successful rendering;
- server-issued conversation continuation;
- reset omission of the prior conversation ID;
- zero calls to `/api/v1/astra/chat`; and
- zero calls to `/api/v1/assistant/query`.

The harness is disabled by default, accepts only approved local/QA targets and hostnames, refuses production during preflight, requires a local authenticated storage-state file under the Git-ignored `.auth/` path, and attaches metadata only. The runbook keeps second-owner isolation as a separate controlled stage and prohibits persistence of credentials, cookies, user data, prompts, answers, DB URLs, or raw provider payloads.

Validation reported at the certified preparation target:

```text
npm run lint                                      passed
npm run typecheck                                 passed
npm run build                                     passed
focused agent Chromium regression                  9 passed
certified exact-chat Chromium regression            7 passed
smoke list/default invocation                      1 listed / 1 skipped
enabled production-target invocation               refused in preflight
git diff --check                                  passed
Vercel non-production status                       success
```

## Astra Certification Decision

Astra independently re-reviewed live PR #8, exact base/head lineage, changed scope, smoke implementation, runbook, Git-ignore boundary, Issue #6 evidence, Vercel status, and Astra source synchronization.

No remaining blocker was found for the **QA-smoke preparation** scope. Astra therefore certified the preparation at exact target:

`3ffd8c6cf07287d516de06989b601dc8f6e9f8a5`

through review:

`4889413022`.

Issue #6 was closed completed after certification. PR #8 remains open, draft, mergeable, and unmerged. Certification of preparation does not certify the real-provider execution result and authorizes no merge, deployment, production configuration, production use, backend/database change, MCP work, or secret-handling change.

The real-provider/browser smoke remains a separate controlled execution gate.

## Final State

```text
ASTRA-FE-AGENT-QA-PREP-001 — QA PREPARATION APPROVED / CERTIFIED / CLOSED
Certified preparation target — 3ffd8c6cf07287d516de06989b601dc8f6e9f8a5
Astra preparation certification review — 4889413022
Issue #6 — CLOSED / COMPLETED
PR #8 — OPEN / DRAFT / UNMERGED / STACKED ON CERTIFIED FRONTEND
PR #7 — HISTORICAL WRONG-BASE REFERENCE / OPEN / DRAFT / UNMERGED
Real-provider browser smoke — SEPARATE CONTROLLED EXECUTION GATE / NOT YET EXECUTED
Merge — NOT AUTHORIZED
MCP work — NOT STARTED
Production — NOT APPROVED
```
