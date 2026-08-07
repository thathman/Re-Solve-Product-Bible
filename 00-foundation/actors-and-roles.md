# Re:Solve Actors and Roles

## Purpose

This document defines the people and machine actors Re:Solve must support and establishes the difference between actors, roles, permissions, teams, and scopes.

The final permission model is capability-based. Roles are reusable bundles of permissions, not hard-coded authorization logic.

## Actor Classes

### Staff User

A person working inside the organisation operating Re:Solve.

Typical responsibilities may include:
- client management
- sales
- project delivery
- technical operations
- finance
- support oversight
- content/knowledge management
- system administration

Staff access primarily uses the Admin OS.

### Client User

A member of a client organisation with authenticated access to the Client Portal.

Client users may have different responsibilities and scopes, including:
- organisation administration
- billing
- approvals
- project collaboration
- property management
- confidential information access
- support visibility

### Contractor / External Collaborator

A trusted non-staff user given limited access to specific projects, properties, tasks, files, or other approved records.

Contractors should not inherit broad staff visibility by default.

### Service Account

A non-human identity used by trusted systems, background workers, plugins, connectors, or integrations.

Service accounts require explicit scopes and auditability.

### API Client

A non-human client using the public Re:Solve API.

API clients may use personal, service, or application credentials and must be scoped independently from human UI sessions.

### MCP Client

A trusted AI/agent client using Re:Solve MCP tools and resources.

Examples may include Claude, ChatGPT, Codex, OpenClaw/Hermes, and future agent systems.

MCP access must not imply unrestricted API access.

### Plugin

An installed extension acting through declared plugin permissions and extension points.

Plugins are actors when they read data, perform actions, register jobs, emit events, or invoke connectors.

### Connector

A configured external-system integration acting through declared connector permissions.

## Role Model

Roles provide named permission bundles for convenience.

The product should ship with sensible defaults while allowing administrators to create or modify roles where permitted.

### Suggested Staff Roles

#### Owner

Full strategic and administrative access, including highly sensitive configuration.

Typical capabilities:
- all business records
- system settings
- security
- plugins
- connectors
- API/MCP configuration
- vault administration
- billing administration
- role administration

Certain destructive or security-sensitive actions may still require step-up authentication.

#### Administrator

Broad operational and system administration without necessarily inheriting ownership-level controls such as ownership transfer or protected break-glass functions.

#### Client Success / Account Manager

Focuses on client relationships, organisations, contacts, services, projects, communication, renewals, and client health.

#### Project / Delivery Manager

Focuses on projects, tasks, milestones, deliverables, client actions, approvals, risks, files, and delivery reporting.

#### Technical Operations

Focuses on properties, monitoring, incidents, credentials where authorized, maintenance, connectors, technical tasks, and infrastructure context.

#### Sales

Focuses on leads, opportunities, pipelines, services, proposals, estimates, follow-up activity, and conversion.

#### Finance

Focuses on invoices, payments, receipts, subscriptions, recurring services, credit notes, reconciliation, and financial reporting.

#### Knowledge / Content Manager

Focuses on Re:Solve knowledge, templates, internal documentation, forms, and content-related modules.

#### Analyst / Read-Only Staff

Can inspect approved business records and reports without mutation capabilities.

### Suggested Client Roles

#### Organisation Owner

Highest client-side role for an organisation.

Typical capabilities:
- manage client organisation profile where allowed
- manage client users and invitations
- assign client-side roles
- manage property access within granted scope
- designate billing contacts
- designate approvers
- manage vault access where permitted

#### Organisation Administrator

Broad client-side administration without protected owner-only actions.

#### Project Collaborator

Access to assigned projects, tasks, deliverables, files, approvals, and project communication.

#### Approver

Can review and decide assigned approvals.

#### Billing Contact

Can view financial records permitted to the organisation and receive billing-related notifications.

#### Property Manager

Can view/manage approved property information, property files, related requests, monitoring status, and other granted actions.

#### Vault User

Can access specifically shared vault items according to explicit grants.

