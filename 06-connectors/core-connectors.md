# Core Connector Contracts

## Purpose
Define the first connector set Re:Solve expects to support while preserving replaceability and consistent lifecycle behavior.

## Shared requirements
Every connector implementation must define:
- connector type
- instance model
- authentication method
- secret-reference strategy
- health check
- capabilities
- rate-limit behavior
- sync/webhook/event behavior
- retry/idempotency requirements
- mapping model
- permissions
- audit events
- logs/diagnostics
- API/MCP exposure
- uninstall/disable behavior

Connector configuration is managed through Re:Solve. Sensitive credentials are stored through approved secure-secret mechanisms, not ordinary settings fields.

## ChatwootConnector
Purpose: managed client support.

Owns/integrates:
- inbox mapping
- contact mapping
- conversation references
- teams/agents metadata where needed
- labels/context
- support metrics
- widget/context launch
- support knowledge boundary
- incident/support context handoff

Re:Solve must not recreate the Chatwoot agent console or Captain engine.

## WhatsApp/BaileysConnector
Purpose: Re:Solve-to-client operational communication.

Use cases:
- ticket/status notices
- project updates
- approval reminders
- payment/receipt notifications
- renewals
- monitoring alerts
- general operational messages

Requirements:
- session/connection health
- sender identity
- recipient mapping
- template/message policy
- delivery state where available
- throttling
- retry
- opt-out/communication preference rules where applicable
- strict distinction from client-customer support handled by Chatwoot

## PaymentConnector implementations
Initial examples: Bachs; optional Paystack/Flutterwave modules/plugins.

Capabilities may include:
- create payment intent/link
- verify provider event
- retrieve transaction
- refund where supported/authorized
- reconcile
- health/configuration

Provider webhook truth supersedes browser-return assumptions. Core Billing remains provider-neutral.

## OpenRouterConnector
Purpose: provider implementation for Re:Solve AI only.

Capabilities:
- model catalogue/config
- chat/completion/tool-capable requests
- model routing
- usage/cost metadata
- failure/fallback signaling

Chatwoot Captain is not routed through the Re:Solve AI engine unless a future explicit integration says otherwise.

## DocumensoConnector
Purpose: specialist document-signing provider.

Re:Solve owns commercial records and signature status/context; Documenso performs envelope/signature workflows. Map document/envelope/signer/status/completion evidence and webhook events.

## UptimeKumaConnector
Purpose: monitoring provider.

Map monitors to Re:Solve properties/checks. Normalize status and events without treating connector availability as property health. Support incident creation and maintenance context through Re:Solve rules.

## OpenBaoConnector
Purpose: optional secure secret backend/provider.

May store or reference system/integration secrets and selected Vault credential payloads depending on architecture. Re:Solve permissions/audit remain authoritative for product access. Never expose backend paths/tokens to normal users.

## OJSConnector
Purpose: publishing-system integration.

Supports multiple instances and journal/property mapping.

Potential safe capabilities:
- version/health
- journals
- public content/current issue
- articles/metadata
- authenticated role-aware submission/workflow data

AI/API/MCP tools must enforce OJS role boundaries. Never expose blind-review identities, confidential editor notes, unreleased decisions or other users' submissions without explicit authorization.

## WordPressConnector
Purpose: CMS/property context.

Potential capabilities: site metadata, version, plugin/theme inventory, health, content references and safe management actions where authorized. Never store site passwords in connector record fields.

## WooCommerceConnector
Purpose: commerce integration.

Initial emphasis: read-only client-safe operational data such as order/payment/fulfilment/delivery status. Write operations such as refunds/order changes are higher risk and added only with explicit scopes/confirmation.

## EmailConnector
Purpose: transactional and operational email delivery.

Capabilities: sender identity, send, delivery metadata where provider supports it, suppression/bounce handling, template compatibility and health. Re:Solve owns notification intent/templates/preferences; provider owns delivery transport.

## CalendarConnector
Google/Microsoft implementations may synchronize selected Re:Solve events and external calendar events. Maintain external IDs, sync direction, conflict policy and duplicate protection.

## Connector instance UI
Every instance page shows:
- name
- type
- linked organisation/property scope where applicable
- status/health
- capabilities
- auth state/expiry
- last successful operation
- last error
- event backlog/dead-letter count
- mappings
- test connection
- rotate/re-authorize
- disable
- logs

## Lovable build slices
1. Connector registry/instance shell with mock connectors.
2. Shared health/config/mapping/event patterns.
3. Chatwoot + WhatsApp demo contracts.
4. Payment + monitoring + AI connector demos.
5. OJS/WordPress/WooCommerce and remaining provider instances.