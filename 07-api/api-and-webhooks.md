# Re:Solve API and Webhooks

## Purpose

Re:Solve must be API-complete enough that its useful business capabilities can be integrated into external tools, automations, agents, and future products without scraping the UI or bypassing permissions.

The API is a first-class product surface. The UI, automations, plugins, connectors, and MCP layer should rely on the same business contracts wherever practical.

## Principles

- versioned and documented
- explicit authentication and scopes
- organisation/property isolation
- predictable pagination/filtering/sorting
- idempotent writes where appropriate
- strong audit for sensitive actions
- consistent errors
- no raw database exposure
- no provider secret exposure
- compatible with self-hosted deployment

## Surface

Conceptual versioned routes:

```text
/api/v1/organisations
/api/v1/contacts
/api/v1/properties
/api/v1/projects
/api/v1/tasks
/api/v1/opportunities
/api/v1/proposals
/api/v1/contracts
/api/v1/invoices
/api/v1/payments
/api/v1/approvals
/api/v1/notifications
/api/v1/files
/api/v1/vault
/api/v1/knowledge
/api/v1/support
/api/v1/automations
/api/v1/plugins
/api/v1/connectors
/api/v1/audit
```

Exact routing style may follow Lovable-preferred implementation conventions, but the product contracts remain stable.

## API documentation

Provide machine-readable OpenAPI documentation and a human developer portal/reference.

Each operation documents:
- purpose
- required scope
- request
- response
- errors
- pagination
- idempotency
- rate limits
- audit behavior
- side effects

## Authentication

Support personal/service API credentials with:
- name
- owner
- scopes
- created date
- expiration
- last used
- optional IP restrictions later
- revoke/rotate

OAuth/service integrations may be added later without replacing the token model.

Raw API tokens are shown only at creation/rotation.

## Scopes

Scopes are capability based, e.g.:
- organisations:read
- organisations:write
- properties:read
- projects:write
- billing:read
- invoices:create
- vault:metadata:read
- notifications:create
- automations:run

Vault reveal/download and high-risk financial actions require narrower scopes.

## Filtering and pagination

Collections should support consistent cursor/page semantics chosen at implementation time, plus documented:
- filter
- sort
- search
- date range
- relationship filters
- status

Avoid unique ad-hoc query conventions per module.

## Idempotency

Mutations that may be retried or create external side effects should accept an idempotency key where appropriate.

Examples:
- create invoice
- create payment request
- trigger automation
- send operational message
- create approval request

## Errors

Standard error envelope includes:
- stable error code
- safe message
- field errors where applicable
- request/correlation ID
- remediation hints when safe

Never leak secrets, stack traces, internal SQL, or provider credentials.

## Rate limits

Rate limits may vary by:
- token/client
- route class
- operation risk
- connector/provider capacity

Responses should surface limit metadata where practical.

## Webhooks outbound

External subscribers can register webhook endpoints for permitted events.

Subscription includes:
- name
- endpoint
- event set
- secret reference
- status
- created by
- last success
- last failure
- failure count

## Webhook delivery

Deliveries include:
- event ID
- event type
- occurred_at
- schema/version
- data
- correlation ID

Requests are signed. Delivery history stores safe request metadata, response status, timing, attempt count, and truncated non-sensitive response/error details.

## Delivery lifecycle

- queued
- sending
- delivered
- retrying
- failed
- disabled

Use retry/backoff and dead-letter policy. Repeated endpoint failure may automatically pause delivery and notify administrators.

## Event catalogue

Document first-class events across domains. Plugins may add namespaced events.

Examples:
- organisation.created
- contact.updated
- property.health_changed
- project.completed
- invoice.sent
- invoice.paid
- payment.confirmed
- approval.completed
- vault.access_granted
- connector.health_changed

## Inbound webhooks

Provider callbacks belong to the Connector integration runtime, not arbitrary general API controllers. Custom generic inbound automation webhooks may be supported as explicit automation triggers with authentication and rate limiting.

## Admin experience

Settings > API & MCP should include:
- API overview
- API tokens
- scopes
- Webhooks
- delivery logs
- developer docs
- usage/limits

Token creation flow must show requested scopes before creation.

## Audit

Audit:
- token created/revoked/rotated
- scopes changed
- webhook created/changed/deleted
- sensitive API calls
- high-risk failures

## MCP relationship

MCP is built on top of controlled Re:Solve capabilities. It should not invent an alternate permission universe. API and MCP may share services/commands, but MCP tools have their own curated schemas and AI safety constraints.

## Plugin relationship

Plugins can register documented namespaced API resources/actions through the platform registry. They inherit auth, scopes, rate limiting, audit, and docs conventions.

## PWA/client relationship

The first-party web/PWA may use internal endpoints optimized for product behavior, but public API semantics should remain stable and independently documented.

## Acceptance criteria

- useful business operations have documented programmatic equivalents where appropriate
- tokens are scope-limited, revocable, expirable, and audited
- cross-organisation/property access is denied server-side
- idempotent operations can be retried safely
- outbound webhooks are signed, observable, and retryable
- provider callbacks use the connector runtime
- plugin endpoints cannot bypass core auth/audit
- OpenAPI documentation remains generated/current

## Lovable build slices

1. API token records + token management UI
2. common API auth/scope enforcement
3. first versioned read APIs
4. write APIs + idempotency
5. OpenAPI/docs
6. outbound webhook subscriptions
7. delivery/retry/log viewer
8. plugin API registry
