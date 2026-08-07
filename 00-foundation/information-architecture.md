# Re:Solve Information Architecture

## Purpose

This document defines the initial navigation and surface hierarchy for the complete Re:Solve operating system. It is intentionally broad enough to support the loaded OS vision while remaining structured enough that detailed page specifications can be written section by section.

This is not a build order. It is the intended product map.

## Product Surfaces

Re:Solve has two primary human-facing surfaces:

1. **Admin OS** — staff-facing operations
2. **Client Portal** — client-facing collaboration and self-service

It also has machine-facing surfaces:

3. **Public/API surface**
4. **MCP surface**
5. **Plugin extension surface**
6. **Connector surface**

## Admin OS — Primary Navigation

```text
Dashboard

My Work
├── Tasks
├── Calendar
├── Mentions
├── Approvals
├── Reminders
├── Saved Items
└── Drafts / Pending Work

CRM
├── Overview
├── Leads
├── Opportunities
├── Pipelines
├── Organisations
├── Contacts
├── Activities
├── Segments
└── Imports

Clients
├── Overview
├── Organisations
├── Client Health
├── Portal Access
├── Services
├── Renewals
└── Client Activity

Properties
├── Overview
├── All Properties
├── Websites
├── Journals
├── OJS Installations
├── Domains
├── Servers
├── Hosting
├── Stores
├── Infrastructure
├── Property Health
├── Renewals
└── Maintenance

Projects
├── Overview
├── Active Projects
├── My Projects
├── Templates
├── Tasks
├── Milestones
├── Deliverables
├── Client Actions
├── Approvals
├── Change Requests
├── Risks / Issues
├── Time
├── Expenses
└── Completed

Sales
├── Overview
├── Opportunities
├── Pipelines
├── Service Catalogue
├── Proposals
├── Estimates / Quotes
├── Contracts
├── Templates
└── Sales Activity

Billing
├── Overview
├── Invoices
├── Payments
├── Subscriptions
├── Recurring Services
├── Credit Notes
├── Refunds
├── Receipts
├── Expenses
├── Reconciliation
├── Revenue / Receivables
└── Financial Activity

Support
├── Overview
├── Conversations
├── Clients
├── Properties
├── Incidents
├── Entitlements
├── SLA
├── Support Health
└── Analytics

Communications
├── Overview
├── Messages
├── WhatsApp
├── Email
├── SMS
├── Templates
├── Sender Identities
├── Delivery Logs
└── Campaign / Broadcast capability if later approved

Knowledge
├── Overview
├── Articles
├── Spaces
├── Categories
├── Sources
├── Drafts
├── Review Queue
├── Client Knowledge
├── AI Knowledge
└── Suggestions

Vault
├── Overview
├── All Items
├── Credentials
├── Confidential Files
├── Sensitive Notes
├── Shared With Me
├── Access Requests
├── Expiring Access
├── Rotation
└── Audit

Monitoring
├── Overview
├── Properties
├── Uptime
├── Performance
├── Domains
├── SSL
├── Backups
├── Email Health
├── Incidents
├── Maintenance
└── Alert Rules

Files
├── Overview
├── All Files
├── Recent
├── Shared
├── Client Files
├── Project Files
├── Property Files
├── Vault Files
├── Storage
└── Trash / Retention

Forms
├── Overview
├── Forms
├── Templates
├── Submissions
├── Routing
└── Analytics

Automations
├── Overview
├── Workflows
├── Templates
├── Runs
├── Scheduled Jobs
├── Failures
├── Event Explorer
└── Action Catalogue

AI
├── Home / Copilot
├── Briefings
├── Conversations
├── Saved Prompts / Recipes
├── Tools
├── AI Activity
├── Usage
└── Admin Configuration shortcut

Reports
├── Overview
├── Clients
├── CRM / Sales
├── Projects
├── Finance
├── Support
├── Properties
├── Services
├── Team / Workload
├── AI
├── Custom Reports
└── Scheduled Reports

Plugins
├── Installed
├── Available
├── Updates
├── Configuration
├── Permissions
├── Health
├── Development
└── Activity

Connectors
├── Overview
├── Instances
├── Catalogue
├── Events
├── Failures
├── Health
├── Logs
├── Credentials
└── Activity

Audit
├── Audit Explorer
├── Security Events
├── Data Access
├── Vault Access
├── API / MCP Activity
├── Plugin / Connector Activity
└── Export

Settings
```

## Admin OS — Dashboard

