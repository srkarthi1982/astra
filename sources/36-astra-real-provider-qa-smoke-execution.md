# Astra Real-Provider QA Smoke Execution

Document Status: Authorized / Pending Controlled Execution.

Created: 2026-08-08.

Canonical execution task: `srkarthi1982/ansiversa#9`.

QA preparation prerequisite:
`3ffd8c6cf07287d516de06989b601dc8f6e9f8a5`.

QA preparation Astra review:
`4889413022`.

Certified frontend executable:
`eceab9c26516ff859c86899a23bd79a553304e2b`.

Certified backend executable:
`4f09bf3cfdf01decb4be1feca2dc79887da6e531`.

Production authorization: NOT APPROVED.

## Authorized Objective

Issue #9 authorizes only a controlled non-production Mac/browser execution of the prepared real-provider Subscription Manager Astra AI smoke.

The intended live chain is:

```text
authenticated browser
  -> Astra AI Subscription Manager mode
  -> natural-language question
  -> POST /api/v1/astra/agent/query
  -> configured real intent provider
  -> deterministic candidate validation
  -> certified Astra governance/read chain
  -> owner-scoped Subscription Manager database
  -> bounded browser response
```

The execution must preserve the certified browser authority boundary, zero request-time fallback, volatile server-issued conversation handling, owner isolation, and metadata-only evidence rules.

## Execution Boundary

Allowed targets are explicit non-production `local`, `development`, `qa`, or `staging` environments and approved hostnames only (`qa.ansiversa.com`, `localhost`, `127.0.0.1`). Production `ansiversa.com` is prohibited.

Frontend gates required:

```text
VITE_ASTRA_GOVERNED_CHAT_ENABLED=true
VITE_ASTRA_AI_INTENT_ENABLED=true
```

Backend intent/provider prerequisites must be enabled only in the approved non-production environment. Provider credentials remain environment-only and must never appear in GitHub, Astra sources, chat, screenshots, traces uploaded for review, or committed files.

## Required Proof

The controlled smoke must prove at minimum:

1. natural-language Subscription Manager paraphrases use only `POST /api/v1/astra/agent/query`;
2. request keys are only `question` plus optional server-issued `conversationId`;
3. zero request-time calls to `/api/v1/astra/chat` and `/api/v1/assistant/query`;
4. bounded non-empty successful rendering;
5. continuation reuses only the server-issued conversation ID;
6. reset causes the next request to omit the prior conversation ID;
7. clarification/unsupported state is bounded and safe;
8. second-owner stage proves no inherited conversation or first-owner data if an approved second owner is available.

Evidence is metadata-only. Never persist secrets, cookies, auth-state content, DB URLs, user/account IDs, subscription names/amounts, raw questions/answers, provider payloads, private prompts, SQL, or database internals.

If any code/configuration repair is required during the smoke, stop and create a separate correction task rather than modifying runtime under this execution issue.

## Current Gate

```text
ASTRA-FE-AGENT-QA-PREP-001 — APPROVED / CERTIFIED / CLOSED
ASTRA-FE-AGENT-QA-SMOKE-001 — AUTHORIZED / PENDING CONTROLLED EXECUTION
Issue #9 — OPEN
Real-provider smoke — NOT YET EXECUTED
Merge — NOT AUTHORIZED
MCP work — NOT STARTED
Production — NOT APPROVED
```
