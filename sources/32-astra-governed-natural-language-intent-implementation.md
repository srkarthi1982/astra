# Astra Governed Natural-Language Intent Implementation

Document Status: Implemented / Pending Astra Review.

Created: 2026-08-07.

Canonical implementation task: `srkarthi1982/ansiversa-api#8`.

Certified architecture commit:
`cc65502990e69c39bc542933d6d8d28aac5b0291`.

Astra architecture review: `4881828844`.

Exact implementation base:
`00102d6669ff9021e7301f689d74090d760a2a03`.

Implementation branch: `feature/astra-ai-intent-001`.

Implementation commit:
`e51943e932ffe3b1b71b3ecbbdcadb3c1616b57b`.

Backend PR #9: open, draft, unmerged, targeting
`feature/astra-ai-intent-arch-001`.

Frontend agent integration: NOT AUTHORIZED.

Production authorization: NOT APPROVED.

## Implemented Surface

Backend commit `e51943e932ffe3b1b71b3ecbbdcadb3c1616b57b` changes exactly:

```text
.env.example
AGENTS.md
app/core/config.py
app/main.py
app/modules/astra_ai/api/agent.py
app/modules/astra_ai/intent_provider.py
app/modules/astra_ai/natural_language_intent.py
docs/iterations/2026-08-astra-ai-intent/tasks/astra-ai-intent-001-implementation.md
tests/test_astra_natural_language_intent.py
```

No certified Runtime, metadata binding, Read Authority, Read Access
Authorization, Read Execution, chat, authentication, or Subscription Manager
capability/adapter implementation changed.

## Runtime Boundary

The new authenticated endpoint is:

```text
POST /api/v1/astra/agent/query
```

Its public request accepts only:

```text
question
conversationId                 optional
clientRequestReference         optional
```

Extra client fields fail validation. The client cannot provide app,
capability, parameters, identity, owner, provider/model, grant, activation,
authority, Governance, Runtime, DB, SQL, tool, or resolved-intent data.

Ten exact canonical questions use a provider-independent server mapping. Every
mapped result is still validated against a fresh metadata projection and then
rechecked against the current app-owned Subscription Manager
`capability_catalog()` before chat construction. Unmatched language may invoke
the intent provider, but unsupported or unavailable input never guesses.

## Provider And Privacy Boundary

`AstraIntentProvider` is a narrow intent-only protocol.
`OpenAIIntentProvider` uses the current OpenAI Responses API structured-output
contract through strict `text.format` JSON Schema. It performs one bounded HTTP
attempt with zero retries, bounded timeout/output/body sizes, `store=false`, and
no tools or function definitions.

Provider input is limited to:

- current question;
- allowed interpretation statuses; and
- enabled capability metadata: app identity, capability ID/version, short
  purpose, and parameter name/type/required state/bounds/eligibility.

No subscription record, billing value, user/owner identity, auth token,
authorization/grant, Runtime/Governance object, evidence authority, DB/session,
SQL, secret, write/action, or final answer is provided. Raw prompt and provider
request/response bodies are not persisted.

## Candidate And Deterministic Validation

The untrusted candidate contains exactly:

```text
interpretation_status
app_id
capability_id
parameters
clarification_reason
```

Allowed statuses are `resolved`, `clarification_required`, and `unsupported`.
Pydantic forbids extra fields at every level. Non-resolved candidates cannot
carry executable data. Resolved candidates require exact
`app_id=subscription_manager`, one enabled current capability, and its exact
declared parameter contract. Nine capabilities accept no parameters.
`subscription.renewing_within_days` accepts exactly one true integer `days`
from 1 through 366; bool, float, numeric string, missing, duplicate, extra, and
out-of-range values fail closed.

Only a validated candidate becomes a server-owned `AstraChatDeclaredIntent`
inside the unchanged certified `AstraChatRequest`. The existing certified
`AstraChatGateway` is invoked in-process and remains the sole orchestration
entry into the certified authority, authorization, execution, and app-owned DB
chain. The provider never receives or rewrites the deterministic DB result.

## Configuration And Environment Gate

```text
ASTRA_AI_INTENT_ENABLED=false
ASTRA_AI_INTENT_MODEL=gpt-4.1-mini
ASTRA_AI_INTENT_TIMEOUT_SECONDS=8
ASTRA_AI_INTENT_MAX_OUTPUT_TOKENS=256
```

All settings and credentials are server-owned. The provider also respects the
existing platform AI master gate. The route registers only in `local`,
`development`, `qa`, and `staging`. `test` and production are absent/fail
closed. Exact supported questions remain provider-independent when the provider
is disabled or unavailable, while the endpoint remains default-off.

## Validation And Provenance

Focused intent/provider/agent validation:

```text
91 passed
1 skipped — real OpenAI smoke not run; credential gated
```

Full Astra regression validation:

```text
541 passed
33 subtests passed
1 skipped — same credential-gated real-provider smoke
```

Compileall passed. `git diff --check` passed. The worktree was clean after the
implementation commit.

Authenticated HTTP database provenance used a deterministic fake intent
provider with the materially different natural-language question
`How many services have I subscribed to?`. The fresh candidate resolved to
`subscription.count_all`, passed deterministic catalog validation, and entered
the unchanged certified chain. The primary authenticated owner's DB-backed
count was 2, became 3 after a committed owner-scoped Subscription Manager row,
and the second authenticated user saw only their own count of 1.

Security coverage includes exact-path provider independence, multiple
paraphrases for every certified read, strict day values, fresh catalog drift,
hallucinated/foreign capabilities, extra identity/role/grant/activation/
Runtime/Governance/SQL/DB/tool/confidence/explanation fields, multiple/malformed/
empty/oversized provider output, timeout/unavailability with zero retries,
prompt injection, write requests, auth negatives, blocked users, feature and
environment gates, foreign conversations, and client authority-shaped fields.

## Review Gate

This source record describes implementation evidence only. It does not certify
the implementation and does not authorize frontend work, merge, deployment,
production configuration, or production use.

```text
ASTRA-AI-INTENT-001 — Implemented / Pending Astra Review
Frontend agent integration — NOT AUTHORIZED
Production — NOT APPROVED
```