The Dashboard is a summary and attention surface, not a duplicate navigation page.

It should ultimately provide role-aware access to:
- AI briefing
- items requiring attention
- my work
- client health
- project risk
- property incidents/renewals
- financial state
- support state
- recent important activity
- quick actions

Dashboard details will be specified separately.

## Admin OS — My Work

My Work is personal operational focus rather than business-wide reporting.

### Tasks
- assigned to me
- assigned by me
- due today
- overdue
- upcoming
- blocked
- waiting on client
- completed recently

### Calendar
- tasks/deadlines
- milestones
- meetings
- renewals
- client dates
- external calendar overlays

### Mentions
- comments
- notes
- project discussions
- records mentioning user

### Approvals
- internal approvals
- client approvals awaiting coordination
- decisions needing action

### Reminders
- personal reminders
- record follow-ups
- snoozed notifications

### Saved Items
- pinned clients
- properties
- projects
- reports
- files
- knowledge

## Admin OS — CRM

CRM is the acquisition and relationship management domain.

### Overview
Cross-pipeline summary, follow-ups, activity, conversion, stale relationships, and sales tasks.

### Leads
Early-stage potential clients and contacts.

### Opportunities
Qualified commercial opportunities.

### Pipelines
Visual and list-based pipeline management.

### Organisations
All organisation records, including non-client lifecycle states.

### Contacts
People directory with organisation relationships.

### Activities
Calls, meetings, notes, interactions, follow-up history.

### Segments
Saved dynamic/static groups for workflow, reporting, and communication.

### Imports
Controlled import history, mapping, validation, and duplicate handling.

## Admin OS — Clients

Clients presents the operational relationship after an organisation becomes an active customer.

### Overview
Portfolio health, renewals, service state, outstanding actions, risk, recent activity.

### Organisations
Client-filtered organisation directory.

### Client Health
Derived health indicators and attention reasons.

### Portal Access
Client memberships, invitations, roles, access state, last sign-in, issues.

### Services
Active client services and entitlements.

### Renewals
Upcoming contract/service/property renewals requiring client/account action.

### Client Activity
Cross-domain timeline.

## Admin OS — Properties

Properties is a central operational area.

### Overview
Portfolio health and attention state.

### All Properties
Unified searchable property list.

### Type Views
Type-specific views such as Websites, Journals, OJS, Domains, Servers, Hosting, Stores, and Infrastructure.

### Property Health
Cross-property health explorer.

### Renewals
Expiry/renewal calendar and workflow.

### Maintenance
Planned maintenance and recurring maintenance schedules.

Each Property record should have a workspace capable of showing, as relevant:
- overview
- relationships
- health
- projects
- services
- support
- monitoring
- renewals
- credentials/vault
- files
- activity
- connectors
- custom/plugin tabs

## Admin OS — Projects

Projects is the complete delivery workspace.

A project record may include:
- overview
- plan/timeline
- tasks
- milestones
- deliverables
- approvals
- client actions
- files
- discussions/activity
- risks/issues
- change requests
- time
- expenses
- related properties
- related services
- commercial records
- financial records
- client portal visibility
- automation history

## Admin OS — Sales

Sales manages commercial conversion and documents.

### Service Catalogue
Reusable services, plans, pricing structures, scope defaults, tax behavior, billing frequency, SLA defaults, and delivery defaults.

### Proposals / Estimates / Contracts
Each should support templates, versions, related opportunity/client, approval/signature status, files, activity, and connector references.

## Admin OS — Billing

Billing is operational finance, not necessarily full statutory accounting.

It should cover:
- receivables
- provider-independent payment records
- recurring billing
- subscriptions
- credit/refund lifecycle
- verified receipts
- reconciliation
- revenue/receivable reporting

Payment providers attach through plugins/connectors.

## Admin OS — Support

Support is the Re:Solve operational view over Chatwoot-managed support.

It should not duplicate the Chatwoot agent workspace unnecessarily.

The Re:Solve view should emphasize:
- client context
- property context
- support entitlement
- SLA/risk
- incidents
- related project/service/finance state
- analytics
- deep links to Chatwoot

## Admin OS — Communications

Communications is for Re:Solve-originated client operations.

Primary channels:
- WhatsApp/Baileys
- email
- SMS
- push/in-app notification relationships where relevant

This area should not become a second Chatwoot inbox.

## Admin OS — Knowledge

Re:Solve Knowledge is internal/controlled operational knowledge, separate from Chatwoot support knowledge.

