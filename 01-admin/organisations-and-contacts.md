# Organisations and Contacts

## Purpose

Organisations and Contacts form the relationship spine of Re:Solve. They represent who Re:Solve serves, who works with them, how people relate to multiple organisations/properties, what access they have, and the complete operational context surrounding those relationships.

This area must support both CRM work and existing-client operations without forcing duplicate records.

## Core concepts

### Organisation
A client, prospect, partner, vendor, institution, or other legal/operational entity.

### Contact
A real person. A contact can relate to multiple organisations and properties through memberships/roles.

### Membership
The relationship between a contact and an organisation, including role, status, permissions, dates, and optional property scope.

### Relationship state
Examples:
- prospect
- active client
- paused
- former client
- partner
- vendor

Relationship state must not be overloaded with billing or project state.

## Organisation List

### Purpose
Give staff a high-speed view of organisations with enough context to prioritize work.

### Columns/fields
Configurable columns may include:
- organisation name
- type
- relationship state
- primary contact
- account owner
- active properties
- active projects
- outstanding receivable summary
- support status
- next renewal
- last meaningful activity
- health indicators
- tags

### Filters
- type
- relationship state
- owner/team
- tags
- has active project
- has overdue invoice
- has property issue
- support plan
- last activity range
- created range
- custom fields

### Views
- all organisations
- active clients
- prospects
- attention needed
- recently active
- archived
- saved custom views

### Actions
- create organisation
- export permitted records
- bulk owner assignment
- bulk tagging
- archive when allowed

## Organisation 360 Workspace

The organisation record is a major workspace, not a single form.

### Header
Shows:
- name
- logo/avatar/initial
- type
- relationship state
- health/context indicators
- account owner
- tags
- primary actions

Primary actions may include:
- add contact
- add property
- create project
- create opportunity
- create invoice
- share vault item
- send operational message
- open support summary

### Tabs/sections

#### Overview
- relationship summary
- primary contacts
- current work
- properties
- finance snapshot
- support snapshot
- upcoming renewals
- latest meaningful activity
- important notes

#### Contacts
- memberships
- contact roles
- portal access
- billing/contact designations
- property-specific roles
- invitation/access state

#### Properties
All properties owned/managed for the organisation with hierarchy and health.

#### Projects
Active, upcoming, completed, and archived projects.

#### Commercial
- opportunities
- proposals
- estimates
- contracts
- services

#### Billing
- invoices
- payments
- subscriptions/recurring services
- credits/refunds where applicable

#### Support
Re:Solve support summary backed by Chatwoot connector metadata and internal service context.

#### Vault
Confidential items scoped to the organisation, permission-gated.

#### Files
Non-vault files shared with or related to the organisation.

#### Activity
Unified operational timeline with filters.

#### Notes
Internal notes with permissions and mentions.

#### Access
Portal members, roles, property grants, invitations.

## Organisation creation flow

Minimum creation should be lightweight:
- name
- organisation type
- relationship state
- owner
- optional primary contact

Additional details can be completed later.

Avoid huge onboarding forms for basic creation.

Duplicate detection should warn on:
- similar organisation name
- matching domain
- matching billing identity

Warnings should not silently merge records.

## Organisation fields

Potential core fields:
- legal/display name
- short name
- type
- relationship state
- website
- email domain(s)
- phone
- address
- country/region
- timezone
- default currency
- billing identity
- tax identifiers
- account owner/team
- source
- tags
- custom fields
- internal description
- archival state

Sensitive finance identifiers must respect permission boundaries.

## Contact List

### Columns
- name
- email
- phone
- organisations
- primary organisation
- role/title
- portal access
- last activity
- owner
- status

### Filters
- organisation
- role
- portal access
- property access
- owner
- status
- tags
- last activity

## Contact Workspace

### Overview
- identity and channels
- memberships
- primary organisation
- role/title
- owner
- communication preferences
- portal/access state
- current work relationships
- recent activity

### Organisations
A contact may belong to more than one organisation.

### Properties
Property-specific roles/access.

### Projects
Projects where the person is a stakeholder, approver, contributor, or contact.

### Communications
Operational communication history owned by Re:Solve. Chatwoot end-customer conversation history is not indiscriminately copied here.

### Access
Portal roles, invitations, MFA/access state where appropriate.

## Contact identity rules

