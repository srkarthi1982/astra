# Astra Real-Provider QA Preparation

Document Status: QA Smoke Prepared / Pending Astra Re-Review.

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

Corrected frontend commit:
`3ffd8c6cf07287d516de06989b601dc8f6e9f8a5`.

Corrected draft stacked PR: `srkarthi1982/ansiversa#8`, targeting
`feature/astra-fe-agent-001`.

Production authorization: NOT APPROVED.

## Authorized Objective

Issue #6 authorizes preparation only for a later Partner-controlled non-production Mac/browser real-provider smoke of the certified Subscription Manager Astra natural-language flow. Codex Cloud must not execute a real OpenAI call, persist credentials, merge, deploy, modify production, or start MCP work.

The later smoke must prove:

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

PR #7 was created against `main` at `4681a23cc08240db8595941a2fee80989ad24825` instead of the required certified frontend branch. GitHub comparison against `feature/astra-fe-agent-001` showed:

```text
status      diverged
ahead_by    1
behind_by   4
merge base  4681a23cc08240db8595941a2fee80989ad24825
required base eceab9c26516ff859c86899a23bd79a553304e2b
```

Changing PR metadata alone is not sufficient. The QA-preparation changes must be recreated or rebased onto the exact certified frontend head before review can pass.

### Wrong smoke target

The initial harness observes `/api/v1/assistant/query` and uses platform-assistant prompts such as app discovery and provider/model disclosure, with `openai_grounded` / `deterministic` response-mode assertions.

That is a different product flow from Issue #6. The prepared smoke must instead exercise the Subscription Manager agent boundary `/api/v1/astra/agent/query` through the existing Subscription Manager mode.

The corrected preparation must prove at minimum:

1. a materially natural-language Subscription Manager question reaches `/api/v1/astra/agent/query`;
2. browser request keys are only `question` plus optional server-issued `conversationId`;
3. zero request-time fallback to `/api/v1/astra/chat` and `/api/v1/assistant/query`;
4. bounded successful Subscription Manager rendering;
5. reset causes the next request to omit the prior conversation ID;
6. the runbook contains a controlled later second-owner isolation stage without embedding credentials.

## Corrected Preparation Evidence

Astra converted PR #7 back to draft. It remains open, unmerged historical
wrong-base evidence and was not modified by the correction.

The corrected branch starts exactly from certified frontend executable
`eceab9c26516ff859c86899a23bd79a553304e2b`. Its six-file preparation scope adds
an operator runbook, explicit opt-in Playwright harness, QA target/test command,
test documentation, and the required frontend task record. No product runtime
source changed.

The harness opens the existing Astra panel, selects Subscription Manager, and
observes the real `POST /api/v1/astra/agent/query` response without interception
or mocking. It checks only `question` plus optional server-issued
`conversationId`, bounded successful rendering, server-issued continuation,
reset omission, and zero calls to `/api/v1/astra/chat` or
`/api/v1/assistant/query`. It is disabled by default, accepts only local/QA
targets and approved hostnames, refuses production in preflight, requires a
local gitignored authenticated storage-state file, and attaches metadata only.
The runbook keeps second-owner isolation as a separate controlled stage and
records no credentials or user data.

Validation passed:

```text
npm run lint                                      passed
npm run typecheck                                 passed
npm run build                                     passed
focused agent Chromium regression                  9 passed
certified exact-chat Chromium regression            7 passed
smoke list/default invocation                      1 listed / 1 skipped
enabled production-target invocation               refused in preflight
git diff --check                                  passed
```

The real-provider smoke was not executed. The corrected preparation is ready
only for Astra live re-review.

```text
ASTRA-FE-AGENT-QA-PREP-001 — QA SMOKE PREPARED / PENDING ASTRA RE-REVIEW
PR #8 — OPEN / DRAFT / UNMERGED / STACKED ON CERTIFIED FRONTEND
PR #7 — HISTORICAL WRONG-BASE REFERENCE / OPEN / DRAFT / UNMERGED
Real-provider smoke execution — NOT YET AUTHORIZED / NOT YET EXECUTED
Merge — NOT AUTHORIZED
MCP work — NOT STARTED
Production — NOT APPROVED
```
