---
name: resolve-api
description: Use when adding, changing, documenting, or reviewing a Re:Solve REST/API resource, action, token scope, outbound webhook, idempotent mutation, or developer-facing integration contract.
---

# Re:Solve API

Read `07-api/api-and-webhooks.md`, canonical permissions, Action Registry, data provenance, security and the source domain spec.

## Principles
API is a first-class product surface, not a thin database wrapper. Reuse the same domain services/commands as UI where practical.

## Resource/action design
Define:
- versioned route/resource/action;
- actor and use case;
- request/response schema;
- stable identifiers and human-readable reference where appropriate;
- required capability/scope and object-level authorization;
- filtering/sorting/search/pagination conventions;
- idempotency for retryable/side-effecting writes;
- concurrency/version behavior where relevant;
- audit and domain events;
- errors/correlation id;
- rate-limit class;
- sensitive-field redaction;
- OpenAPI documentation.

## Actions
Prefer registered domain Actions for meaningful mutations. Do not create UI-only permission semantics that differ from API behavior.

## Webhooks outbound
Define event set, payload version, signature, delivery id, retry/backoff, dead-letter/pause, logs and secret-reference behavior. Subscribers never gain source-record access they were not authorized to receive.

## Provider callbacks
External provider webhooks belong to Connector runtime, not generic API controllers.

## Security
No arbitrary SQL, raw provider credentials, broad Vault reveal, stack traces or hidden internal fields. Token scopes are narrow, revocable and expirable. High-risk operations require stronger scopes/confirmation policy as specified.

## Completion
Update OpenAPI/docs/tests, verify cross-organisation/property denial, retry/idempotency, validation errors and audit. Ensure API semantics can remain stable even if Supabase/Lovable implementation details change.