Potential uses:
- SOPs
- service playbooks
- project procedures
- client documentation
- reusable knowledge for built-in Re:Solve AI

## Admin OS — Vault

Vault is a secure collaboration space for confidential information and files.

Vault navigation should make security state visible without exposing secret values unnecessarily.

## Admin OS — Monitoring

Monitoring aggregates operational health from connectors and internal checks.

It should focus on actionable state and incidents rather than recreating every specialist monitoring UI.

## Admin OS — Automations

Automations provides no-code/low-code orchestration over domain events and connector/plugin actions.

The UI should eventually include:
- visual workflow builder or structured step builder
- trigger selection
- conditions
- branches
- delays
- actions
- approvals
- run history
- failures/retry

## Admin OS — Plugins

Plugins UI manages installed business extensions.

Plugin record surfaces should include:
- overview
- version
- compatibility
- permissions
- extension points
- configuration
- migrations
- health
- activity/logs
- update state

## Admin OS — Connectors

Connector UI manages external integrations.

Connector Type view:
- description
- capabilities
- setup requirements
- instances
- docs

Connector Instance view:
- status
- authentication state
- mapped organisation/property
- capabilities
- last sync/call
- health
- recent events
- failures
- credentials reference
- configuration
- logs
- disable/remove

## Admin OS — Settings

Settings is intentionally deep and will receive its own full specification.

Initial hierarchy:

```text
General
├── Workspace
├── Branding
├── Locale
├── Currency
├── Dates & Time
└── Defaults

People & Access
├── Staff
├── Teams
├── Roles
├── Permissions
├── Invitations
├── Sessions
└── Security Access

Client Portal
├── Portal Defaults
├── Client Roles
├── Navigation
├── Permissions
├── Invitations
├── Registration
└── Branding

CRM
├── Lead Sources
├── Pipelines
├── Stages
├── Custom Fields
├── Activities
└── Defaults

Properties
├── Types
├── Relationships
├── Statuses
├── Health Rules
├── Renewal Rules
├── Maintenance
└── Custom Fields

Projects
├── Statuses
├── Priorities
├── Task Types
├── Templates
├── Time Tracking
├── Approvals
└── Defaults

Sales
├── Services
├── Proposal Defaults
├── Estimate Defaults
├── Contract Defaults
├── Numbering
└── Templates

Billing
├── Invoice Defaults
├── Numbering
├── Currencies
├── Taxes
├── Payment Terms
├── Credit Notes
├── Subscriptions
├── Receipts
└── Reconciliation

Support
├── Chatwoot
├── Support Plans
├── Entitlements
├── SLA
├── Categories
├── Routing
├── Business Hours
└── Branding

Notifications
├── Channels
├── Policies
├── Delivery Rules
├── Templates
├── Digests
├── Priorities
└── Defaults

Communications
├── WhatsApp
├── Email
├── SMS
├── Sender Identities
├── Templates
└── Delivery

AI
├── Provider
├── Models
├── Profiles
├── Features
├── Tools
├── Usage
├── Limits
├── Guardrails
└── Audit

Vault
├── Policies
├── Access
├── Step-up Authentication
├── Retention
├── Categories
└── Rotation Defaults

Files
├── Provider
├── Limits
├── Types
├── Retention
└── Security

Automations
├── Defaults
├── Limits
├── Schedules
├── Failure Policy
└── Action Permissions

Plugins
├── Installed Sources
├── Permissions
├── Updates
├── Development
└── Policy

Connectors
├── Defaults
├── Authentication
├── Health
├── Events
├── Retry
├── Secrets
└── Policy

API & MCP
├── REST API
├── API Tokens
├── Scopes
├── Webhooks
├── MCP
├── AI Clients
├── Rate Limits
└── Audit

Security
├── Authentication
├── MFA
├── Password Policy
├── Sessions
├── Devices
├── IP Policy
├── Rate Limits
└── Security Events

System
├── Health
├── Jobs
├── Queue
├── Logs
├── Backups
├── Updates
├── Feature Flags
├── Diagnostics
└── About
```

## Client Portal — Primary Navigation

