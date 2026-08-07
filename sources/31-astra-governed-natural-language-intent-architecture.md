# Astra Governed Natural-Language Intent Architecture

Document Status: Architecture Approved / Certified / Closed.

Created: 2026-08-07.

Canonical task: `srkarthi1982/ansiversa-api#5`.

Backend architecture base:
`615ef1b3ec375aacca9a9a9cb564832688a0d34c`.

Backend architecture commit:
`cc65502990e69c39bc542933d6d8d28aac5b0291`.

Astra architecture review: `4881828844`.

Backend architecture certification-record commit:
`00102d6669ff9021e7301f689d74090d760a2a03`.

PR #6: open, draft, unmerged.

Implementation: NOT AUTHORIZED.

Production authorization: NOT APPROVED.

## Purpose

ASTRA-AI-INTENT-ARCH-001 certifies an intent-only AI boundary for supported
Subscription Manager natural-language questions while preserving the certified
governed execution chain.

```text
question
  -> exact deterministic mapping OR bounded intent provider
  -> untrusted candidate
  -> deterministic exact validation
  -> unchanged certified AstraChatRequest and AstraChatGateway
  -> certified authority, authorization, execution, and app-owned DB read
  -> deterministic answer
```

## Ownership And Candidate Boundary

```text
Applications own capabilities. Astra owns orchestration.
```

Subscription Manager's certified `capability_catalog()` remains the only
authority-bearing catalog. A metadata-only projection may be sent to the
interpreter but cannot become a second registry. The model owns no identity,
authorization, grant, activation, Governance, Runtime, execution, tool, or DB
authority.

The proposed interpreter receives only the current question and minimal
eligible capability/parameter metadata. It may return only status, app ID,
capability ID, parameters, and bounded clarification reason. Status is exactly
`resolved`, `clarification_required`, or `unsupported`.

All output is untrusted. Extra or authority-looking fields, malformed or
oversized output, multiple candidates, unsupported or not-supplied capability,
and invalid parameters fail closed before chat construction.

The only parameterized pilot capability is
`subscription.renewing_within_days`; `days` must independently validate as a
true integer from 1 through 366. Ambiguity must clarify, not invent a number.

## API And Provider Decision

The proposed endpoint is:

```text
POST /api/v1/astra/agent/query
```

It is separate so certified `/api/v1/astra/chat` remains unchanged and the new
natural-language/provider boundary can be gated and certified independently.
It constructs the declared-intent request server-side and invokes the existing
gateway in-process. It does not depend on `/api/v1/assistant/query`.

The exact-question fast path precedes provider use and continues when the
provider is disabled or unavailable. Unmatched provider failure returns bounded
guidance and never guesses a capability.

The provider has no function/tool calling, Tool Executor, plugin, MCP, DB, HTTP,
write, or final-answer role. It receives no records, billing data, identity,
auth, grants, authority objects, SQL, DB URLs, secrets, or prior private
payloads. The first phase sends only the current turn and keeps the certified
deterministic response authoritative.

## Configuration, Privacy, And Memory

Future implementation is default-off and server-owned:

```text
ASTRA_AI_INTENT_ENABLED=false
```

It may run only in recognized non-production environments unless later
separately authorized. Client input cannot enable or select a provider/model.

Safe evidence may retain references, status, validated capability, metadata
digest, latency/output buckets, and bounded failures. Raw prompts and provider
payloads are not persisted by default. No persistent, cross-session, vector,
profile-learning, or personalization memory is introduced. Future clarification
context must be minimal, in-memory, principal-bound, current-turn, short-lived,
and invalidated on logout, principal change, stale lifecycle, or Runtime restart.

## Existing Provider Infrastructure Finding

The shared Assistant has a small provider protocol, bounded HTTP client,
environment secrets/settings, timeout, safe unavailable error, and deterministic
failure fallback. Those generic patterns may be adapted. Its free-text parser,
public knowledge prompt, Assistant route, actions/tools, response modes, and
authority assumptions must not be inherited. The governed intent client needs
strict structured validation and redacted metadata-only observability. Initial
retries are zero.

## Frozen Certified State

Certified Runtime activation, metadata activation, Read Authority, Read
Execution, backend chat, frontend chat, authentication, and Subscription Manager
catalog/adapter remain unchanged. No executable code, provider call, route,
configuration, frontend, DB/schema, tool, write, deployment, merge, or production
action is authorized by this architecture.

```text
ASTRA-AI-INTENT-ARCH-001 — Architecture Approved / Certified / Closed
ASTRA-AI-INTENT implementation — NOT AUTHORIZED
Production — NOT APPROVED
```

The certification-record commit is documentation-only and is not a new
architecture target. A separate Product Owner/Astra-authorized GitHub issue is
required before implementation.
