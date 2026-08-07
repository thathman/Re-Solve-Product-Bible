# Core Connector Contracts

## Purpose
Define the first connector/provider set Re:Solve expects to support while preserving replaceability, data authority and shared lifecycle behavior.

## Shared requirements
Every Connector implementation declares:
- Connector Type/capabilities;
- Instance model;
- authentication/protected credential reference;
- Principal permissions;
- mappings;
- data authority/sync direction/conflict policy;
- source/freshness expectations;
- health check;
- rate limits;
- inbound/outbound event behavior;
- verification/idempotency/retry/dead-letter;
- registered Actions and risk levels;
- Audit/log/diagnostics;
- API/MCP/Àríyá exposure;
- disable/disconnect/uninstall behavior.

Credentials never live as ordinary plaintext settings.

## ChatwootConnector
Purpose: managed client support.

Capabilities/context:
- account/contact/inbox mappings;
- conversation references/summaries;
- team/agent references where operationally useful;
- safe labels/custom context;
- selected support metrics;
- widget/deep-link launch;
- webhooks;
- health/freshness.

Chatwoot owns conversation/message truth, support Knowledge and Captain. Re:Solve does not recreate the agent console or mirror every message.

## WhatsApp/BaileysConnector
Purpose: Re:Solve-to-client operational communications.

Use cases:
- Project/Request updates;
- reminders/Approvals;
- invoice/payment/receipt;
- Renewals;
- Property outage/recovery/maintenance;
- client onboarding/offboarding communication;
- direct operational message.

Requirements include session health, sender identity, authorized recipient mapping, communication eligibility/privacy, media policy, delivery state, throttling, retry and Audit.

It is not the client's end-customer support inbox.

## PaymentConnector implementations
Examples: Bachs initially; optional Paystack/Flutterwave or future provider packages.

Capabilities may include:
- create Payment intent/link;
- verify/normalize provider event;
- get transaction;
- refund where supported/authorized;
- settlement/reconciliation metadata;
- health.

A provider implementation may be distributed as a Plugin registering a PaymentConnector.

Verified provider evidence establishes Payment truth; browser return pages never do.

## OpenRouter AIConnector
Purpose: initial provider implementation for Àríyá/Re:Solve AI.

Capabilities:
- model catalogue/metadata;
- completion/tool-capable request;
- routing/fallback;
- usage/cost evidence;
- rate/provider health.

Chatwoot Captain remains separate.

## Documenso SignatureConnector
Purpose: signature provider for Document Studio/Contracts and other approved signable documents.

Re:Solve owns business record, document Final Snapshot and signature status context. Provider owns envelope/signature transaction.

Mappings may cover document snapshot, envelope, signer, state, completed evidence and verified webhooks.

## Cloudflare Connector
Purpose: optional Domain/DNS/edge/monitoring context.

See `06-connectors/cloudflare.md`.

Capability groups may include:
- Registrar: registration/expiry/auto-renew state where supported;
- DNS: zones/nameservers/records/DNSSEC context;
- Edge/TLS: selected certificate/zone health;
- Monitoring/Alerts: health checks/alert events;
- safe operational analytics where useful.

Initial policy is read-first. DNS/registrar/security writes are high impact and use Action Registry, strong capability, confirmation and possibly step-up/Approval.

Cloudflare Connector failure is not equivalent to Property outage.

## Native Monitoring versus Uptime Kuma
Re:Solve owns a native Monitoring Engine and Property Posture.

### UptimeKumaConnector
Optional compatibility connector for deployments already using Uptime Kuma. It can map existing monitors/events into normalized Monitoring Signals.

Uptime Kuma is **not** a required Re:Solve dependency and is not necessary for a fresh installation to perform common HTTP/SSL/domain/heartbeat checks.

## OpenBao VaultConnector
Optional external secret backend. It may store/reference selected system/Connector/Vault secret material while Re:Solve permission/Audit policy remains authoritative.

No backend token/path is exposed casually.

## OJS PublishingConnector
Supports multiple installations and Property/Journal mappings.

Potential capabilities:
- version/health/scheduler signals;
- journals;
- public content/issues/articles;
- role-aware workflow/submission metadata where authorized;
- selected safe management Actions.

Never expose blind-review identities, confidential editorial notes or unreleased decisions outside actual authorization.

OJS health/version/scheduler signals may contribute to Property Posture.

## WordPress CMSConnector
Potential capabilities:
- site metadata/version;
- plugin/theme inventory/update state;
- Site Health signals;
- content references;
- approved management Actions.

Version/update/site-health evidence can contribute to Property Posture. Site credentials remain protected references.

## WooCommerce CommerceConnector
Initial emphasis is operational read context such as orders/payments/fulfilment/delivery/customer mappings.

Refund/order-change writes are higher-risk registered Actions with explicit scope/confirmation. WooCommerce payment state must not override Re:Solve Billing truth unless the product workflow explicitly maps authoritative provider evidence.

## EmailConnector
Transactional/operational delivery:
- sender identities;
- send;
- accepted/delivered/bounce/failure evidence where supported;
- suppressions;
- domain/sender verification health;
- template compatibility.

Re:Solve owns communication/Notification intent. Provider owns transport evidence. Opens/clicks, if captured under privacy policy, are not absolute proof a human read the message.

## CalendarConnector
Google/Microsoft/future providers may offer:
- free/busy;
- selected event read;
- Booking/event create/update;
- external ID mapping;
- sync health.

Sync direction/conflict policy and data minimization are explicit. Re:Solve does not implement HR shifts/leave/attendance.

## StorageConnector / provider abstraction
File/Vault storage may use Supabase in development and other self-hostable/provider options later. Business File/Vault semantics remain independent of one storage provider.

## Connector Instance UI
Canonical detail tabs:
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

Summary shows name/type/provider, Operating Entity/Organisation/Property context, status/health, auth expiry, last success/sync, freshness, failures/dead-letter count and available registered Actions.

## Attention / Notifications
Persistent Connector failure, auth expiry, dead-letter buildup, stale sync and rate limitation may create Attention/Notifications. Avoid transient-noise alerts that recover automatically.

## Core UI/navigation
Connectors live under Platform -> Connectors with simple list/detail navigation. Individual providers do not add separate root apps merely because they are installed.

## Lovable build slices
1. Connector registry/Instance shell with fictional connectors.
2. shared health/mapping/events/sync-authority patterns.
3. Chatwoot + WhatsApp demo contracts.
4. Payment + OpenRouter + Documenso demo contracts.
5. Cloudflare + native-monitoring external-source integration.
6. OJS/WordPress/WooCommerce/Calendar/Email and optional Uptime Kuma compatibility.
