# Admin Dashboard

## Purpose

The Admin Dashboard is the operational command surface for Re:Solve staff. It must answer, within seconds: what changed, what needs attention, what is blocked, what is due, what is at risk, and what action should happen next.

It is not a generic KPI wall. It is a prioritized operating brief that combines personal work, client health, project state, finance, properties, support signals, system health, and AI-generated synthesis.

## Primary users

- Workspace Owner
- Administrator
- Operations staff
- Account/Client managers
- Project/Delivery staff
- Finance staff
- Support-adjacent staff with permission

The dashboard is permission-shaped. Users never see summary counts for data they cannot open.

## Core flow

1. User opens Admin.
2. System resolves role, team, organisation scope, property scope, saved preferences, and current attention state.
3. Dashboard renders critical and personal information first.
4. User scans the briefing and attention queue.
5. User drills into a record, acts inline where safe, or opens a focused workspace.
6. Completed actions immediately update dashboard state and notifications.

## Information hierarchy

### 1. Header

Contains:
- contextual greeting
- current date
- global search trigger
- quick-create trigger
- notification center trigger
- AI assistant/briefing trigger
- user menu

No decorative hero banner.

### 2. Operational Briefing

A compact, high-information summary generated from deterministic system state, with optional Re:Solve AI synthesis.

Examples:
- 3 client actions are blocking delivery
- 2 properties require attention
- 4 invoices became overdue
- 1 connector has failed repeatedly
- 6 tasks are due today

The AI layer may summarize and prioritize, but the underlying facts must remain inspectable and link to source records.

States:
- AI available
- AI unavailable: deterministic briefing still works
- no attention items: calm all-clear state
- partial data: affected sections labeled

### 3. Attention Queue

This is the most important dashboard element.

Each item must have:
- severity/priority
- concise event title
- related client
- related property/project/invoice/etc.
- age or due time
- owner
- source
- next action
- deep link

Examples:
- Approval overdue
- Domain renewal in 7 days
- Client blocked on deliverable
- Payment verification failed
- Critical connector failure
- Project milestone overdue
- Vault access request waiting

Controls:
- filter by mine/team/all permitted
- snooze
- assign
- resolve when supported
- open source record

### 4. My Work

Shows:
- overdue tasks
- due today
- upcoming
- approvals assigned to me
- reminders
- mentions
- recently reassigned work

Items support quick completion only when the underlying workflow allows safe inline action.

### 5. Client Health

Not a simplistic red/green score. Show explainable signals.

Possible signals:
- active projects at risk
- overdue invoice
- unresolved support escalation
- pending client action
- property incidents
- upcoming renewal
- recent relationship inactivity

Each health indicator must expose why it is shown.

### 6. Project & Delivery Pulse

Shows:
- active projects
- at-risk projects
- milestones due soon
- blocked deliverables
- client actions outstanding
- workload concentration

Optional visualization must answer a real operational question; do not add charts for decoration.

### 7. Property Health

Shows only actionable or noteworthy property information:
- down/degraded properties
- expiring domains/SSL
- failed backup signals
- maintenance due
- connector monitoring failures

Healthy properties should not dominate the dashboard.

### 8. Finance Pulse

Role-gated.

Includes:
- overdue receivables
- invoices due soon
- payments awaiting verification/reconciliation
- recent confirmed payments
- recurring services/renewals due
- unusually large financial exceptions

Amounts must use configured currencies and respect finance visibility permissions.

### 9. Support Pulse

Chatwoot remains support truth.

Re:Solve dashboard may show selected operational support signals only:
- escalated conversations
- SLA risk
- support incidents
- high-priority client issues
- support connector health

Do not mirror every Chatwoot message.

### 10. Activity Stream

Recent meaningful events across permitted records.

Examples:
- project milestone completed
- invoice paid
- property updated
- vault item shared
- client invited
- connector reconnected

Controls:
- filter by domain
- filter by client
- pause live updates
- open source record

### 11. System / Connector Health

Visible to permitted administrators only.

Show exceptions first:
- failing connectors
- webhook backlog
- job failures
- plugin health issue
- notification delivery degradation
- PWA push delivery issue

## Customization

Users may:
- reorder selected sections
- collapse low-priority sections
- choose mine/team/workspace scope where permitted
- save dashboard density preference
- save filters

Users may not remove mandatory critical-alert surfaces.

## Quick Create

Context-aware quick create should support permitted record types such as:
- organisation
- contact
- lead/opportunity
- property
- project
- task
- invoice
- approval request
- vault item

Creation opens a focused drawer/dialog where appropriate rather than navigating away by default.

## Responsive and PWA behavior

### Desktop
Dense multi-column operational layout.

### Tablet
Two-column adaptive layout; attention and my work remain first.

### Mobile
Single-column priority feed. Recommended navigation order:
1. briefing
2. attention
3. my work
4. critical property/project/support/finance signals
5. activity

Use touch-friendly controls, bottom sheets for quick actions, and no horizontally crushed desktop tables.

### Offline
- shell loads
- last safely cached non-sensitive dashboard snapshot may display with stale indicator
- destructive/write actions disabled unless safely queued
- no cached vault secret values
- clear offline banner

## Permissions

Dashboard queries must enforce permissions server-side. Counts must not leak inaccessible records.

Examples of capabilities:
- dashboard.view
- dashboard.team_scope
- dashboard.workspace_scope
- finance.summary.read
- system.health.read
- support.summary.read

## Notifications

Dashboard does not replace the notification center. It promotes selected unresolved notification-derived items into the attention queue.

## API

Expose dashboard primitives, not one opaque UI blob:
- GET summary
- GET attention items
- GET work queue
- GET health summaries
- GET activity
- mutation/action endpoints for supported inline actions

Responses must be permission filtered.

## MCP candidates

- get_daily_briefing
- get_attention_queue
- get_my_work
- get_client_risks
- get_property_alerts
- get_finance_exceptions

AI clients must receive source identifiers and deep links where possible.

## Plugin extension slots

Plugins may contribute:
- attention item providers
- dashboard widgets
- quick-create actions
- health signals
- activity event renderers

Plugin widgets must use approved design primitives and obey dashboard density rules.

## Connector interactions

Dashboard can consume summarized states from connectors including Chatwoot, monitoring, payment, signing, calendar, and communications connectors.

## Analytics

Track product behavior, not vanity:
- dashboard section engagement
- attention item resolution path
- quick-create usage
- drilldown usage
- ignored/snoozed items

## Empty state

A healthy workspace should feel calm:
- no fake sample KPIs
- clear 'No urgent attention required'
- show upcoming work and recent activity instead

## Acceptance criteria

- A user can identify their top actionable items without opening another page.
- Hidden data does not leak through counts or summaries.
- Critical items remain prominent regardless of widget customization.
- AI failure does not break the deterministic dashboard.
- Mobile preserves action priority rather than merely stacking every desktop widget.
- Offline mode clearly distinguishes stale data.
- Every dashboard fact links to an inspectable source.

## Demo data

Use realistic demo records around a university client with multiple websites/journals, active projects, one overdue invoice, one expiring domain, one pending approval, selected Chatwoot escalation metadata, and several routine healthy records so priority behavior can be evaluated.

## Lovable build slices

1. Dashboard shell + header + skeleton/empty states.
2. Attention Queue with static realistic demo data.
3. My Work.
4. Client/Project/Property summary sections.
5. Finance and support summary sections with permissions.
6. Activity stream.
7. Customization and responsive/PWA pass.
8. AI briefing integration after deterministic facts are stable.
