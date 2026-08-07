# Client Portal Home

## Purpose

The Client Portal Home is the client's operating summary. It should answer: what needs my attention, what is happening with my services/properties/projects, what do I owe, what has changed, and where do I go next?

It is not a mirror of the Admin Dashboard. It must be calmer, simpler, client-safe, task-focused, and deeply useful on mobile/PWA.

## Primary users

- Client organisation owner/admin
- Billing contact
- Project approver
- Project stakeholder
- Technical/property contact
- Other client members with restricted access

The page is shaped by organisation membership, property grants, project participation, billing permissions, and role.

## Core flow

1. Client signs in.
2. Portal resolves organisation and access scope.
3. Home renders urgent client actions first.
4. Client reviews current work, properties, support, billing, and recent activity.
5. Client takes an action or opens a focused workspace.
6. Completion immediately updates the source record and notification state.

## Header

Contains:
- organisation identity
- contextual greeting
- global portal search where permitted
- notification trigger
- account/organisation switcher if user belongs to multiple organisations
- support/chat access
- install-PWA affordance when appropriate

Avoid admin-oriented controls.

## 1. Requires Your Attention

Highest-priority portal section.

Potential items:
- approval requested
- client action overdue
- invoice due/overdue
- credential/access request
- project question requiring response
- upcoming renewal requiring decision
- maintenance notice acknowledgement where applicable

Each item includes:
- plain-language title
- source
- due date/status
- why action is needed
- one obvious primary action
- deep link

Client-facing language must avoid internal jargon.

## 2. Current Work

Summarizes active projects and service work visible to the user.

For each project:
- name
- status
- progress/state representation
- next milestone
- next client action if any
- last meaningful update

Do not expose internal tasks, notes, risks, budgets, or staff-only metadata unless explicitly client-visible.

## 3. Properties

Shows permitted properties with meaningful status.

Each property summary may include:
- name/type
- status
- health summary where client-visible
- maintenance state
- upcoming renewal
- current related project/service

If many properties exist, show prioritized/recent ones plus "View all".

## 4. Support

Chatwoot remains support system.

Portal Home may show:
- support availability/status
- open conversation count if available and permitted
- important support incident/status
- recent selected conversation references
- button to start/open support

Do not duplicate complete Chatwoot conversation streams on Home.

## 5. Billing

Permission-gated.

Shows:
- amount currently due
- overdue invoices
- next recurring service/renewal
- recent payment/receipt

For users without billing permission, this block is omitted entirely rather than showing redacted mystery counts.

## 6. Files & Deliverables

Shows recent client-visible files such as:
- deliverables
- reports
- shared documents
- receipts

Vault-confidential files should be visually distinguished and require appropriate access.

## 7. Recent Activity

Client-safe chronological feed.

Examples:
- milestone completed
- deliverable shared
- invoice issued/paid
- approval recorded
- maintenance completed
- property recovered
- file shared

Never expose internal staff notes, connector logs, AI internals, security metadata, or private finance data beyond role.

## 8. Upcoming

Optional compact timeline for:
- project milestones
- renewal dates
- maintenance windows
- due invoices
- scheduled meetings/events where connected

## Empty / first-use state

A new client with no work yet should see:
- welcome/context
- organisation details
- support access
- onboarding actions if any
- clear explanation of what will appear here

No fake charts or sample records.

## Role-specific home behavior

### Organisation Admin
Broadest permitted overview, including access/team actions.

### Billing Contact
Billing and renewals promoted.

### Project Approver
Approvals and project actions promoted.

### Technical Contact
Properties, maintenance, credentials and support promoted.

One person can have multiple designations; the page prioritizes combined responsibilities without duplicating sections.

## Notifications

Portal Home surfaces unresolved action items, but full history/preferences remain in Notifications.

Important client-facing events can deliver via:
- in-app
- PWA push
- email
- WhatsApp when configured and appropriate

## WhatsApp relationship

WhatsApp/Baileys is appropriate for operational Re:Solve-to-client communication, for example:
- approval reminder
- project update
- invoice reminder
- maintenance/renewal notification
- resolved issue notice

It does not replace Chatwoot for the client's own end-customer support.

## API

Portal API responses must be client-safe projections rather than reusing unrestricted admin payloads.

Expose:
- portal home summary
- attention items
- visible project summaries
- visible property summaries
- billing summary where permitted
- client-safe activity
- support summary

All responses require membership and object-level authorization.

## MCP / AI client access

If client-facing AI/MCP access is ever enabled, it must use separate client scopes and client-safe projections. Admin MCP keys must never be reused in the portal.

Potential future read tools:
- get_my_client_actions
- get_my_projects
- get_my_properties
- get_my_invoices

## Plugin extension slots

Plugins may add client-home blocks only if:
- explicitly portal-safe
- permission aware
- responsive
- bounded in size
- configurable by administrators

## Responsive/PWA

The portal is mobile-first enough to function as an installed daily-use app.

### Mobile priority
1. attention
2. support shortcut
3. current work
4. properties
5. billing if permitted
6. recent files/activity

Use bottom navigation or equally reachable mobile navigation per portal shell spec.

PWA requirements:
- installable
- push capable
- safe offline shell
- touch-friendly
- update prompt
- last-sync indicators for cached content
- notification deep links into exact portal records

Offline:
- safe cached summaries may display
- financial/payment actions require connectivity
- approvals should not be silently queued unless designed for conflict-safe offline operation
- Vault contents must never be broadly cached

## Accessibility

- plain-language action labels
- priority not color-only
- screen-reader-friendly status summaries
- keyboard support on desktop
- adequate touch targets on mobile

## Acceptance criteria

- Client can identify outstanding actions within seconds.
- User sees only organisations/properties/projects/billing they are authorized for.
- Home is useful for clients with one property and clients with many properties.
- Chatwoot remains the actual support engine.
- Billing block disappears cleanly for unauthorized users.
- Mobile is a first-class experience rather than a collapsed desktop dashboard.
- Offline/stale state is explicit.
- All client-visible activity is safe for the client's role.

## Demo data

Use a university client with:
- multiple portal members with different roles
- several journal/website properties
- active website redesign project
- one pending approval
- one upcoming domain renewal
- one open support escalation summary
- one unpaid invoice visible only to billing users
- recent deliverable and receipt

## Lovable build slices

1. Portal Home shell + first-use/loading/empty states.
2. Requires Your Attention.
3. Current Work.
4. Properties.
5. Support summary/Chatwoot launch.
6. Billing role-gated block.
7. Recent files/activity/upcoming.
8. Role-specific prioritization.
9. Mobile/PWA/offline polish.
