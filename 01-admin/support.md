# Support Operations & Chatwoot

## Purpose
Support in Re:Solve is the operational context layer around Chatwoot-managed client support. Re:Solve must not rebuild Chatwoot's helpdesk, web chat, conversation engine, support knowledge base, routing, teams, or AI.

## Ownership boundary
Chatwoot owns:
- inboxes and channels
- customer conversations and messages
- support attachments
- agent/team assignment
- conversation status and routing
- web chat widgets on client properties
- support knowledge used by Chatwoot
- CSAT and native support analytics
- Chatwoot AI/Captain

Re:Solve owns:
- organisations and contacts
- properties
- services and support entitlements
- property/support mappings
- incidents and operational escalations
- support summaries
- related project/billing/property context
- connector health
- selected analytics and business reporting
- client access/visibility rules

## Support overview
A calm operational view showing:
- open/waiting/urgent conversation counts by client/property
- breached/at-risk SLA where available
- active incidents
- client/property support health
- support entitlement warnings
- recent high-priority conversations
- Chatwoot connector health
- unresolved items that should become projects/tasks/incidents

Do not mirror every message into Re:Solve.

## Conversation references
Re:Solve stores durable mappings/references, not a second message store. Fields may include organisation, contact, property, Chatwoot inbox, conversation ID, status snapshot, priority, category, assigned team/agent reference, first/last activity timestamps, support plan, incident/project linkage, and last sync.

## Property context
Every managed web-chat/support flow should attempt to identify:
- organisation
- property
- property type
- source domain/path
- authenticated user context when available
- support category
- application type

Never send passwords, secrets, session tokens, or unnecessary PII to Chatwoot.

## Chatwoot connector
Capabilities:
- create/update contact mapping
- create/read inbox mappings
- fetch conversation summaries
- fetch unread/open counts
- attach safe custom attributes/context
- assign team/labels where authorized
- health check
- webhook ingestion
- deep link to conversation
- provision/update property support configuration where policy allows

## Inbox model
Default: one organisation-level inbox per external client family, with property context carried on each conversation. Do not create an inbox per property unless a genuine isolation requirement exists.

Airix-owned brands may each have their own brand inbox.

## Support plans / entitlements
Support entitlement may define:
- covered properties/services
- support hours
- response targets
- escalation rules
- included request categories
- exclusions
- emergency route
- client contacts authorized to escalate

Entitlement does not replace Chatwoot SLA mechanics; Re:Solve supplies commercial/operational context.

## Incidents
Incident is a Re:Solve record for an operational service-impacting event. It can link to multiple Chatwoot conversations, properties, monitoring signals, tasks/projects, client notifications, root cause, timeline, mitigation, and resolution.

States: Investigating → Identified → Monitoring → Resolved → Postmortem / Closed.

Severity is separate from Chatwoot conversation priority.

## Client portal support
Portal shows:
- Start/continue support action
- recent conversation references where permitted
- open/waiting/resolved counts
- support plan/coverage summary
- active known incidents
- service status
- escalation route

The Chatwoot widget may be globally available. Full messaging remains Chatwoot-powered.

## WhatsApp distinction
Re:Solve WhatsApp/Baileys is for operational communication between Re:Solve and clients: ticket/status updates, reminders, approvals, invoice notices, project updates, alerts, and direct client messages. It is not the client-customer support inbox.

## Permissions
support.read, support.analytics.read, support.context.manage, support.entitlements.manage, incidents.manage, support_connector.configure, support_mapping.manage. Access to actual Chatwoot conversations additionally respects connector and client/property scope.

## Notifications
Re:Solve should surface meaningful support events only: urgent escalation, SLA risk, new incident, incident update, conversation needing operational action, connector failure, entitlement mismatch. Do not notify on every Chatwoot message.

## Automations
Examples:
- high-severity monitoring alert → create/associate incident
- urgent Chatwoot conversation with matching property → alert assigned Re:Solve owner
- incident created → notify affected client contacts according to policy
- recurring support request pattern → suggest project/problem record
- support entitlement expires soon → renewal workflow

## API/MCP
API exposes support summaries, mappings, entitlements, incidents, and provider-neutral conversation references. Chatwoot message APIs are not re-exposed wholesale.

MCP candidates: get_support_summary, list_active_incidents, get_incident, search_support_references, find_chatwoot_conversation, get_support_entitlement. AI tools must not invoke Chatwoot AI or expose hidden support content outside caller permissions.

## PWA/mobile
Support summary, incidents, client/property context, deep links, status updates, and escalation actions must work well on mobile. Chatwoot widget/linked experience must remain usable in installed PWA mode.

## Acceptance criteria
- no duplicate internal message store is created
- Chatwoot remains conversation truth
- property/client context is safe and minimal
- one client's support data cannot leak to another
- connector downtime produces clear degraded state rather than false zero counts
- Chatwoot AI remains architecturally separate from Re:Solve AI

## Lovable build slices
1. support overview using demo connector data
2. organisation/property/inbox mappings
3. conversation reference views + deep links
4. support plans/entitlements
5. incidents + monitoring links
6. webhooks, health, analytics, portal support summary
