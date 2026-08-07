# Client Portal Home

## Purpose
Client Portal Home is the client's calm operating summary. Within seconds it should answer: what needs my action, what is happening with my Projects/Properties/Services, what do I owe, what is changing, and where do I go next?

It is not a mirror of Admin Dashboard. It consumes client-safe Attention and domain projections while hiding internal implementation/risk detail.

## Core flow
1. Client User signs in.
2. Portal resolves Membership plus Organisation/Property/record grants.
3. client-safe Attention renders first.
4. current Projects, Property Posture, Support, Billing/Renewals and recent meaningful Activity follow according to role.
5. user takes one obvious action or opens a focused workspace.
6. source record/Attention updates; Notification read state remains separate.

## Shell relationship
Global Portal navigation, Notifications and Account live in the Portal shell. Support access is globally reachable.

Optional Portal Àríyá, if enabled later, uses the same stable shell/command entry philosophy and must not crowd Home.

## 1. Requires Your Attention
Backed by the shared Attention Engine using a client-safe projection.

Examples:
- Approval requested;
- Client Action overdue;
- Request needs clarification;
- Invoice/deposit due;
- Contract/Proposal action;
- Domain/Hosting renewal decision/payment;
- requested File upload;
- active Incident/maintenance action;
- permitted Vault Access request/action.

Each item has plain-language reason, source/context, due/status, one primary registered action and deep link.

Internal risk scores, staff-only notes and hidden source evidence never leak.

## 2. Current Work
Visible active Projects and relevant Requests/Client Actions.

Project summary:
- name/status;
- progress/milestone state;
- next milestone;
- next client action/Approval;
- latest client-visible update.

Do not expose internal Tasks/Notes/Risks/Budgets unless explicitly client-visible.

## 3. Properties
Show permitted Properties with client-safe **Property Posture**, not raw provider dashboards.

Summary may include:
- name/type;
- lifecycle status;
- Posture: healthy/attention/degraded/maintenance/unknown;
- client-safe reason/last updated;
- active Incident/Maintenance;
- upcoming Renewal Obligation;
- related Project/Service.

Provider names such as Cloudflare/Uptime Kuma are normally hidden unless useful. Client should understand the Property, not Re:Solve's monitoring implementation.

## 4. Support
Chatwoot remains support engine.

Home may show:
- entitlement/availability;
- active Incident;
- safe open/waiting conversation count/references;
- escalation route;
- Start/Open Support action.

Do not reproduce full conversation streams.

## 5. Billing & Renewals
Permission-gated.

May show:
- currently due/overdue;
- next Invoice/payment milestone;
- recent verified Payment/Receipt;
- Account Statement shortcut;
- active Client Service renewal;
- Domain/Hosting/other Renewal requiring client decision/payment.

No Client Service Consumption/remaining-hours/credits.

If user lacks Billing permission, financial content is omitted entirely rather than leaking counts.

## 6. Approvals / Documents / Files
Recent/relevant:
- Deliverable awaiting review;
- Proposal/Estimate/Contract action;
- requested File;
- client-visible report/document;
- Receipt;
- authorized protected Vault item/action.

Protected Vault content is a separate secure experience and is never an ordinary File preview/cache.

## 7. Recent Activity
Client-safe meaningful chronology:
- Milestone/Deliverable;
- Request update;
- Approval;
- Invoice/Payment/Receipt;
- Proposal/Contract outcome;
- Property recovery/Maintenance;
- Renewal completion;
- File shared;
- client-visible Comment/update.

No internal Notes, connector logs, Audit details, AI internals or hidden finances.

## 8. Upcoming
Compact agenda may include:
- Project Milestones;
- Approvals/Client Actions;
- Renewals;
- Maintenance;
- Invoices/payment schedule;
- Booking/meeting.

## Àríyá optional client briefing
If Portal Àríyá is enabled, it can provide a narrow evidence-backed summary such as:
- `What do I need to do?`
- `Summarize my website project.`
- `Why is this Property marked Attention?`
- `Explain this Invoice.`

It sees only client-safe permitted projections and cannot expose staff/internal/Vault-secret context.

## First-use / onboarding state
A new client sees:
- welcome/Operating Entity Brand;
- Organisation details;
- onboarding actions/Requests;
- support access;
- invited team/access status where authorized;
- explanation of what will appear later.

No fake charts/sample records.

## Role shaping
### Organisation Admin
Broader Organisation/member/access/Property overview.

### Billing Contact
Finance/Renewals promoted.

### Approver
Approvals/Documents promoted.

### Property Manager / Technical Contact
Property Posture, Renewal, Incidents, Requests and Support promoted.

### Project Collaborator
Current Work/Files/Approvals promoted.

Combined responsibilities are ranked without duplicate sections.

## Notifications / WhatsApp
Home surfaces current Attention; full history/preferences remain Notifications.

Permitted client events can deliver via in-app, push, email or WhatsApp/Baileys according to policy. WhatsApp remains operational Re:Solve-to-client communication, not end-customer support.

## Requests
When enabled, Home may provide a simple `New Request` Action and show clarification/status for current Requests rather than forcing every ask into Chatwoot or Project work immediately.

## API / MCP
Portal APIs return client-safe projections, not unrestricted Admin payloads.

Potential resources:
- home summary;
- client Attention;
- visible Projects/Requests;
- visible Property Posture/Renewals;
- Billing summary where permitted;
- client-safe Activity;
- Support summary.

Client-facing MCP/agent access, if enabled later, uses separate scoped Client Principals/tools.

## Plugins
Portal Home contributions are explicitly portal-safe, scoped, responsive, bounded and configurable. A Plugin cannot add a competing navigation/dashboard framework.

## Responsive/PWA
Portal mobile is primary quality target.

Phone priority:
1. Requires Your Attention;
2. Support / New Request shortcuts;
3. Current Work;
4. Properties/Posture;
5. Billing/Renewals if permitted;
6. Documents/Files/Activity/Upcoming.

Use Core UI components and deliberate mobile nav. Safe cached summaries show last refresh; payment/Approval/high-risk actions require connectivity unless specifically designed replay-safe. Vault content never offline caches.

## Accessibility
Plain language, non-color-only priority/status, semantic status summaries, keyboard desktop use and generous touch targets.

## Acceptance criteria
- client sees outstanding actions within seconds;
- Home uses client-safe Attention rather than Notification unread count as priority;
- Property Posture/Renewals are understandable without provider jargon;
- Chatwoot remains Support engine;
- unauthorized Billing/Property/Project data disappears without leakage;
- optional Àríyá remains strictly client scoped;
- mobile is first-class;
- stale/offline state is truthful;
- no Client Service Consumption/Timesheet/HR concept appears.

## Demo data
Use fictional Westbridge University context with different client roles, several Properties, active Project, pending Approval/Request, upcoming Domain renewal, active Support/Incident summary, role-gated Invoice, recent Deliverable/Receipt and realistic healthy/quiet state.

## Lovable build slices
1. Portal Home first-use/loading/empty shell content after Portal shell exists.
2. client-safe Attention.
3. Current Work / Requests.
4. Properties/Posture/Renewals.
5. Support/Chatwoot launch.
6. role-gated Billing/Documents.
7. Activity/Upcoming.
8. role-prioritization + optional Àríyá later.
9. mobile/PWA/offline polish.
