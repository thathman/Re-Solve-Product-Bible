# Support Operations & Chatwoot

## Purpose
Support in Re:Solve is the operational/context layer around Chatwoot-managed client support. Re:Solve must not rebuild Chatwoot's helpdesk, conversation/message engine, web chat, support Knowledge, agent/team routing or Captain.

## Ownership boundary
Chatwoot owns:
- inboxes/channels;
- customer conversations/messages;
- support attachments;
- agent/team assignment;
- conversation status/routing;
- web chat widgets;
- Support Knowledge;
- CSAT/native support analytics;
- Captain.

Re:Solve owns:
- Organisations/Contacts;
- Properties;
- Client Services/Support Entitlements;
- safe support mappings/references/summaries;
- Incidents/operational escalation;
- related Projects/Requests/Billing/Renewals/Property context;
- Connector health/freshness;
- selected cross-domain reporting;
- client access/visibility.

## Support versus Requests
A Request is a structured Re:Solve business/operational ask that may need triage into a Project, Task, Approval, commercial flow or Support.

Chatwoot Support is for actual support conversation handling.

Examples:
- `Website is down` -> Support/Incident context is likely appropriate.
- `Please add a new journal next quarter` -> Request/Opportunity/Project path.
- `Change our Billing Contact` -> Request/Organisation workflow.

A Request may create/link a Chatwoot conversation when support is the appropriate channel, but the two records remain distinct and traceable.

## Support overview
Prioritize:
- open/waiting/urgent safe conversation counts by Organisation/Property;
- SLA risk/breach where provider data permits;
- active Incidents;
- client/Property support health;
- Support Entitlement mismatch/expiry;
- recent high-priority references;
- Chatwoot Connector health/freshness;
- support items that should become Request/Task/Project/Incident;
- repeated patterns needing Knowledge/Problem work.

Do not mirror every message into Re:Solve.

## Conversation references
Store durable mappings/references/snapshots only, such as Organisation, Contact, Property, Chatwoot inbox/conversation id, status/priority/category snapshot, assigned agent/team reference, first/last activity, entitlement, linked Incident/Project/Request and last sync.

`status snapshot` is derived/provider-sourced and shows freshness; it is not a second authoritative conversation record.

## Property context
Managed support handoff should attempt to identify safe:
- Organisation;
- Property;
- Property Type;
- source domain/path;
- authenticated client User context when available;
- support category;
- application type.

Never send passwords, session tokens, secrets, Vault content or unnecessary PII to Chatwoot.

## Chatwoot Connector
Capabilities may include:
- Contact/account mapping;
- inbox mapping;
- conversation summary/reference retrieval;
- open/unread counts;
- safe custom context;
- labels/team assignment where explicitly authorized;
- health/freshness;
- webhook ingestion;
- deep link;
- property-support configuration where policy allows.

Connector sync declares Chatwoot authority for conversation state and conflict/freshness policy.

## Inbox model
Default may use an Organisation/client-family inbox with Property context on conversations rather than creating an inbox for every Property. Genuine isolation/brand requirements can justify separate inboxes.

Operating Entities/Brands may map to their own support identities/inboxes.

## Support Entitlements
May define:
- covered Properties/Services;
- support hours/business hours as availability windows, not consumption tracking;
- response targets;
- channels;
- categories/exclusions;
- escalation rules;
- authorized client Contacts.

**Do not track Client Service Consumption/remaining support hours/credits.**

Entitlement supplies commercial/operational context and does not replace Chatwoot's own SLA/conversation mechanics.

## Incidents
Incident is a Re:Solve operational record related to Properties, Monitoring Signals, Chatwoot references, Projects/Tasks/Requests, client updates and resolution/postmortem.

Lifecycle: Investigating -> Identified -> Monitoring -> Resolved -> optional Postmortem/Closed.

Severity is separate from Chatwoot conversation priority.

## Client Portal Support
Show:
- Start/Open Support;
- recent permitted conversation references/counts;
- Support Entitlement summary;
- active Incidents/service status;
- escalation route;
- relevant Requests if product flow links them.

The Chatwoot widget/deep-linked experience provides messaging.

## WhatsApp distinction
WhatsApp/Baileys is Re:Solve-to-client operational communication for Project/Request status, Reminders, Approvals, Billing, Renewals, Property alerts and direct operational updates. It is not the client-customer support inbox.

## Attention
Examples:
- urgent Support escalation requiring Account/Technical action;
- SLA/entitlement mismatch requiring intervention;
- active Incident;
- Connector stale/auth failure;
- recurring support pattern requiring Project/Request/Knowledge action.

Attention represents ongoing condition; Notifications deliver awareness.

## Permissions
Canonical examples:
- `support.read`
- `support.analytics.read`
- `support.context.manage`
- `support.entitlements.manage`
- `support.mappings.manage`
- `incidents.read`
- `incidents.manage`
- `connectors.configure` for Connector administration.

Access still respects Organisation/Property scope and provider mapping visibility.

## Notifications
Surface meaningful events only: urgent escalation, SLA risk, Incident created/update/resolved, support item requiring operational action, Connector failure and entitlement mismatch/renewal.

Do not notify Re:Solve Users on every Chatwoot message.

## Automations
Examples:
- confirmed monitoring outage -> create/link Incident;
- urgent support reference -> Attention/notify Account/Technical owner;
- Incident created -> client-safe update policy;
- repeated support category -> suggest Request/Project/Knowledge;
- Support Entitlement renewal -> Renewal workflow.

## API / MCP / Àríyá
Expose provider-neutral support summaries, mappings, entitlements, Incidents and safe conversation references.

Do not wholesale proxy Chatwoot's message API.

MCP candidates:
- get_support_summary
- list_active_incidents
- get_incident
- search_support_references
- find_chatwoot_conversation
- get_support_entitlement

Àríyá may summarize authorized operational Support context and source freshness. It does not invoke Chatwoot Captain as if Captain were Re:Solve AI.

## Reports
Cross-domain reporting can combine Support context with Organisation/Property/Service/Incident data while avoiding employee-agent productivity/HR scoring and Client Service Consumption.

## PWA/mobile
Support summary, Incident, entitlement/context, deep links and escalation/actions work well on phone. Chatwoot linked/widget experience remains usable in installed PWA mode.

## Acceptance criteria
- Chatwoot remains conversation/message truth;
- Requests and Support are distinct but linkable;
- no duplicate internal message store;
- client/Property context is safe/minimized;
- one client's Support data cannot leak;
- Connector downtime produces stale/degraded state rather than false zero;
- Captain remains separate from Àríyá;
- no Client Service Consumption/Timesheet/HR behavior appears.

## Lovable build slices
1. Support overview using fictional Connector data.
2. Organisation/Property/inbox mappings + provenance.
3. conversation reference views/deep links.
4. Support Entitlements.
5. Incidents + native Monitoring links.
6. Request/Project/Knowledge triage links.
7. webhooks/health/analytics/Portal Support summary.
