# Astra Frontend Governed Natural-Language Agent Certification

Document Status: Certified / Approved / Closed.

Created: 2026-08-08.

Canonical frontend task: `srkarthi1982/ansiversa#4`.

Astra certification review: `4888398174`.

Certified frontend executable:
`eceab9c26516ff859c86899a23bd79a553304e2b`.

Certified frontend prerequisite head:
`d6dc2b59a1dace03096d4359ededfbd1f082e9c5`.

Certified backend executable consumed unchanged:
`4f09bf3cfdf01decb4be1feca2dc79887da6e531`.

Certified backend review: `4886585552`.

Frontend PR #5 remains open, draft, mergeable, and unmerged against
`feature/astra-governed-subscription-chat`.

Production authorization: NOT APPROVED.

## Certification Decision

Astra independently reviewed the live GitHub implementation, branch/base,
changed files, request and response contracts, browser authority boundary,
conversation isolation, regression coverage, PR state, Vercel status, and Astra
source synchronization.

No architecture, authority, privacy, fallback, conversation-isolation, or
frontend-contract blocker remained. `ASTRA-FE-AGENT-001` is therefore
Certified / Approved at exact executable
`eceab9c26516ff859c86899a23bd79a553304e2b`.

The executable certification target remains the implementation commit above.
Any later documentation-only closure commit is not a new executable target.

## Certified Browser Boundary

When both non-production frontend gates are eligible, Subscription Manager
natural-language questions use only:

```text
POST /api/v1/astra/agent/query
credentials: include
```

The browser request contains only:

```text
question
conversationId     optional, server-issued only
```

The browser does not provide app identity, capability identity, parameters,
declared intent, user/owner identity, role, permission, authority, grant,
activation, Runtime/Governance material, provider/model selection, DB, SQL, or
tool fields.

The browser remains non-authoritative. Returned `capabilityId` is bounded
response/evidence metadata only and is never converted into client-side
execution authority.

## Feature And Environment Gates

Agent mode requires both:

```text
VITE_ASTRA_GOVERNED_CHAT_ENABLED=true
VITE_ASTRA_AI_INTENT_ENABLED=true
```

and a recognized product environment:

```text
local
development
qa
staging
```

Missing/false gates, `test`, and production fail closed. Explicit
`VITE_APP_ENV` preserves QA/staging support in optimized builds. No production
configuration was changed.

When the agent gate is disabled, the previously certified exact governed-chat
frontend remains selected as a pre-request compatibility path. Once an agent
request is selected, failure never falls back to `/api/v1/astra/chat` or
`/api/v1/assistant/query`.

## Response And Rendering Boundary

The frontend validates the certified camelCase response contract, recognized
agent statuses, bounded strings, conversation identifier shape, structured
result object boundary, bounded reason-code shape, and exact:

```text
productionAuthorizationState = not_approved
```

User-facing rendering distinguishes success, clarification required,
unsupported request, provider unavailable, invalid provider response,
stale/invalid conversation, governed denial, authentication failure, network
failure, non-2xx unavailable response, and malformed/invalid response.

Rendering remains bounded and does not expose raw JSON, reason arrays,
provider/model internals, grants, Runtime/Governance material, SQL, tokens, or
raw provider payloads.

## Conversation And Principal Isolation

The backend-issued conversation identifier remains only in volatile component
memory. The frontend never invents or persists one. It is cleared on reset,
stale/invalid conversation, authenticated-principal change, and logout. The
implementation also clears it conservatively on governed denial. Tests prove a
second principal does not receive the first principal's conversation ID.

## Validation Evidence

Reported repository validation at the certified target:

```text
npm run lint                                      passed
npm run typecheck                                 passed
npm run build                                     passed
focused agent Playwright desktop/mobile           18 passed
certified exact-chat regression desktop/mobile    14 passed
platform-assistant regression desktop/mobile      24 passed, 2 established skips
git diff --check                                  passed
```

Astra independently inspected the focused Playwright source and confirmed it
covers materially different natural-language questions, exact suggestions,
question-only renewal convenience, sealed request keys, every certified agent
state, transport/malformed failures, zero fallback, environment gates,
reset/stale/principal/logout isolation, and unchanged platform-mode transport.

Vercel status for certified executable
`eceab9c26516ff859c86899a23bd79a553304e2b` is success. The preview is
non-production only and grants no production authority.

## Real Provider / Final Product Gate

This certification is deterministic frontend implementation certification. It
does not claim completion of the separately planned real secret-backed OpenAI
provider + controlled QA/browser smoke.

That end-to-end product proof requires a separate authorization/gate before the
Subscription Manager Astra AI flow is declared fully complete.

## Superseded Pending-Review Records

The implementation-stage pending-review statements in:

```text
sources/22-current-repository-checkpoint.md
sources/32-astra-governed-natural-language-intent-implementation.md
sources/33-astra-frontend-governed-natural-language-agent.md
```

remain historical implementation evidence. For the current certification state,
this source is authoritative and supersedes those `Implemented / Pending Astra
Review` downstream-status statements.

Permanent governance source 30 remains unchanged by this certification.

## Final State

```text
ASTRA-AI-INTENT-001 — Backend Approved / Certified / Closed
ASTRA-FE-AGENT-001 — Frontend Approved / Certified / Closed
Certified frontend executable — eceab9c26516ff859c86899a23bd79a553304e2b
Astra frontend certification review — 4888398174
Frontend PR #5 — OPEN / DRAFT / UNMERGED
Merge — NOT AUTHORIZED
Real provider QA/browser smoke — NOT YET AUTHORIZED / NOT YET COMPLETED
MCP work — NOT STARTED
Production — NOT APPROVED
```
