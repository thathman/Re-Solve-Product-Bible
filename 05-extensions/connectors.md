# Re:Solve Connector Platform

## Purpose

Connectors integrate Re:Solve with specialist external systems while keeping domain logic provider-neutral. Connectors are replaceable implementations of stable capability contracts.

A connector does not add an unrelated business domain. A plugin may depend on a connector, but provider integration must remain separate from business logic.

## Core goals

- prevent provider SDKs from leaking across the product
- support multiple instances of the same connector type
- expose connection health, logs, events, credentials, rate limits, and sync state
- centralize webhook verification, retry, idempotency, and diagnostics
- support future provider substitution without rewriting business modules
- make integrations manageable from Admin rather than environment variables alone

## Connector categories

- Support
- Payment
- AI
- Vault
- Signature
- Monitoring
- Commerce
- CMS
- Publishing
- Email
- Messaging
- Calendar
- Storage
- Identity

## Initial connector implementations

- Chatwoot → SupportConnector
- Bachs → PaymentConnector
- Paystack → PaymentConnector
- Flutterwave → PaymentConnector
- OpenRouter → AIConnector
- OpenBao → VaultConnector where configured
- Documenso → SignatureConnector
- Uptime Kuma → MonitoringConnector
- OJS → PublishingConnector
- WordPress → CMSConnector
- WooCommerce → CommerceConnector
- WhatsApp/Baileys → MessagingConnector
- SMTP/Resend/other provider → EmailConnector

## Connector contract

Each connector type exposes only the capabilities relevant to its domain. Example conceptual contracts:

### SupportConnector
- getConversations
- getConversation
- createConversation where supported
- addContext
- getUnreadCount
- listInboxes
- listTeams
- health

### PaymentConnector
- createPaymentIntent/link
- verifyPayment
- getPayment
- refund where supported and permitted
- parseWebhook
- health

### MessagingConnector
- sendMessage
- sendTemplate where supported
- resolveDeliveryStatus
- receiveInboundEvent
- health

Exact implementation signatures are deferred to technical planning.

## Connector instances

One connector type may have many instances.

Example OJS instances:
- Kampala University OJS
- DOMJ OJS
- AJTMBR OJS

Each instance stores non-secret operational metadata:
- connector type
- provider
- display name
- organisation
- property
- endpoint
- environment
- auth reference
- status
- health
- capabilities
- allowed tools/actions
- last successful call
- last sync
- version
- rate limit state
- created/updated metadata

Raw credentials belong in approved secure storage; normal records store references only.

## Admin experience

### Connector Overview

Cards/rows show:
- provider
- type
- instances
- status
- health
- last event
- failures
- authentication expiry warning
- configuration action

### Instance detail

Tabs:
- Overview
- Configuration
- Capabilities
- Mappings
- Events
- Logs
- Health
- Permissions
- Audit

Actions:
- test connection
- enable/disable
- rotate credentials
- resync
- replay failed event
- view diagnostics
- disconnect

## Shared integration event runtime

All external events enter a common runtime.

Flow:

```text
External Provider
→ Receiver
→ Raw Event Record
→ Signature/Auth Verification
→ Idempotency Check
→ Normalize
→ Process
→ Retry if needed
→ Dead Letter if exhausted
```

Minimum event fields:
- id
- connector_instance_id
- provider
- external_event_id
- event_type
- payload_hash
- received_at
- verified
- verification_detail
- status
- attempt_count
- next_retry_at
- last_error
- correlation_id
- processing_started_at
- processed_at
- retention class

Do not expose full sensitive payloads to ordinary logs.

## Event states

- received
- rejected
- duplicate
- pending
- processing
- processed
- retrying
- dead_letter
- manually_replayed

## Idempotency

Where providers offer stable event IDs, enforce uniqueness per connector instance. Where they do not, use a documented derived idempotency key/payload hash strategy.

Business mutations triggered by connector events must also be idempotent where practical.

## Retry

Central retry behavior should support:
- exponential/backoff policy
- max attempts
- retryable vs terminal errors
- next retry time
- manual retry
- dead-letter visibility

## Mapping layer

Connectors often need mappings between Re:Solve records and provider records.

Examples:
- Organisation ↔ Chatwoot account/contact context
- Property ↔ Chatwoot inbox/context
- Invoice ↔ Bachs payment reference
- Property ↔ OJS installation/journal
- Organisation/contact ↔ WooCommerce customer

Mappings are first-class records with audit and repair tooling.

## Secrets

Connector credentials must be referenced, not casually copied into settings records or logs.

Rules:
- mask secret values
- allow rotation
- record last rotation
- audit credential changes
- restrict reveal/export
- test connection without exposing raw credential

## Health model

Health states:
- connected
- healthy
- degraded
- authentication_required
- rate_limited
- misconfigured
- unavailable
- disabled

Health may consider:
- authentication validity
- endpoint reachability
- recent successful operations
- webhook delivery
- sync freshness
- rate limits

## Permissions

Examples:
- connectors.read
- connectors.configure
- connectors.test
- connectors.rotate_credentials
- connectors.replay_events
- connectors.disconnect

Provider-specific sensitive actions may require additional permissions.

## Notifications

Notify appropriate administrators for:
- authentication expiration
- persistent connector failure
- dead-letter accumulation
- rate-limit degradation
- credential rotation due
- provider outage if materially affecting operations

Avoid noisy notifications for transient failures that recover automatically.

## Automations

Connector events can be automation triggers after verification and normalization.

Connector actions can be automation actions only when explicitly registered and permissioned.

## API and MCP

API should expose connector health, instances, capability metadata, and permitted operational actions.

MCP may expose safe connector-backed tools through Re:Solve's tool registry. AI clients must never receive unrestricted provider credentials or arbitrary provider API access.

## Chatwoot special boundary

Chatwoot remains support truth. Re:Solve surfaces selected business context and analytics without copying every message into Re:Solve as canonical data.

## WhatsApp/Baileys special boundary

WhatsApp/Baileys is primarily for Re:Solve-to-client operational messaging and notifications. It is not the helpdesk for a client's end customers.

## Payment special boundary

Provider confirmation/webhook truth, not browser-return success, establishes payment state. Re:Solve billing remains provider-neutral.

## Acceptance criteria

- multiple instances of a connector type are supported
- credentials are not stored or logged as ordinary plaintext configuration
- external events are verified, deduplicated, retryable, and diagnosable
- connector health is visible and permission-controlled
- domain code can consume connector contracts without provider-specific branching throughout the app
- disabled connector cannot continue processing actions/events except explicitly required cleanup
- mappings can be inspected and repaired
- API/MCP exposure never bypasses connector permissions

## Lovable build slices

1. connector registry + overview
2. connector instance record + detail page
3. test connection + health model
4. mapping records
5. integration event store + event viewer
6. retry/dead-letter/manual replay
7. first real connector adapter implementation
8. credential rotation and diagnostics
