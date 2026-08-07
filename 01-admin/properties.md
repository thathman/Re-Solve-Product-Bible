# Properties

## Purpose
Properties are a central native object in Re:Solve. A Property represents a digital or operational asset that an Organisation owns, operates, publishes, hosts, manages or receives service for.

Properties prevent Domains, Websites, Journals, hosting, servers, stores and applications from becoming disconnected records scattered across modules.

A Property is the context anchor for Projects, Requests, Support, Vault, native Monitoring, Property Posture, Renewals, Files, Knowledge, Services, Automations, Connectors and client access.

## Examples
- Website
- Journal / publication
- OJS installation
- WordPress site
- WooCommerce store
- Domain
- Hosting account
- Server
- application/service endpoint
- other managed asset

## Hierarchy and relationships
Properties may use parent/child hierarchy plus typed relationships.

Example:
```text
Westbridge University
├── Main Website
├── WBU Journals
│   ├── Westbridge Journal of Social Research
│   └── Westbridge Business Review
├── westbridge.example Domain
└── Primary Hosting
```

Rules:
- hierarchy is explicit;
- circular relationships are prohibited;
- descendant access may inherit only when policy allows;
- child Properties can override service, monitoring, connector and access configuration;
- moving hierarchy/relationship is audited;
- typed relationships such as hosted-on/domain-for/depends-on remain distinguishable from parent-child.

## Property types
Configurable type definitions may declare icon, descriptive/custom fields, permitted child/relationship types, relevant Connector capabilities, Posture evidence categories, default tabs and Service applicability.

Core ships useful examples but does not hard-code every future type.

## Property List
Use the canonical Re:Solve DataTable/Saved View patterns.

Columns may include:
- Property/reference;
- Organisation;
- type;
- parent;
- lifecycle status;
- Property Posture;
- owner/team;
- primary URL/identifier;
- next Renewal/Expiry obligation;
- last monitoring evidence/freshness;
- Connector state;
- active Project/Request count;
- Support/Incident state.

Curated views:
- All Properties
- Needs Attention
- Degraded/Critical
- Renewals Soon
- Maintenance
- Unknown/Stale Monitoring
- Archived
- personal/team Saved Views

Website/Journal/Domain/Hosting/etc. are normally filters/saved views rather than permanent root navigation.

## Property Workspace

### RecordHeader
Shows name, human reference, type, Organisation, hierarchy/context, lifecycle status, Posture, owner/team, primary identifier and primary/overflow actions.

Registered actions may include:
- edit;
- create child/relationship;
- start Project;
- create Request;
- attach Client Service;
- configure native Monitor;
- connect external provider;
- add Renewal Obligation;
- schedule Maintenance;
- open Support context;
- create/share authorized Vault Item.

### Overview
Answer:
1. What is this Property?
2. Is it operationally healthy?
3. Why is the current Posture what it is?
4. What work/services/renewals/incidents need attention?
5. Who is responsible?

Sections may include:
- identity/context;
- Property Posture reasons;
- Attention;
- active Client Services;
- active Projects/Requests;
- Incidents/Maintenance;
- upcoming Renewal Obligations;
- Connector summary/freshness;
- Support summary;
- recent Collaboration/Activity;
- Files/Vault metadata;
- Knowledge.

## Details
Type-specific native/custom metadata.

Examples:
### Website
URL, platform/CMS, environment, repository reference, related Domain/Hosting.

### Journal
Title, acronym, ISSN, OJS/application relationship, public URL and approved editorial/technical metadata.

### Domain
Domain name, registrar source, DNS provider, registration/expiry evidence, auto-renew state and related Website/Hosting.

Provider-specific identifiers live in Connector Mappings rather than polluting core identity.

## Property Posture
Property Posture replaces vague generic `health` as the richer operational state.

Suggested states:
- HEALTHY
- ATTENTION
- DEGRADED
- CRITICAL
- MAINTENANCE
- UNKNOWN

It is derived and explainable from evidence such as:
- native HTTP/HTTPS/latency checks;
- SSL/certificate state;
- Domain registration/expiry;
- DNS/hosting evidence;
- heartbeat/backup freshness;
- WordPress/OJS/application status;
- active Incident;
- Maintenance;
- Renewal state;
- Connector freshness.

Every material reason shows source and freshness. Connector outage alone does not mean the Property itself is down.

## Lifecycle status vs Posture
Lifecycle status may include Onboarding, Active, Paused, Retired and Archived.

Posture describes current operational condition. Never conflate them.

## Native Monitoring
Properties can own native Re:Solve Monitor definitions. Initial common checks include HTTP/HTTPS, expected status, latency and certificate/domain expiry evidence; later DNS/TCP/content/heartbeat/backup checks.

The architecture supports separately deployable Monitoring Workers/Probes.

## External monitoring / Cloudflare
External sources are optional connectors.

