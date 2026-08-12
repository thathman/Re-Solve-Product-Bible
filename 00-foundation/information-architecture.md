# Re:Solve Information Architecture

## Purpose
This document defines the complete Re:Solve surface hierarchy while keeping daily navigation simple. It is product architecture, not build order.

## Product surfaces
1. **Admin OS** — staff-facing operations.
2. **Client Portal** — client-facing collaboration/self-service.
3. **Secure External Access** — narrow guest actions, Forms and commercial documents before/without Portal membership.
4. **Public/API surface**.
5. **MCP surface**.
6. **Plugin extension surface**.
7. **Connector surface**.

A public-site/headless CMS is a distant-future expansion and is not part of the current run.

## Navigation rule
The product may contain many capabilities without exposing them all as root navigation. Admin navigation is shallow, business-readable and task-oriented. Do not use app-launcher grids, icon-only root navigation or deep permanent trees.

Ariya is persistent global/contextual intelligence, not an ordinary module that users must visit to benefit from it.

## Admin OS — recommended primary navigation

```text
Home
Tasks
Clients
CRM
Sales
Delivery
Support
Billing
Forms
Calendar
Information
Reports
Automations
Settings
```

Capabilities such as Properties, Monitoring, Renewals, Files, Knowledge, Vault, Connectors, Plugins, Audit and System Operations appear as strong destinations inside the relevant group and through Search/Command/Quick Create/Saved Views without forcing dozens of permanent root rows.

Module visibility can be configured by deployment/role so breadth does not become clutter. Hiding a module never changes authorization.

Global chrome provides Search/Command, Quick Create, Notifications, connection state, Account and Ariya.

## Home
Role-aware operational summary focused on decisions, not interchangeable KPI cards:
- Ariya briefing;
- Needs Attention;
- Tasks due/overdue/waiting;
- client health;
- project/delivery state;
- Property Health/incidents/renewals;
- receivables/commercial state;
- Support state;
- important recent activity;
- quick actions.

Dashboards may be configurable within governed widgets/layouts and role/module visibility.

## Tasks
Tasks is the canonical staff execution center. It replaces the former `My Work` terminology.

Views may include:
- Assigned to me;
- Focus;
- Today;
- Overdue;
- Upcoming;
- Waiting on client;
- Approvals;
- Requests;
- Renewals;
- Mentions;
- Reminders;
- Ariya-created/proposed where policy permits;
- Property-health work;
- Calendar/agenda.

Every projected item deep-links to authoritative source truth. Re:Solve has no timesheets/work timers.

## Clients
Clients is the post-sale relationship area.

Views may include Organisations, Contacts, Client Health, Onboarding, Renewals, Relationship Reviews, Portal Access, Active Services and Former Clients.

Organisation 360 may include Overview, Contacts/Memberships, Account Team, Properties, Services, Opportunities, Proposals, Contracts, Projects, Billing, Support, Forms, Files, Communications, Notes, Activity, Audit, Portal Access and Connector mappings.

## CRM
CRM covers acquisition and relationship development.

Views:
- Leads;
- Opportunities;
- Pipeline;
- Organisations/Contacts;
- Activities/Cadences;
- Communications/Inbox Triage;
- Segments;
- Imports;
- Forecast.

Lead conversion preserves/deduplicates Organisation and Contact identity.

## Sales
Sales owns the commercial commitment path.

Views:
- Opportunities/Pipeline shortcuts;
- **Proposals**;
- Service Catalogue;
- Price Books / Rate Cards;
- Service Packages;
- Contracts;
- Recurring Arrangements / Client Services;
- commercial Templates/Document Studio entry;
- Sales Activity/Cadences;
- Forecast/Goals.

There are no separate Quote or Estimate modules. Proposal is the canonical offer record with detailed, quote-style or estimate-style presentation.

Commercial chain:
`Lead -> Organisation/Contact -> Opportunity -> Discovery/Form -> Proposal -> Acceptance -> Portal Invitation -> Contract/Onboarding -> Project/Delivery -> Invoice/Adjustments -> Payment -> Renewal/Review`.

## Delivery
Delivery contains the work required to fulfil commitments.

Primary areas:
- Projects;
- Project Templates;
- Milestones/Deliverables;
- Tasks;
- Approvals;
- Requests/Change Requests;
- Renewals;
- Client Actions;
- risks/issues.

Project workspace may include Overview, Milestones, Tasks, Deliverables, Approvals, Requests, Risks/Issues, Properties, Forms, Files, Communications, Notes, commercial/Billing context, Expenses, client visibility and Automation history.

## Properties and Monitoring
Properties remains a first-class operational asset domain even when grouped under Clients/Delivery/Operations in navigation.

Property workspace may include Overview, hierarchy/relationships, Health/Posture, monitors, incidents, renewals/expiry, maintenance, Projects, Services, Support, Requests, Vault, Files, Knowledge, Communications, connector mappings and plugin tabs.

Monitoring views may include Properties, Native Monitors, Incidents, Domains/SSL, Backups/Heartbeats, Performance, Maintenance, alert rules, Worker/Probe health and external sources.

Ariya continuously consumes authorised Property Health evidence and may Watch/Investigate/Recommend or create controlled work through policy.

## Support
Support is Re:Solve operational case/context plus the Chatwoot human-conversation bridge.

