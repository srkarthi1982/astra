# Astra Governed Natural-Language Intent Implementation

Document Status: Backend Approved / Certified / Closed.

Created: 2026-08-07.

Canonical implementation task: `srkarthi1982/ansiversa-api#8`.

Certified architecture commit:
`cc65502990e69c39bc542933d6d8d28aac5b0291`.

Astra architecture review: `4881828844`.

Astra initial implementation review: `4886169635`.

Astra certification review: `4886585552`.

Issue #8 correction gate: `5221470917`.

Exact implementation base:
`00102d6669ff9021e7301f689d74090d760a2a03`.

Implementation branch: `feature/astra-ai-intent-001`.

Initial implementation commit:
`e51943e932ffe3b1b71b3ecbbdcadb3c1616b57b`.

Certified executable target / acceptance-proof correction commit:
`4f09bf3cfdf01decb4be1feca2dc79887da6e531`.

Backend PR #9: open, draft, unmerged, targeting
`feature/astra-ai-intent-arch-001`.

Frontend agent integration: separately authorized and implemented by
`srkarthi1982/ansiversa#4`; pending Astra frontend review.

Production authorization: NOT APPROVED.

## Implemented Surface

Initial backend implementation commit `e51943e932ffe3b1b71b3ecbbdcadb3c1616b57b` changes exactly:

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

## Astra Review Correction

Astra review `4886169635` found no architecture or runtime defect. It required
four explicit acceptance-proof corrections. Correction commit
`4f09bf3cfdf01decb4be1feca2dc79887da6e531` changes only:

```text
AGENTS.md
docs/iterations/2026-08-astra-ai-intent/tasks/astra-ai-intent-001-implementation.md
tests/test_astra_natural_language_intent.py
```

The added tests prove:

1. a genuinely foreign `app_id=expense_tracker` candidate fails before
   certified chat execution;
2. `subscription.count_active`, although catalog-valid, fails before
   `AstraChatRequest` construction/chat execution when omitted from the exact
   metadata projection supplied and validated for that request;
3. authenticated requests with client-supplied app, capability, parameters,
   user, authority, grant, Runtime, or Governance fields each return HTTP 422
   before provider or chat execution; and
4. an actual JSON array containing two resolved candidate objects fails closed
   after exactly one bounded provider attempt with no chat execution.

The correction exposed no behavioral defect. No runtime implementation,
endpoint contract, provider behavior, certified prerequisite, or Subscription
Manager source changed.

## Certification Closure

Astra live re-review `4886585552` independently verified the correction commit
`4f09bf3cfdf01decb4be1feca2dc79887da6e531` against Issue #8 and the prior
review gate. All four mandatory proof blockers are closed in the committed tree.
The correction is exactly one commit ahead of the initially reviewed executable
implementation and contains tests plus evidence records only; runtime source is
unchanged from the architecture-compliant implementation already reviewed.

`4f09bf3cfdf01decb4be1feca2dc79887da6e531` is the certified executable target
for `ASTRA-AI-INTENT-001`.

Certification does not authorize frontend integration, merge, manual
deployment, production configuration, or production use. PR #9 remains open,
draft, and unmerged. Production remains NOT APPROVED.

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
`OpenAIIntentProvider` uses the OpenAI Responses API structured-output contract
through strict `text.format` JSON Schema. It performs one bounded HTTP attempt
with zero retries, bounded timeout/output/body sizes, `store=false`, and no
tools or function definitions.

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

Focused intent/provider/agent validation at the certified target:

```text
101 passed
1 skipped — real OpenAI smoke not run; credential gated
```

Committed-tree focused suite plus certification parent-source guard:

```text
102 passed
1 skipped — same credential-gated smoke
```

Full Astra regression validation:

```text
551 passed
33 subtests passed
1 skipped — same credential-gated real-provider smoke
```

Compileall passed. `git diff --check` passed. GitHub's automatic Vercel PR
status check succeeded at the certified commit. The real-provider smoke remained
credential-gated and was not required for deterministic certification.

Authenticated HTTP database provenance used a deterministic fake intent
provider with the materially different natural-language question
`How many services have I subscribed to?`. The fresh candidate resolved to
`subscription.count_all`, passed deterministic catalog validation, and entered
the unchanged certified chain. The primary authenticated owner's DB-backed
count was 2, became 3 after a committed owner-scoped Subscription Manager row,
and the second authenticated user saw only their own count of 1.

Security coverage includes exact-path provider independence, multiple
paraphrases for every certified read, strict day values, fresh catalog drift,
genuinely foreign app identity, a catalog-valid capability absent from the
request projection, hallucinated/foreign capabilities, extra identity/role/
grant/activation/Runtime/Governance/SQL/DB/tool/confidence/explanation fields,
an actual two-candidate array, malformed/empty/oversized provider output,
timeout/unavailability with zero retries, prompt injection, write requests,
auth negatives, blocked users, feature and environment gates, foreign
conversations, and authenticated HTTP client authority-shaped fields.

## Certification And Downstream Frontend

Astra certification review `4886585552` approved ASTRA-AI-INTENT-001 at exact
backend executable `4f09bf3cfdf01decb4be1feca2dc79887da6e531`.
ASTRA-AI-INTENT-001 is Certified / Approved / Closed. Certification did not
authorize merge, deployment, production configuration, or production use.

Product Owner/Astra separately authorized the downstream frontend task through
`srkarthi1982/ansiversa#4`. Frontend commit
`eceab9c26516ff859c86899a23bd79a553304e2b` consumes this certified endpoint
without changing the backend contract. Draft stacked frontend PR #5 remains
open and unmerged. The frontend implementation is pending Astra review and is
recorded in `sources/33-astra-frontend-governed-natural-language-agent.md`.

```text
ASTRA-AI-INTENT-001 — Backend Approved / Certified / Closed
Certified executable target — 4f09bf3cfdf01decb4be1feca2dc79887da6e531
Astra certification review — 4886585552
ASTRA-FE-AGENT-001 — Implemented / Pending Astra Review
Backend PR #9 — OPEN / DRAFT / UNMERGED
Frontend PR #5 — OPEN / DRAFT / UNMERGED
Production — NOT APPROVED
```
