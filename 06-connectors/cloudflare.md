# Cloudflare Connector

## Purpose
Cloudflare is a first-class optional Re:Solve connector for domain/DNS, edge, certificate, alerting and monitoring context.

It must not become a mandatory infrastructure dependency or the only supported registrar/DNS/monitoring provider.

## Connector capabilities
One Cloudflare instance may expose one or more capability groups depending on account permissions and available APIs:

### Domain/Registrar
- list managed registrations where supported
- registration/expiry state
- auto-renew state
- registrar status
- domain mapping

### DNS
- zones
- nameservers
- DNS records metadata
- DNSSEC status where available
- configuration health

### Edge/TLS
- zone/TLS state
- certificate-related status where available
- selected edge configuration health

### Monitoring/Health
- origin/health-check state where configured
- alert/webhook ingestion
- recovery/degradation events
- selected performance/availability signals

### Analytics/Posture
- safe summarized traffic/health metrics where useful
- security/edge signals only when they contribute clear operational value

## Mapping
Mappings may include:
- Connector Instance -> Cloudflare Account
- Property(Domain) -> Zone
- Property(Website/Application) -> Zone/hostname
- Renewal Obligation -> Registration
- Native Monitor -> Cloudflare health signal reference

Mappings are first-class and repairable.

## Read-first policy
Initial integration should prioritize read/observe capabilities.

High-impact writes such as:
- modifying production DNS
- changing registrar/renewal configuration
- changing SSL/TLS/security configuration
- deleting zones/records
must require explicit provider-supported capability, strong permissions, confirmation, audit, and potentially step-up/approval.

Àríyá cannot casually execute production DNS/security changes from natural-language requests.

## Events
Cloudflare webhook/alert events should enter the shared Integration Event runtime:
verify/authenticate -> dedupe -> normalize -> process -> retry/dead-letter.

Normalized events may update:
- Monitoring Signal
- Property Posture
- Incident
- Renewal/Expiry Obligation
- Attention Item
- Notification

## Health
Connector health is independent from property health.

States should distinguish:
- connector healthy
- authentication required
- rate limited
- provider/API unavailable
- stale sync
- mapped property actually degraded

## Credentials
Use least-privilege API tokens where supported. Raw credentials live behind the Vault/secret abstraction and are never exposed in normal connector records/logs.

## Multi-instance
Support multiple Cloudflare accounts/instances across different operating entities or clients where needed.

## Portal
Portal should never expose Cloudflare-specific implementation detail unless it is genuinely useful. Prefer client-safe domain/property status and renewal information.

## API/MCP
Expose provider-neutral Re:Solve operations first. Cloudflare-specific diagnostic operations may exist for authorized technical users.

## Acceptance criteria
- Cloudflare can contribute expiry/DNS/health signals without owning Re:Solve's Property model
- connector outage does not falsely mark all properties down
- dangerous writes are strongly controlled
- native Re:Solve Monitoring continues to work without Cloudflare
- multiple account instances and explicit mappings are supported
