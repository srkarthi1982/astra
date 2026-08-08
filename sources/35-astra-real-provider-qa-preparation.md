# Astra Real-Provider QA Preparation

Document Status: Changes Required / Pending Astra Re-Review.

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

## Current Gate

Astra converted PR #7 back to draft. It remains open and unmerged.

Codex must correct the lineage and smoke target, rerun required validation, synchronize Astra evidence as Prepared / Pending Astra Re-Review, post the corrected completion report to Issue #6, and stop for Astra live re-review.

```text
ASTRA-FE-AGENT-QA-PREP-001 — CHANGES REQUIRED / NOT CERTIFIED
PR #7 — OPEN / DRAFT / UNMERGED
Real-provider smoke execution — NOT AUTHORIZED / NOT EXECUTED
Merge — NOT AUTHORIZED
MCP work — NOT STARTED
Production — NOT APPROVED
```