Portal live chat architecture is `Portal -> Ariya -> Chatwoot -> Ariya -> Client`. Re:Solve does not build a second live-chat console.

Views may include Support overview/cases, Clients, Properties, Incidents, Entitlements/SLA context, Support Health, analytics and Chatwoot references/handoff.

## Billing
Views may include:
- Overview;
- Invoices;
- Payments;
- Receipts;
- Credit Notes;
- Adjustments;
- Refunds;
- Recurring Billing/Arrangements;
- Deposits/Payment Schedules;
- Reconciliation;
- Account Statements;
- Credit Control;
- Expenses/Spend where enabled.

Payment remains transaction evidence. Discounts/late fees/penalties/credits/write-offs are pricing or controlled Adjustment/Credit records, never hidden Payment mutations.

## Forms
Forms is a first-class shared workspace because it powers discovery, project questionnaires, onboarding, surveys, review requests, intake, Requests and structured internal/client submissions.

Views:
- Forms/Templates;
- Form Requests/Assignments;
- Responses/Submissions;
- Review/Triage;
- Routing/Automations;
- Review Requests/Feedback where enabled.

## Calendar
Unified business calendar/agenda may aggregate Tasks, meetings/bookings, Milestones, Reminders, Renewals, Contract expiries, Invoice due dates, maintenance and scheduled Automations. No employee shift/attendance scheduling.

## Information
Grouped information capabilities may include:
- Files;
- File Requests;
- Knowledge;
- Vault;
- internal Notes/Comments/Mentions;
- recent/favorites/saved views.

## Communications
Communications is contextual across Client/CRM/Project/Billing/Support records and may also expose a Shared Inbox/Inbox Triage workspace.

It covers inbound/outbound email, connected mailboxes, delivery evidence, record-linked communication history, review requests, operational announcements and configured non-support channels.

Chatwoot remains the live-chat/human handoff transport for Portal Support.

## Reports
Reports may cover Clients, CRM/Sales, Projects, Finance, Support, Properties/Monitoring/Renewals, Services, Ariya usage and custom/scheduled reports. Money remains currency-aware; unlike currencies are never silently aggregated.

## Automations
Views:
- Workflows;
- Recipes/Templates;
- Runs;
- Scheduled Jobs;
- Failures/Retry;
- Event Explorer;
- Action Catalogue.

## Settings
Top-level groups are searchable and domain-owned:
- General / Workspace;
- Operating Entities & Brands;
- People & Access;
- Client Portal;
- CRM / Clients;
- Properties / Monitoring / Renewals;
- Projects / Tasks / Delivery;
- Sales / Service Catalogue / Proposals / Contracts;
- Billing / Spend / Adjustments;
- Forms / Requests / Reviews;
- Communications / Email / Templates;
- Documents / PDF Signatures;
- Notifications;
- Ariya / AI;
- Files / Vault;
- Automations;
- Data / Custom Fields / Imports;
- Plugins / Connectors;
- API & MCP;
- Security / Privacy;
- System / Setup / Health.

## Client Portal — experience model
The Portal must not mirror Admin. Its default experience answers:
1. What needs my attention?
2. What are you working on?
3. What do I owe?
4. What do you need from me?
5. Where are my files?
6. How do I get help?

Recommended primary navigation:

```text
Home
Projects
Billing
Support
Files
More
```

`More` may expose authorised Properties, Approvals, Forms/Requests, Knowledge, Organisation/Account and Vault. Navigation can adapt to enabled modules/access without hiding required actions.

### Portal Home
Primary section: **Needs Your Attention**.

It may include:
- Proposal/Contract decisions where still relevant;
- documents to sign;
- Forms/questionnaires to complete;
- Files requested;
- Project approvals/client actions;
- invoices/deposits/payment milestones;
- renewals/client decisions;
- important incidents/maintenance;
- recent meaningful updates.

### Portal Ariya / live chat
Portal Ariya is strictly Organisation/record scoped. It may explain Projects, Billing, Property Health and client-visible Knowledge, help upload a requested File, create a Support request and hand off through Chatwoot. It never sees internal-only material.

### Preview as Client
Authorized staff must have a safe read-only `Preview as Client` capability for a selected Organisation/User/access context. Preview cannot confer the client's mutation authority.

## Secure External Access and Portal activation
Before Portal Membership, guest/lead/third-party surfaces may include:
- Discovery/Form Request;
- Proposal view/comment/acceptance;
- Contract/signature handoff where configured;
- File Request;
- survey/feedback;
- controlled approval/handover.

Default Portal invitation occurs after Proposal acceptance/commercial commitment. Manual early invite remains possible.

## Global platform primitives not necessarily root navigation
Attention, Action Registry, Notifications, Activity, Audit, collaboration, Reminders, Saved Views/Favorites/Recents, Custom Fields/Taxonomy, Data Provenance, Import/Export/Data Quality, reference numbering, Trash/Restore, Secure External Access, Document Studio, Approvals, booking/scheduling, module toggles and configurable dashboards can appear contextually across the OS.

## Explicit exclusions
The architecture must not create placeholder navigation or schemas for HR, payroll, recruitment, leave/attendance, performance reviews, Timesheets/Time Tracking, work timers or Client Service Consumption/remaining-hours metering.
