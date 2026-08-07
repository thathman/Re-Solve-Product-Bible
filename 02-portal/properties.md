# Client Portal — Properties

## Purpose
Give client users a clear, role-appropriate view of every property Re:Solve manages for their organisation without exposing staff-only operational complexity.

## Primary flows
1. Browse permitted properties.
2. Understand current property health and service status.
3. Open a property workspace.
4. Review related projects, support context, files, renewals, monitoring summaries, maintenance and approved Vault items.
5. Take required client actions.

## Property list
Each card/row may show: name, type, parent, status, health, current service, active project count, open client actions, next renewal, recent incident, and last update. Users only see properties permitted by organisation membership and property grants.

Filters: type, status, health, service, parent property, requires action. Search matches name, domain, code and aliases.

## Property workspace
Tabs/sections:
- Overview
- Projects
- Support
- Services
- Files
- Monitoring
- Renewals
- Vault
- Activity

Overview prioritizes: current status, what is being managed, what requires client attention, recent changes, active work, known incidents, next maintenance and renewals.

## Support
Do not recreate Chatwoot. Surface selected support state and provide a clear action to open/start support through the configured Chatwoot experience.

## Monitoring
Expose client-safe summaries only: uptime, recent incidents, certificate/domain expiry, backups and maintenance where relevant. Hide internal diagnostics, credentials, provider internals and noisy raw checks.

## Vault
Only items explicitly shared with the client and permitted to the current user are visible. Reveals/downloads remain audited and may require step-up authentication.

## States
Support loading, empty organisation, no permitted properties, healthy, degraded, incident, maintenance, archived, partially configured connector data, offline/PWA stale-cache state, permission denied and connector unavailable.

## Notifications
Property-related notifications deep-link into the relevant property and section. Urgent outage/expiry events may also use push/email/WhatsApp according to policy.

## API / MCP
API exposes only caller-authorized client-safe property representations. MCP read tools may include list_my_properties, get_my_property, get_property_status, get_property_upcoming_renewals. No hidden monitoring details or Vault data through generic tools.

## Mobile/PWA
Property cards become the primary mobile representation. Critical status/action information remains visible without horizontal scrolling. Selected summaries may be cached read-only for offline access.

## Extension points
Plugins may add approved property tabs/cards/actions. Connectors may contribute typed health summaries and external references but may not bypass visibility rules.

## Lovable build slices
1. Property list + responsive cards/filtering with demo data.
2. Property workspace overview.
3. Projects/support/services tabs.
4. Monitoring/renewals/files/activity.
5. Vault and permission-sensitive states.