Cloudflare can contribute domain/DNS/registrar/edge/health evidence where configured.
Uptime Kuma may contribute Monitoring signals for deployments already using it, but is never a required dependency.

## Renewal / Expiry Obligations
A Property can have one or more obligations for Domain, Hosting, Certificate, license, maintenance/service dependency or another managed item.

Each obligation records source, expiry, auto-renew state, owner, client responsibility, related Service/Contract/Billing, reminder/approval/payment state and verification evidence.

Renewal workflow is surfaced in Property and the cross-client Renewal Desk.

## Incidents and Maintenance
Incidents relate one/more Properties and retain source signals, client impact, timeline and resolution.
Maintenance windows intentionally annotate/suppress monitoring according to policy.

## Requests
Property-scoped Requests provide a structured route for change/access/maintenance/service asks before they become Tasks, Projects, Support or commercial work.

## Services
Show current Client Services, scope, renewal, Support Entitlement and linked commercial records. Do not show hours/credits consumed because Client Service Consumption is out of scope.

## Projects
Show linked active/completed Projects and relevant current blockers/deliverables.

## Support
Show provider-neutral Chatwoot-backed Support context: entitlement, safe conversation references, Incidents and escalation. Full messaging remains in Chatwoot.

## Vault and Files
Vault shows only protected metadata/actions authorized for the Property.
Files shows ordinary non-confidential content.

A protected confidential document must not remain accessible through a parallel ordinary File path.

## Knowledge
Property-scoped internal/client-safe Re:Solve Knowledge.

## Connectors and provenance
Show Connector Instances/Mappings plus authority/freshness. Provider records do not become canonical Property identity.

## Collaboration / Activity
Use the shared Comments/Mentions/Following model plus user-readable Activity. Audit remains separate.

## Access and client visibility
Property access grants are independently enforceable and may inherit to descendants where explicitly configured.

Portal visibility options may include hidden, summary-only, normal and explicit-grant-only.

Hidden data cannot leak through Search, counts, Attention, Notifications, API, MCP or Àríyá.

## Attention
Examples:
- Posture degraded/critical;
- Domain/Hosting/Certificate renewal due;
- backup heartbeat stale;
- Incident unresolved;
- Monitoring source unknown/stale;
- required client decision/request waiting;
- Connector authentication affects management capability.

## Notifications
Meaningful state transitions such as confirmed outage/recovery, renewal threshold, Maintenance and critical Connector/credential issues. Do not emit a client notification for every raw monitor sample.

## Automations
Examples:
- qualifying failure -> create/link Incident;
- expiry threshold -> Renewal Attention/Request;
- recovery -> resolve relevant Attention/update Incident;
- Maintenance window -> suppress/annotate checks;
- client decision due -> Portal Request/notification;
- Connector state change -> data-freshness Attention.

## API / MCP / Àríyá
First-class APIs expose Property, hierarchy/relationships, Posture, Renewal summaries, native monitoring configuration where permitted, Services, Projects, Requests, Access, Connector mappings and Activity.

Ordinary Property APIs never expose Vault secret values.

MCP candidates:
- search_properties
- get_property
- get_property_posture
- list_property_children
- list_expiring_properties
- list_property_services
- get_property_support_summary
- list_property_attention

Àríyá can explain Posture from evidence/freshness and propose registered actions.

## Plugins
Plugins may contribute Property Types, fields, tabs, Posture signal providers, Actions, Reports, Automation and MCP contributions through approved Core UI/extension contracts.

## Security
- cross-Organisation access denied;
- descendant inheritance inspectable;
- sensitive technical metadata can require stronger capability;
- Vault remains separate;
- dangerous Connector-backed Property actions route through Action Registry and may require confirmation/step-up/Approval.

## Responsive/PWA
Phone priority:
- identity/status;
- Posture/Attention;
- Incidents/Renewals;
- active work/Requests;
- Services/Support;
- Activity.

Hierarchy uses drill-down rather than cramped trees. Cached summaries show refresh timestamp; credentials and high-impact actions remain online-only according to policy.

## Acceptance criteria
- hierarchy/typed relationships are safe and explainable;
- Posture is explainable and distinct from lifecycle status;
- native monitoring can exist without Uptime Kuma;
- Renewal is workflow, not a date badge;
- Cloudflare/external data exposes provenance/freshness;
- client visibility/access are separately controlled;
- Vault cannot leak through Property responses/caches;
- no Client Service Consumption or Timesheet behavior appears.

## Lovable build slices
1. Property list + Saved Views + fictional demo hierarchy.
2. Create/edit + type/relationship handling.
3. Property Overview + RecordHeader.
4. hierarchy/relationship UX.
5. Services/Projects/Requests/Support panels.
6. Property Posture with demo/native signals.
7. Renewals/Incidents/Maintenance.
8. Access/Portal visibility.
9. Connector/provenance + Vault/File metadata.
10. real native Monitor execution + Cloudflare/external sources later.
