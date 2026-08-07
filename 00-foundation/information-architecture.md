# Re:Solve Information Architecture

## Purpose
This document defines the complete Re:Solve surface hierarchy while keeping daily navigation simple.

This is not a build order. The Product Bible can be broad while Lovable implementation remains slice-by-slice.

## Product surfaces
1. **Admin OS** — staff-facing operations.
2. **Client Portal** — client-facing collaboration/self-service.
3. **Secure External Access** — narrow guest actions/documents/forms.
4. **Public/API surface**.
5. **MCP surface**.
6. **Plugin extension surface**.
7. **Connector surface**.

## Navigation rule
The product may contain many capabilities without exposing them all as root navigation.

Admin root navigation must remain shallow, obvious and closer to straightforward service-CRM navigation than app-launcher/module-grid systems.

Do not use Odoo-style app-grid navigation or Twenty-style object/app switching as the primary user model.

## Admin OS — Primary Navigation

```text
Home
  Dashboard
  My Work

Clients
CRM
Properties
Projects
Sales
Billing
Support

Operations
  Monitoring
  Renewals
  Requests
  Knowledge
  Files
  Vault
  Automations
  Reports

Platform
  Connectors
  Plugins
  Audit
  Settings
```

TopBar/global chrome provides Search/Command, Quick Create, Àríyá, Notifications, connection state and Account rather than adding them to root navigation.

## Home

### Dashboard
Role-aware operational summary:
- Àríyá briefing
- Attention
- My Work
- client health
- project state
- Property Posture/incidents/renewals
- receivables/commercial state
- support state
- important recent activity
- quick actions

Dashboard is not a page of interchangeable KPI cards.

### My Work
Views may include:
- Tasks
- Approvals
- Reminders
- Mentions
- Client Actions requiring coordination
- Requests assigned to me
- Renewals assigned to me
- Saved/Favorites
- Draft/Pending work
- Calendar/deadlines

Re:Solve does **not** include timesheets or employee HR workflows.

## Clients
Clients is the post-sale relationship area.

Views:
- Overview
- Organisations
- Client Health
- Onboarding
- Renewals
- Relationship Reviews
- Portal Access
- Active Services
- Client Activity
- Offboarding/Former Clients

Organisation 360 may include:
- overview
- contacts/memberships
- account team
- properties
- services
- projects
- requests
- commercial records
- billing
- support context
- documents/files
- Vault metadata/access
- knowledge
- collaboration/activity
- attention
- portal access
- connectors
- custom/plugin tabs

## CRM
CRM covers acquisition and relationship development before/around active-client state.

Views:
- Overview
- Leads
- Opportunities
- Pipeline
- Organisations
- Contacts
- Activities
- Cadences/Follow-up
- Segments
- Imports
- Forecast

Lead conversion must preserve/deduplicate Organisation and Contact identities rather than blindly creating duplicates.

## Properties
Properties is a first-class operational area.

Views:
- Overview
- All Properties
- Health / Property Posture
- Renewals
- Maintenance
- Incidents
- optional saved/type views such as Websites, Domains, Journals, OJS, Hosting, Servers, Stores

Property workspace may include:
- overview
- hierarchy/relationships
- health/posture and source freshness
- native monitors
- incidents
- renewal/expiry obligations
- maintenance
- projects
- services
- support context
- requests
- Vault
- files
- knowledge
- collaboration/activity
- connector mappings
- plugin tabs

Property type filters should normally be views, not permanent root navigation.

## Projects
Views:
- Overview
- Active
- My Projects
- Completed
- Templates

Project workspace may include:
- overview
- milestones
- tasks
- deliverables
- approvals
- client actions
- requests/change requests
- risks/issues
- files
- collaboration/activity
- related properties/services
- commercial/billing records
- expenses where enabled
- client visibility
- automation history

No Timesheet/Time Tracking feature is part of Re:Solve.

## Sales
Views:
- Overview
- Opportunities / Pipeline shortcuts
- Service Catalogue
- Proposals
- Estimates / Quotes
- Contracts
- Document Studio
- Templates
- Sales Activity/Cadences
- Forecast/Goals

Commercial chain:
`Lead -> Opportunity -> Proposal/Estimate -> Contract -> Client Service -> Project/Delivery -> Billing/Renewal`.

## Billing
Views may include:
- Overview
- Invoices
- Payments
- Receipts
- Credit Notes
- Refunds
- Recurring Billing / Subscriptions
- Payment Schedules / Deposits
- Reconciliation
- Account Statements
- Credit Control / Receivables
- Expenses/Spend where enabled

Client Service Consumption/usage-credit tracking is explicitly out of scope.

## Support
Support is the Re:Solve operational/context surface around Chatwoot.

Views:
- Overview
- Conversation References / Open in Chatwoot
- Clients
- Properties
- Incidents
- Entitlements
- SLA/Commercial Context
- Support Health
- Analytics

Re:Solve does not recreate Chatwoot's message/helpdesk console, routing, agents, support KB or Captain.

## Monitoring
Monitoring is a native Re:Solve platform capability.

Views:
- Overview
- Properties
- Native Monitors
- Incidents
- Domains / SSL
- Backups / Heartbeats
- Performance
- Maintenance
- Alert Rules
- Probe/Worker Health
- External Monitoring Sources

Uptime Kuma is optional connector territory, not required infrastructure.

## Renewals
Renewal Desk provides cross-domain obligations:
- Domains
- Hosting
- Certificates
- Services
- Contracts
- Licenses/provider obligations
- other Property dependencies

Views:
- Overdue
- Next 7 / 30 / 60 / 90 Days
- Client Decision Required
- Payment Required
- Auto-renew Unknown/Off
- Completed / Verification Required