Email is not canonical identity by itself.

A contact may have:
- multiple email addresses
- multiple phone numbers
- one or more organisation memberships
- one or more external identities/mappings

Potential duplicate detection should use multiple signals.

## Client/portal designations

Membership can include designations such as:
- organisation owner/admin
- billing contact
- project approver
- project stakeholder
- technical contact
- property manager
- vault administrator
- support contact

These designations do not automatically grant every related permission; final access is resolved from role + explicit grants + policy.

## Health and relationship signals

Health indicators should be explainable and derived from operational evidence such as:
- unresolved project blockers
- overdue billing
- property incidents
- important support escalations
- inactivity
- renewal risk

Never show a mysterious numerical score without explanation.

## Activity timeline

Potential event families:
- contact added/removed
- portal invitation
- property created
- project started/completed
- proposal/contract events
- invoice/payment events
- vault share/access events
- operational communications
- support escalation references
- ownership change
- important notes

Timeline filtering by entity/event category is required.

## Archive and deletion

Prefer archive over destructive deletion for records with operational history.

Deletion requires dependency analysis and elevated permission. Records with legal, billing, audit, or project history may be non-deletable.

## Permissions

Representative capabilities:
- organisations.read
- organisations.create
- organisations.update
- organisations.archive
- organisations.export
- contacts.read
- contacts.create
- contacts.update
- contacts.archive
- client_access.manage
- organisation_finance.read
- organisation_vault.read

Property-scoped users only see relevant related data where policy permits.

## Notifications

Events may include:
- ownership assigned
- new client portal invitation accepted
- important contact role changed
- designated approver changed
- client becomes inactive/risk condition triggered

Routine CRUD changes should not spam users.

## Automations

Potential triggers:
- organisation created
- relationship state changed
- contact added
- contact role changed
- portal access granted/revoked
- inactivity threshold reached

Potential actions:
- create onboarding project
- notify owner
- send welcome communication
- create follow-up task
- apply tags
- provision connector mappings

## API

First-class endpoints for organisations, contacts, memberships, access grants, activity, related summaries, and custom fields.

Support filtering, pagination, stable identifiers, optimistic concurrency or equivalent conflict handling for edits, and idempotency for import/create workflows where needed.

## MCP candidates

- search_organisations
- get_organisation
- create_organisation
- update_organisation
- search_contacts
- get_contact
- create_contact
- list_organisation_properties
- get_client_health

Sensitive finance/vault fields must be redacted unless explicitly scoped.

## Plugin extension slots

Plugins may contribute:
- organisation/contact tabs
- custom field groups
- summary cards
- actions
- related record types
- health signals
- activity renderers

## Connector interactions

Possible mappings:
- Chatwoot organisation/contact identifiers
- OJS user identities
- WooCommerce customer identities
- external accounting/contact IDs

Mappings are stored separately from canonical identity.

## Responsive/PWA

Mobile organisation workspace prioritizes:
- header/action summary
- contacts
- current work
- properties
- attention items

Dense tabular detail becomes cards/list rows rather than compressed tables.

Offline reads may use safe cached summaries. Editing identity/access data while offline should normally be disabled.

## Accessibility

- all relationships readable without relying on color
- tab workspaces keyboard navigable
- contact methods have descriptive labels
- tables expose accessible headers and list fallback on mobile

## Acceptance criteria

- One contact can belong to multiple organisations without duplication.
- Organisation 360 presents operational context without requiring module hopping.
- Portal/property access is explicit and inspectable.
- Archived records retain historical references.
- Health indicators always explain their source.
- Duplicate detection warns without auto-merging.
- Sensitive related data obeys permission boundaries.

## Demo data

Use realistic organisations including:
- a university with a main website and multiple journal properties
- a commercial client with one website and active billing
- a prospect with an opportunity but no active service
- a former/archived client

Use contacts with multiple roles, including an organisation owner, billing contact, journal editor, technical contact, and project approver.

## Lovable build slices

1. Organisation list with realistic filters and responsive states.
2. Create/edit organisation.
3. Organisation Overview.
4. Contacts tab + memberships.
5. Contact list and Contact Workspace.
6. Properties/projects relationships.
7. Finance/support/vault summaries with permission gates.
8. Access management.
9. Activity timeline.
10. Mobile/PWA polish and edge states.
