# Admin Dashboard

## Purpose
The Admin Dashboard is Re:Solve's operational command surface. Within seconds it should answer: what needs attention, what changed, what is blocked, what is due, what is at risk, and what should happen next.

It is not a KPI wall and it is not a navigation replacement. It consumes the shared Attention Engine, My Work and domain summaries instead of recreating separate risk logic.

## Core flow
1. User enters Admin.
2. System resolves Principal/User permissions, scopes, Saved Views/preferences and current Attention.
3. Deterministic attention/work state renders first.
4. Àríyá may synthesize an operational briefing from the same permitted evidence.
5. User opens source context or executes a registered action.
6. Source-record changes resolve/update Attention and Notifications naturally.

## Header / shell relationship
Global Search/Command, Quick Create, Àríyá, Notifications and Account belong to the shared TopBar rather than being reimplemented in Dashboard content.

Dashboard content begins below the shell with a compact context/title and role-appropriate briefing/attention.

## 1. Àríyá Operational Briefing
A compact synthesis of current permitted evidence.

Examples:
- two client actions are blocking delivery;
- three Renewal Obligations require decisions this month;
- one Property is degraded and an Incident is active;
- four Invoices are overdue;
- one Connector authentication problem is making data stale.

Rules:
- source evidence/deep links visible;
- freshness shown where material;
- deterministic Dashboard still works if Àríyá/provider is unavailable;
- AI inference is visually distinguishable from system fact;
- no generic chat hero occupies the page.

## 2. Attention Queue
Primary Dashboard element backed by `03-platform/attention-engine.md`.

Each item may show:
- priority;
- concise reason;
- Organisation/Property/Project context;
- age/due threshold;
- owner/assignee;
- source evidence/freshness;
- primary registered action;
- deep link.

Examples:
- approval waiting;
- Domain Renewal in seven days;
- Invoice overdue;
- onboarding blocked;
- confirmed outage;
- stale backup heartbeat;
- Connector authentication failed;
- Vault access request waiting;
- Proposal expiring.

Controls may include mine/team/all-permitted scope, acknowledge, snooze, assign where allowed and open source. Manual UI dismissal cannot falsely resolve an underlying business condition.

## 3. My Work
Compact personal responsibility summary:
- Tasks due/overdue;
- Approvals;
- Requests assigned;
- Reminders;
- Mentions;
- Renewals assigned;
- Client Actions requiring coordination;
- recent reassignment.

Do not add Timesheet/Time Tracking or employee workload/utilization features.

## 4. Client / Relationship Pulse
Show exceptions and meaningful state from Client Success:
- clients At Risk / needing attention;
- onboarding blockers;
- renewals without action;
- major Project/Property/Support/Billing concerns;
- relationship reviews due.

Client Health must remain explainable.

## 5. Project & Delivery Pulse
Show:
- active/at-risk Projects;
- milestones due soon;
- blocked Deliverables/Tasks;
- Client Actions outstanding;
- approvals/Change Requests waiting.

No staff utilization/Timesheet charts.

## 6. Property Posture & Renewals
Prioritize:
- degraded/critical/unknown Properties;
- active Incidents;
- Domain/Hosting/SSL Renewal Obligations;
- stale heartbeat/backup evidence;
- Maintenance;
- native Monitoring/Connector source problems affecting confidence.

Healthy Properties should not dominate.

## 7. Finance Pulse
Role-gated:
- overdue receivables;
- due soon;
- unmatched/failed Payments;
- deposits/payment milestones due;
- recent verified Payments;
- credit-control Attention;
- recurring Billing generation issues.

## 8. Support Pulse
Provider-neutral Chatwoot context only:
- urgent/escalated conversation references;
- SLA/entitlement risk;
- active Incidents;
- Support Connector degradation.

Do not mirror every Chatwoot message.