## Requests
Views:
- Overview
- New / Triage
- Assigned
- Waiting on Client
- In Progress
- Completed
- Request Types / Templates where authorized

Requests may convert/link into Tasks, Projects, Support, Approvals, Opportunities/Estimates, Change Requests or Vault access flows.

## Knowledge
Re:Solve Knowledge is separate from Chatwoot support Knowledge.

Views:
- Home
- Articles
- Spaces
- Categories
- Drafts
- Review Queue
- Client Knowledge
- Suggestions
- Sources / AI indexing controls

## Files
Views:
- All Files
- Recent
- Shared
- By Client
- By Property
- By Project
- Storage / Retention
- Trash where supported

Protected confidential documents belong in Secure Vault rather than being simultaneously exposed as ordinary Files.

## Vault
Views:
- My Access
- Authorized Items
- Credentials
- Confidential Files/Documents
- Shared With Clients
- Access Requests
- Expiring/Rotation Due
- Audit

## Automations
Views:
- Overview
- Workflows
- Recipes/Templates
- Runs
- Scheduled Jobs
- Failures / Retry
- Event Explorer
- Action Catalogue

Automation actions reuse the shared Action Registry and connector/plugin contracts.

## Reports
Views may include:
- Overview
- Clients
- CRM/Sales
- Projects
- Finance
- Support
- Properties/Monitoring/Renewals
- Services
- AI/Àríyá usage
- Custom Reports
- Scheduled Reports

No HR/timesheet/workforce-performance reporting.

## Connectors
Views:
- Overview
- Instances
- Catalogue
- Mappings
- Events
- Failures / Dead Letter
- Health
- Logs
- Credential references

Initial/future connectors include Chatwoot, WhatsApp/Baileys, payment providers, OpenRouter, Documenso, Cloudflare, optional Uptime Kuma, OJS, WordPress, WooCommerce, email, calendar, storage and others.

## Plugins
Views:
- Installed
- Available/Sources
- Updates
- Permissions
- Health
- Configuration
- Development
- Activity

Plugins add capability; connectors integrate external systems.

## Audit
Views:
- Audit Explorer
- Security Events
- Data Access
- Vault Access
- API/MCP Activity
- Plugin/Connector Activity
- Export where permitted

Audit is append-only evidence, distinct from Activity.

## Settings
Top-level groups:
- General / Workspace
- Operating Entities & Brands
- People & Access
- Client Portal
- CRM
- Clients / Lifecycle
- Properties / Monitoring / Renewals
- Projects
- Sales / Document Studio
- Billing
- Support / Chatwoot
- Requests / Forms
- Notifications
- Communications
- Àríyá / AI
- Vault
- Files
- Automations
- Data / Custom Fields / Imports
- Plugins
- Connectors
- API & MCP
- Security / Privacy
- System

Settings is deep, but ordinary navigation remains simple.

## Global platform primitives not necessarily root navigation
These capabilities can appear contextually across the OS:
- Attention Engine
- Command and Action Registry
- Notifications
- Collaboration/comments/mentions/following
- Reminders/cadences
- Saved Views/Favorites/Recents
- Custom Fields/Taxonomy
- Data Provenance/Freshness
- Import/Export/Data Quality
- Human Reference Numbering
- Archive/Trash/Restore lifecycle
- Secure External Access
- Document Studio
- Forms
- Approvals
- Calendar/Booking
- Feedback/Surveys
- Business Goals/Forecasting
- Operational Communications/Announcements

## Client Portal — Primary Navigation
Recommended default:

```text
Home
Properties
Projects
Support
Billing
Approvals
Files
Knowledge
Organisation
```

Conditional destinations:
- Requests
- Vault, only when client has authorized secure access

Notifications and Account remain in global chrome rather than main navigation.

## Client Portal areas

### Home
- client-safe Attention/actions
- project summary
- Property Posture
- incidents/maintenance
- invoices/renewals
- approvals
- requested files/actions
- recent meaningful updates

### Properties
- hierarchy/summary
- client-safe posture
- incidents/maintenance
- renewal actions
- related projects/services/files/knowledge

### Projects
- status
- milestones
- deliverables
- approvals
- client actions
- files
- client-visible collaboration

### Support
- support entitlement
- active incidents
- recent safe conversation references
- open/continue support in Chatwoot
- service status

### Billing
- invoices
- payments
- receipts
- account statement
- active services
- renewals
- accepted client-safe commercial documents

### Approvals
- awaiting me
- completed
- approval detail

### Files
- shared files
- project/property files
- requested uploads

### Knowledge
- client-visible articles and property/project guidance

### Organisation
- profile
- members/access/invitations for authorized client admins
- billing contacts
- communication preferences

### Requests
If enabled, simple request submission/status/clarification.

### Vault
Only explicitly authorized secure items and access requests.

## Secure External Access
Guest/lead/third-party surfaces may include:
- proposal/estimate view/acceptance
- contract signature handoff
- file upload request
- form/survey
- deliverable approval
- controlled report/handover package

These pages are branded, narrow and do not expose the full Portal shell.

## Machine-facing surfaces

### API
Versioned provider-neutral resources/actions with capability and record-level authorization.

### MCP
Curated tools/resources for approved AI/agent clients. No arbitrary SQL or unrestricted Vault access.

### Àríyá
User-facing AI consumes controlled tools/actions and source evidence while inheriting caller permissions.

## Explicit product exclusions
The following are not Re:Solve product areas:
- HR management
- payroll
- leave/attendance/recruitment/performance reviews
- timesheets/time-tracking
- Client Service Consumption/credit-hour metering

The architecture should not create placeholder navigation or schemas for them.