#### Read-Only Client Member

Can view approved portal information without mutation rights.

## Permission Structure

Permissions should use stable capability names.

Examples:

### Organisations
- `organisations.read`
- `organisations.create`
- `organisations.update`
- `organisations.archive`
- `organisations.manage_members`

### Contacts
- `contacts.read`
- `contacts.create`
- `contacts.update`
- `contacts.archive`

### Properties
- `properties.read`
- `properties.create`
- `properties.update`
- `properties.archive`
- `properties.manage_access`
- `properties.manage_connectors`

### Projects
- `projects.read`
- `projects.create`
- `projects.manage`
- `projects.archive`
- `projects.approve`

### Billing
- `billing.read`
- `billing.manage`
- `billing.issue_invoice`
- `billing.record_payment`
- `billing.refund`
- `billing.manage_subscriptions`

### Vault
- `vault.read_metadata`
- `vault.create`
- `vault.reveal`
- `vault.download`
- `vault.share`
- `vault.manage_access`
- `vault.delete`

### Plugins / Connectors
- `plugins.read`
- `plugins.install`
- `plugins.configure`
- `plugins.disable`
- `connectors.read`
- `connectors.configure`
- `connectors.rotate_credentials`
- `connectors.replay_events`

### API / MCP
- `api.manage_tokens`
- `api.manage_webhooks`
- `mcp.manage_clients`
- `mcp.manage_tools`
- `mcp.invoke_write_tools`

## Scope Model

Permissions alone are not enough. Access must also be scoped.

Scopes may include:
- workspace
- organisation
- property
- project
- service
- team
- owned/assigned records

A user with `properties.read` should not automatically be able to read every property if their membership or grant limits them to specific organisations/properties.

## Property-Level Access

Property access must be independently enforceable because one organisation may contain multiple properties with different teams and confidentiality boundaries.

A grant may specify:
- property
- descendant inheritance
- permission bundle
- expiration
- source/owner of grant

## Team-Based Access

Teams can be used for:
- assignment
- routing
- ownership
- notification targeting
- reporting
- access defaults

Team membership should not silently bypass explicit security boundaries.

## Temporary and Delegated Access

The system should support time-bound access for sensitive workflows such as:
- temporary vault sharing
- contractor access
- incident response
- project-specific access

Temporary grants require:
- start/end time
- grantor
- reason where required
- audit event
- revocation

## Step-Up Authentication

Certain actions should be able to require recent stronger authentication even when the user is already signed in.

Likely examples:
- reveal highly sensitive vault secret
- download protected credential bundle
- rotate connector credentials
- create/revoke privileged API tokens
- change MFA/security settings
- transfer ownership
- destructive system actions

## Break-Glass Access

A future system-security spec should define emergency access for owner/admin recovery.

Break-glass access must be:
- rare
- strongly authenticated
- highly visible
- fully audited
- notified to appropriate administrators

## Client Portal Visibility

Portal access should be determined by both:
- organisation membership
- record/property grants

Client users must never infer hidden records through counts, search, notifications, URLs, API responses, or AI/MCP outputs.

## AI Actor Rules

Re:Solve AI acts on behalf of the initiating user unless explicitly operating as a separately authorized service workflow.

AI must inherit:
- user permissions
- user scope
- redaction rules
- confirmation policy
- audit policy

AI cannot elevate access.

## Plugin and Connector Actor Rules

Plugins/connectors should request declared capabilities.

They should not receive broad database access merely because they are installed.

Their activity should be attributable through audit/event metadata.

## Role Administration Principles

Administrators should be able to:
- inspect role permissions
- clone roles
- create custom roles where allowed
- compare roles
- view members assigned to roles
- understand inherited versus direct access
- detect dangerous permission combinations

Role editing must clearly explain high-risk permissions.

## Acceptance Rules for Future Specs

Every major feature spec must identify:
- actors
- required permissions
- applicable scope
- client/staff differences
- read-only behavior
- permission-denied state
- audit requirements
- step-up requirements
- API/MCP scope implications