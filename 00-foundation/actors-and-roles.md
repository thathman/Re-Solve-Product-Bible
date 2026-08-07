# Re:Solve Actors, Principals, Roles and Access

## Purpose
This document defines people/machine actors and establishes the difference between Principal, User, Role, Permission, Team and Scope.

The final authorization model is capability + scope. Roles are reusable permission bundles, not hard-coded authorization logic.

## Principal classes

### Human User
Authenticated person. Context may be:
- Staff User
- Client User
- Contractor / External Collaborator

A User may have multiple memberships/grants but remains one human identity.

### Service Account
Non-human system/background identity with explicit scopes and auditability.

### API Client
Non-human Principal using the public Re:Solve API.

### MCP Client
AI/agent Principal using approved MCP tools/resources.

### Plugin
Installed extension acting through declared permissions/extension points.

### Connector
Configured external-system integration acting through declared connector capabilities/permissions.

## Human contexts

### Staff User
Works inside an Operating Entity and primarily uses Admin OS.

Typical responsibilities include client/account operations, sales, projects, technical operations, finance, support oversight, knowledge and system administration.

This role model is operational access only and does not create HR records.

### Client User
Member of a client Organisation using Client Portal with organisation/property/project/billing/Vault scope as granted.

### Contractor / External Collaborator
Trusted limited User with explicit project/property/task/file grants. No broad staff visibility by default.

## Suggested staff roles
Roles are defaults/convenience bundles and may be customized.

### Owner
Broad strategic/system access including protected administration. Step-up may still be required.

### Administrator
Broad platform/operational administration without protected ownership/break-glass powers.

### Client Success / Account Manager
Organisations, Contacts, Services, Projects, Requests, Renewals, relationship reviews and client health.

### Project / Delivery Manager
Projects, Tasks, Milestones, Deliverables, Client Actions, Approvals, Changes, Files and delivery reporting.

No Timesheet responsibility exists.

### Technical Operations
Properties, Monitoring, Incidents, Maintenance, connector context and authorized Vault access.

### Sales
Leads, Opportunities, Pipeline, Services, Proposals, Estimates, Contracts, follow-up/cadences and forecast.

### Finance
Invoices, Payments, Receipts, Subscriptions/recurring billing, Credit Notes, Refunds, reconciliation, statements and approved operational spend.

### Knowledge / Content Manager
Re:Solve Knowledge, templates, Forms and content-related capabilities.

### Analyst / Read-only Staff
Approved read/report access without mutation capabilities.

## Suggested client roles

### Organisation Owner
Highest client-side role for an Organisation, including permitted membership/access administration.

### Organisation Administrator
Broad client administration without protected owner-only actions.

### Project Collaborator
Assigned Projects/Tasks/Deliverables/Files/Collaboration/Approvals.

### Approver
Assigned Approval decisions.

### Billing Contact
Permitted financial records/notifications.

### Property Manager
Approved Property status/Requests/Files/renewal/monitoring visibility and actions.

### Vault User
Only explicitly authorized Vault Items/actions.

### Read-only Client Member
View-only approved Portal information.

## Permission grammar
Canonical capability naming:
- `domain.action`
- `domain.resource.action` when a meaningful sub-resource exists.

Examples:

### Organisations / Contacts
- `organisations.read`
- `organisations.create`
- `organisations.update`
- `organisations.archive`
- `organisations.members.manage`
- `contacts.read`
- `contacts.create`
- `contacts.update`

### Properties
- `properties.read`
- `properties.create`
- `properties.update`
- `properties.archive`
- `properties.access.manage`
- `properties.connectors.manage`
- `properties.monitoring.manage`

### Projects
- `projects.read`
- `projects.create`
- `projects.manage`
- `projects.archive`
- `projects.approve`

No Timesheet/Time permission family exists.

### Billing
- `billing.read`
- `billing.manage`
- `billing.invoices.issue`
- `billing.payments.record`
- `billing.refunds.manage`
- `billing.subscriptions.manage`

### Vault
- `vault.metadata.read`
- `vault.items.create`
- `vault.secret.reveal`
- `vault.secret.copy`
- `vault.file.download`
- `vault.access.request`
- `vault.access.approve`
- `vault.access.manage`
- `vault.audit.read`
- `vault.items.delete`

### Plugins / Connectors
- `plugins.read`
- `plugins.install`
- `plugins.configure`
- `plugins.disable`
- `connectors.read`
- `connectors.configure`
- `connectors.credentials.rotate`
- `connectors.events.replay`

### API / MCP
- `api.tokens.manage`
- `api.webhooks.manage`
- `mcp.clients.manage`
- `mcp.tools.manage`
- `mcp.tools.write.invoke`

## Scope model
Permissions are always combined with scope.

Scopes may include:
- Workspace
- Operating Entity
- Organisation
- Property
- Project
- Service
- Team
- owned/assigned records
- specific protected record

A Principal with `properties.read` does not automatically read every Property when grants limit scope.

## Property-level access
Property grants may specify descendants, expiration, source/grantor and capability bundle.

## Team-based access
Teams support assignment/routing/ownership/notification/access defaults. Team membership must not silently bypass explicit scope/security boundaries.

## Temporary/delegated access
Time-bound grants support contractors, incidents and Vault sharing. Record start/end, grantor, reason where required, Audit and revocation.

## Step-up authentication
Likely actions:
- reveal sensitive Vault secret;
- protected download/export;
- rotate connector credentials;
- create/revoke privileged API/MCP credentials;
- security/MFA changes;
- ownership transfer;
- destructive/high-impact system actions.

## Break-glass
Emergency access must be rare, strongly authenticated, highly visible, append-only audited and notified to appropriate administrators.

## Client Portal visibility
Portal access is determined by Membership plus record/property grants. Hidden records cannot leak through counts, search, URLs, Notifications, API, Àríyá or MCP.

## Àríyá rules
Àríyá acts on behalf of the initiating Principal/User unless an explicitly authorized service workflow is used. It inherits permissions/scope/redaction/confirmation/audit and cannot elevate access.

## Plugin/Connector rules
Plugins/connectors request declared capabilities and do not receive broad database access merely because installed/configured.

## Role administration
Admins can inspect, clone, compare and understand roles/effective access and detect dangerous combinations. High-risk permissions require clear explanation.

## Product exclusions
People & Access is not HR. Do not add employee HR records, payroll, recruitment, attendance, leave, performance review or Timesheets.

## Acceptance rule for future specs
Every major feature identifies:
- actor/Principal;
- required capability;
- scope;
- client/staff differences;
- read-only/denied state;
- Audit;
- step-up/confirmation/approval where applicable;
- API/MCP/Àríyá implications.