## 9. Requests / Commercial Pulse
When relevant:
- new Requests awaiting triage;
- Proposals/Estimates expiring;
- Contracts awaiting signature;
- Renewal Opportunities;
- stale Opportunities requiring follow-up.

## 10. Meaningful Activity
Recent permitted user-readable events such as Project milestone, Payment, Proposal acceptance, Property recovery, Vault share, Portal access change or Connector recovery.

Activity is not Audit and should not become an endless low-value CRUD feed.

## 11. Platform Health
Authorized administrators only:
- failing Connectors;
- stale integrations;
- dead-letter/event backlog;
- Automation/job failure;
- native Monitoring Worker/Probe problem;
- notification delivery degradation;
- Plugin health/update issue;
- backup/system issue.

## Customization
Users may reorder/collapse approved secondary sections, choose mine/team/permitted scope, and save relevant view preferences.

Mandatory critical Attention cannot be hidden through personalization.

## Quick actions
Dashboard may surface registered contextual Actions, but the global Quick Create remains part of TopBar.

Examples:
- create Request;
- create Project/Task;
- create Opportunity;
- draft Invoice;
- schedule Reminder;
- acknowledge Incident;
- open Renewal action.

## Responsive/PWA
### Desktop
Dense but calm operational composition. Do not default to a uniform card grid.

### Tablet
Attention/Briefing/My Work remain dominant; supporting domains adapt below/alongside.

### Phone
Priority feed:
1. Àríyá/deterministic briefing;
2. Attention;
3. My Work;
4. critical Property/Finance/Project/Support/Request state;
5. meaningful Activity.

No crushed desktop tables/charts.

### Offline/stale
Safe cached summary may display with clear timestamp/stale label. High-impact writes remain online-only unless explicitly replay-safe. No Vault secrets cached.

## Permissions
All aggregates/counts are permission filtered server-side. A hidden record cannot leak through a count, brief, Attention item or Àríyá summary.

Representative capabilities may include `dashboard.view`, `dashboard.team_scope`, `dashboard.workspace_scope`, `billing.summary.read`, `system.health.read` and `support.summary.read`.

## Notifications relationship
Dashboard does not consume unread Notifications as a substitute for Attention. An unresolved source condition may appear in Attention even after its Notification was read.

## API / MCP / Àríyá
Expose composable provider-neutral primitives such as summary, Attention, My Work, domain exception summaries and Activity rather than one opaque UI blob.

MCP candidates:
- get_daily_briefing
- get_attention_summary
- get_my_work
- get_client_risks
- get_property_posture_exceptions
- get_finance_exceptions
- get_upcoming_renewals

## Plugins
Plugins may contribute approved Attention providers, secondary dashboard modules, actions and Activity renderers through Core UI contracts. They cannot turn Dashboard into an uncontrolled widget marketplace.

## Analytics
Measure product usefulness such as Attention resolution path, drill-down/registered-action usage and noisy/ignored areas—not engagement vanity metrics.

## Empty state
Healthy workspace should feel calm:
- `No urgent attention required`;
- upcoming work/renewals;
- recent meaningful Activity;
- no fake KPIs.

## Acceptance criteria
- top actionable items are obvious without module hopping;
- Dashboard consumes shared Attention rather than duplicate logic;
- Àríyá failure does not break deterministic state;
- every material fact is inspectable/source-linked;
- hidden data cannot leak through summaries;
- mobile preserves priority;
- no Timesheet/HR/utilization surface is introduced;
- design uses the Core UI Framework and Tremor influence selectively rather than generic cards/charts.

## Lovable build slices
1. Dashboard layout with deterministic fictional Attention/My Work demo data.
2. Attention Queue interactions.
3. My Work/Client/Project/Property exception summaries.
4. Finance/Support/Requests/Commercial summaries with permissions.
5. Activity + platform-health sections.
6. responsive/PWA/customization polish.
7. Àríyá briefing after deterministic source contracts are stable.