```text
Home

Properties
├── Overview
└── Property Workspace

Projects
├── Active
├── Completed
└── Project Workspace

Support
├── Overview
├── Conversations
├── Service Status
└── Support Entitlement

Billing
├── Overview
├── Invoices
├── Payments
├── Receipts
├── Services
├── Subscriptions
└── Renewals

Approvals
├── Awaiting Me
├── Completed
└── Approval Detail

Files
├── All Files
├── Recent
├── Shared
└── Project / Property Files

Vault
├── Shared With Me
├── Credentials
├── Confidential Files
├── Access Requests
└── Expiring Access

Knowledge
├── Home
├── Articles
├── Categories / Spaces
└── Saved

Organisation
├── Profile
├── Team
├── Invitations
├── Access
└── Billing Contacts

Notifications

Account
├── Profile
├── Security
├── Devices / Sessions
├── Notification Preferences
└── Appearance / Accessibility Preferences where supported
```

## Client Portal — Home

The Client Portal home should ultimately summarize:
- greeting/context
- actions requiring attention
- project status
- property health
- support state
- billing state
- renewals
- recent files/activity
- notifications

It must not expose internal-only staff data.

## Client Portal — Properties

Client property access is permission-scoped.

A client-safe Property workspace may include:
- overview
- health/status
- related projects
- services
- support
- renewals
- monitoring summary
- approved files
- approved vault items
- activity

## Client Portal — Projects

Client-safe project workspaces may include:
- status/progress
- timeline/milestones
- deliverables
- approvals
- client actions
- files
- project updates
- allowed discussions
- change requests

Internal-only notes, costs, risks, staff-only tasks, and private operational details must remain hidden unless explicitly configured otherwise.

## Client Portal — Support

Support uses Chatwoot as the conversation engine.

Portal should provide:
- support entry point
- recent/open conversation references where useful
- service/support entitlement
- incidents/status relevant to client
- global Chatwoot widget or approved embedded experience

The portal should not recreate a full helpdesk agent UI.

## Client Portal — Billing

The client should be able to understand:
- what they owe
- what has been paid
- what renews next
- what services are active
- what receipts/documents are available

Billing actions must respect payment-provider availability and permissions.

## Client Portal — Vault

Client Vault access should support secure, explicit sharing rather than broad folder inheritance by default.

Likely client flows:
- view shared confidential item metadata
- request access
- step-up authenticate
- reveal/copy/download
- upload requested credentials/files
- see expiry/revocation state

## Client Portal — Organisation

Organisation owners/admins may manage:
- organisation profile fields allowed for self-service
- members
- invitations
- roles
- property access
- billing contacts
- approvers
- vault-related access where permitted

## Global Surfaces

### Global Search

Admin search should support cross-domain discovery with permissions applied before results are returned.

Potential result groups:
- organisations
- contacts
- properties
- projects
- tasks
- opportunities
- commercial records
- invoices
- files
- knowledge
- vault metadata
- support references

### Command Palette

Admin may expose keyboard-first navigation/actions.

### Notification Center

Both Admin and Portal require a global notification entry point.

### Quick Create

Admin may expose context-aware creation actions.

### Activity Timeline

Reusable timeline pattern across organisations, properties, projects, and other major records.

## Machine-Facing Information Architecture

### REST API

Primary resource areas should mirror durable product domains rather than frontend routes.

### Webhooks

Outbound subscriptions should expose approved domain events.

### MCP

MCP tools/resources should be grouped by capability/domain and clearly label read vs write actions.

### Plugin Extensions

Documented extension points should exist for:
- navigation
- dashboard
- record tabs
- settings
- actions
- API
- MCP
- reports
- automations
- notifications

### Connector Interfaces

Connector capabilities should be discoverable through Admin and machine APIs.

## Navigation Principles

1. Navigation groups should map to real operational domains.
2. Avoid duplicate concepts appearing in multiple areas unless one is clearly a contextual view.
3. Record workspaces should reduce unnecessary cross-navigation.
4. Admin supports dense information and power-user movement.
5. Portal supports clarity and confidence.
6. Plugin navigation must use approved extension slots.
7. Connector-specific navigation should not overwhelm core navigation.
8. Mobile portal navigation may use a different presentation pattern while preserving the same information hierarchy.
9. Permissions may hide inaccessible areas, but hidden navigation never replaces authorization.
10. Search and command surfaces must obey permissions and redaction.

## Open Decisions for Detailed Specs

- exact top-level Admin navigation grouping and ordering
- whether Clients remains separate from CRM or becomes a filtered client-focused workspace
- whether Communications is top-level or nested under Clients/Operations
- whether AI is top-level or primarily accessed through global command/assistant UI
- degree of customization allowed for Admin and Portal navigation
- mobile Portal bottom-navigation choices
- plugin navigation limits
- custom dashboards and saved workspace layouts