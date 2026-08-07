# Re:Solve Connector Platform

## Purpose
Connectors integrate Re:Solve with specialist external systems while domain logic remains provider-neutral. Connectors are replaceable implementations of stable capability contracts.

A Plugin adds business/product capability. A Connector integrates an external system. An optional provider package may be distributed as a Plugin that registers a Connector implementation.

## Goals
- prevent provider SDK leakage across domains;
- support multiple instances of one Connector Type;
- expose health, mappings, events, sync state, credentials references, limits and diagnostics;
- centralize event verification/idempotency/retry/dead-letter;
- declare data authority/sync direction/conflict policy;
- make provider substitution possible without rewriting core features.

## Connector categories
- Support
- Payment
- AI
- External Vault
- Signature
- Monitoring
- Domain / DNS / Edge
- Commerce
- CMS
- Publishing
- Email
- Messaging
- Calendar
- Storage
- Identity

## Initial/future implementations
- Chatwoot -> SupportConnector
- Bachs/Paystack/Flutterwave provider packages -> PaymentConnector implementations
- OpenRouter -> AIConnector
- OpenBao -> optional external VaultConnector
- Documenso -> SignatureConnector
- Cloudflare -> Domain/DNS/Monitoring/Edge capability connector
- Uptime Kuma -> optional MonitoringConnector for existing deployments
- OJS -> PublishingConnector
- WordPress -> CMSConnector
- WooCommerce -> CommerceConnector
- WhatsApp/Baileys -> MessagingConnector
- SMTP/transactional providers -> EmailConnector
- Google/Microsoft/etc -> CalendarConnector

Re:Solve native Monitoring does **not** require Uptime Kuma.

## Capability contracts
Each Connector Type exposes only relevant capabilities.

Conceptual examples:

### SupportConnector
- get conversation summaries/reference
- add safe context
- list inbox/team references
- health

### PaymentConnector
- create payment intent/link
- verify/get payment
- refund where supported/authorized
- parse verified event
- health

### MessagingConnector
- send message/template where supported
- delivery status
- inbound event where applicable
- health

### MonitoringConnector
- list/source monitor signals
- health/status
- ingest alert events
- source freshness

### DomainRegistrar/DNS capability
- registration/expiry/auto-renew read where supported
- zone/DNS metadata
- controlled high-impact writes only when explicitly exposed/authorized

Exact technical signatures remain implementation decisions.

## Connector instances
One Type can have many Instances.

Example OJS Instances:
- Westbridge Journals
- Meridian Research Review

Instance metadata:
- type/provider
- display name
- Operating Entity
- Organisation/Property context where relevant
- endpoint/account reference
- environment
- protected auth reference
- state/health
- capabilities
- allowed actions/tools
- last successful call/sync
- provider version
- rate-limit state
- freshness

Raw credentials live behind approved protected storage.

## Admin experience
### Overview
Show provider/type/instances/status/health/last event/failures/auth expiry/configuration.

### Instance detail
Tabs:
- Overview
- Configuration
- Capabilities
- Mappings
- Sync / Authority
- Events
- Logs
- Health
- Permissions
- Audit

Actions may include test, enable/disable, reconnect, rotate credentials, resync, replay failed event, diagnostics and disconnect.

## Shared Integration Event runtime

```text
External Provider
-> Receiver
-> Raw Event Record
-> Verification
-> Idempotency
-> Normalize
-> Process
-> Retry
-> Dead Letter if exhausted
```

Minimum metadata:
- connector instance
- provider
- external event id
- type
- payload hash
- received/verified state
- processing state
- attempts/next retry/error
- correlation id
- timestamps
- retention class

Do not expose sensitive raw payloads in ordinary logs.

## Event states
received, rejected, duplicate, pending, processing, processed, retrying, dead_letter and manually_replayed.

## Idempotency / retry
Prefer provider event IDs; otherwise documented derived keys. Business mutations triggered by events should also be idempotent where practical.

Retry distinguishes retryable/terminal errors, uses bounded backoff and exposes dead-letter/manual replay.

## Mapping layer
First-class mappings connect Re:Solve and provider identifiers, for example:
- Organisation/Contact/Property -> Chatwoot references
- Invoice -> payment-provider reference
- Property -> Cloudflare zone/domain
- Property -> OJS/WordPress/WooCommerce resource

Mappings are auditable and repairable.

## Data provenance and sync contract
Each mapping/Connector must declare:
- read/write direction;
- authoritative source per field/resource;
- trigger model;
- conflict policy;
- stale threshold;
- create/update/delete/archive semantics.

Do not use silent newest-wins for consequential data.

## Secrets
Credentials are references, masked in UI, rotatable, audited and never logged/displayed casually. Connection tests must not reveal raw credentials.

## Health
Possible connector states:
- connected/healthy
- degraded
- authentication_required
- rate_limited
- misconfigured
- provider_unavailable
- stale
- disabled

Connector health is separate from target/business-record health. A Cloudflare/Uptime connector outage must not automatically mark every Property down.

## Permissions
Canonical examples:
- `connectors.read`
- `connectors.configure`
- `connectors.test`
- `connectors.credentials.rotate`
- `connectors.events.replay`
- `connectors.disconnect`

Provider-specific dangerous operations may require additional capabilities/step-up/approval.

## Notifications / Attention
Persistent authentication failure, dead-letter accumulation, stale sync, rate limiting or provider outage can create Platform Attention/Notifications without noise from transient recovery.

## Automations / Action Registry
Verified Connector events may trigger Automations. Connector-backed writes must register approved Actions rather than expose arbitrary provider calls.

## API / MCP / Àríyá
Expose safe health/instance/capability/operational actions. Machine/AI clients never receive provider credentials or arbitrary provider API access.

## Special boundaries
### Chatwoot
Chatwoot remains support conversation/message truth.

### WhatsApp/Baileys
Operational Re:Solve-to-client messaging, not client-customer helpdesk.

### Payments
Provider confirmation/event truth establishes Payment state; Billing remains provider-neutral.

### Monitoring
Native Re:Solve Monitoring owns common monitoring/posture logic. External monitors contribute optional signals.

### Cloudflare
First-class optional source for domain/DNS/edge/health signals. High-impact DNS/security/registrar writes are strongly controlled.

## Acceptance criteria
- multiple Instances per Type;
- credentials protected;
- events verified/deduped/retryable/diagnosable;
- sync authority/conflict policy explicit;
- domain code consumes capability contracts rather than provider branching;
- disabled Connector cannot keep normal processing;
- mappings can be repaired;
- health distinguishes provider failure from business target failure;
- API/MCP/Àríyá cannot bypass permissions.
