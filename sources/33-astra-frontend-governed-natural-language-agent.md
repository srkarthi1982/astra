# Astra Frontend Governed Natural-Language Agent

Document Status: Implemented / Pending Astra Review.

Created: 2026-08-08.

Canonical frontend task: `srkarthi1982/ansiversa#4`.

Certified backend target:
`4f09bf3cfdf01decb4be1feca2dc79887da6e531`.

Certified backend review: `4886585552`.

Certified frontend prerequisite head:
`d6dc2b59a1dace03096d4359ededfbd1f082e9c5`.

Frontend branch: `feature/astra-fe-agent-001`.

Frontend implementation commit:
`eceab9c26516ff859c86899a23bd79a553304e2b`.

Frontend PR #5: open, draft, unmerged, targeting
`feature/astra-governed-subscription-chat`.

Production authorization: NOT APPROVED.

## Implemented Boundary

The existing shared `AvAiAssistant` panel and Subscription Manager mode are
reused. No second assistant UI or mini-app-owned orchestration was created.

Agent mode requires both default-off frontend gates in a recognized product
environment:

```text
VITE_ASTRA_GOVERNED_CHAT_ENABLED=true
VITE_ASTRA_AI_INTENT_ENABLED=true
VITE_APP_ENV=local|development|qa|staging
```

Missing/false gates, `test`, and production fail closed. An explicit
`VITE_APP_ENV` preserves QA/staging support in optimized builds. No production
environment configuration was changed.

When eligible, all Subscription Manager question text uses only:

```text
POST /api/v1/astra/agent/query
credentials: include
```

The public camelCase request contains only:

```text
question
conversationId     optional, server-issued only
```

The browser sends no app or capability ID, parameters, declared intent,
identity/owner, role/permission/authority, grant/activation,
Runtime/Governance material, provider/model selection, DB, SQL, or tool field.
Suggestions and the 1..366 renewal-days convenience create normal question text
only and establish no authority.

## No-Fallback Compatibility

The new agent gate is a pre-request feature-selection boundary. When disabled,
the certified exact governed chat remains available exactly as the prior
feature. When enabled, agent questions are not exact-match gated and failures
never fall back to:

```text
/api/v1/astra/chat
/api/v1/assistant/query
```

Platform assistant mode remains on its existing `/api/v1/assistant/query`
behavior and is not routed through the Subscription Manager agent.

## Response And Rendering

The frontend strictly validates the certified camelCase response fields,
recognized statuses, bounded strings, conversation ID shape, structured-result
object boundary, bounded reason-code shape, and exact:

```text
productionAuthorizationState = not_approved
```

It distinguishes success, clarification, unsupported, provider unavailable,
invalid provider response, stale/invalid conversation, governed denial,
unauthenticated, network, non-2xx unavailable, and malformed/invalid response.
Successful structured records reuse the certified allowlisted formatter and a
50-record cap. Raw JSON, reason arrays, capability authority, grants,
Runtime/Governance details, provider/model names, SQL, tokens, and raw provider
payloads are not rendered. Returned `capabilityId` is evidence metadata only
and never client authority.

## Conversation And Principal Isolation

The backend-issued conversation ID remains only in volatile mounted-component
memory. The frontend never invents or persists a conversation ID. It is cleared
on reset, stale/invalid conversation, governed denial, authenticated principal
change, and logout. A returned ID is reused only for a later agent turn by the
same current principal.

The shared reset path was narrowly corrected so the reset button's immediate
clear is not repeated by the asynchronous store-reset listener. This preserves
both agent and platform route context while preventing a post-reset answer from
being erased.

## Validation Evidence

Repository validation:

```text
npm run lint        passed
npm run typecheck   passed
npm run build       passed
git diff --check    passed
```

Deterministic browser evidence across desktop Chromium and mobile Chromium:

```text
ASTRA-FE-AGENT-001 focused suite      18 passed
certified exact-chat regression       14 passed
platform-assistant regression         24 passed, 2 established skips
```

The focused suite proves materially different natural-language questions,
exact suggestions, question-only renewal convenience, sealed request fields,
credentials, every certified status, 401/network/non-2xx/malformed/invalid
authorization-state handling, bounded structured rendering, zero fallback,
reset/stale/principal/logout isolation, and unchanged platform-mode transport.

Normal frontend certification is deterministic and uses mocked agent
responses. No real OpenAI call, credential, raw prompt, provider payload,
cookie, token, user record, or secret is stored in this source record.

## Review Gate

This record describes implementation evidence. It does not certify the
frontend and authorizes no merge, deployment, production configuration,
production use, or MCP work.

```text
ASTRA-FE-AGENT-001 — Implemented / Pending Astra Review
Merge — NOT AUTHORIZED
Production — NOT APPROVED
```
