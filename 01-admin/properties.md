# Properties

## Purpose

Properties are a central native object in Re:Solve. A Property represents a digital or operational asset that an organisation owns, operates, publishes, hosts, manages, monitors, or receives service for.

Properties prevent domains, websites, journals, servers, stores, and related assets from becoming disconnected records scattered across modules.

A property is the context anchor for projects, support, credentials, monitoring, files, knowledge, services, renewals, automations, connectors, and client access.

## Examples

- Main corporate website
- University website
- Journal index
- Individual OJS journal
- WordPress site
- WooCommerce store
- Domain
- Hosting account
- Server
- Email service
- API/service endpoint
- Other managed asset

## Hierarchy

Properties may have parent/child relationships.

Example:

Kampala University
- Main Website
- KU Journals
  - Journal A
  - Journal B
  - Journal C
- Main Domain
- Production Server

Rules:
- hierarchy is explicit
- child permissions can inherit where policy allows
- child properties may override service, connector, health, and access configuration
- circular relationships are prohibited
- moving a property between parents is audited

## Property types

Core supports configurable property types. Each type may define:
- icon
- descriptive fields
- supported connectors
- health capabilities
- default tabs
- allowed child types
- default service associations

Core should ship sensible examples without hard-coding every future asset type.

## Property List

### Purpose
Give staff a fast portfolio view of all managed assets.

### Columns
Configurable fields may include:
- property name
- organisation
- type
- parent
- status
- health
- service status
- owner/team
- primary URL/identifier
- renewal/expiry
- last check
- connector status
- active project count
- support state

### Views
- all properties
- websites
- journals
- domains
- infrastructure
- attention needed
- maintenance due
- expiring soon
- disconnected
- archived
- saved views

### Filters
- organisation
- type
- parent
- status
- health
- owner/team
- connector
- service
- expiry range
- maintenance state
- tags
- custom fields

### Bulk actions
Where permitted:
- assign owner/team
- tag
- change status
- schedule maintenance
- export
- trigger allowed health refresh

## Property Workspace

### Header
Shows:
- name
- type
- organisation
- hierarchy breadcrumb
- operational status
- health state
- owner/team
- primary identifier/URL
- important badges
- primary actions

Primary actions can include:
- edit
- create child
- start project
- add service
- add connector instance
- share credential
- schedule maintenance
- create client action
- open support context

### Overview

The overview should answer:
- what is this property?
- who owns/manages it?
- is it healthy?
- what services are attached?
- what work is active?
- what needs attention?

Sections:
- property identity
- health summary
- active services
- active projects/tasks
- upcoming renewals
- connector summary
- support summary
- recent activity
- related credentials/files

### Details
Type-specific operational metadata.

Examples for website:
- URL
- platform/CMS
- environment
- repository reference
- hosting relation

Examples for journal:
- journal title
- acronym
- ISSN fields
- OJS installation relation
- public URL
- editorial/support metadata where permitted

Examples for domain:
- domain name
- registrar
- renewal date
- auto-renew status
- DNS provider

### Children
Hierarchy browser with health/state summaries.

### Services
Services currently delivered for this property, history, recurring/renewal state, service owner, and linked agreements.

### Projects
Projects and project work attached to the property.

### Support
Re:Solve context about support for this property, backed by Chatwoot where applicable. Includes support entitlement, known incidents, selected conversation references, and escalation state.

### Monitoring
Health signals from native checks or monitoring connectors:
- uptime
- domain expiry
- SSL
- backup state
- performance
- application version state
- connector health

Monitoring capability varies by property type and configured providers.

### Vault
Permission-gated credentials/confidential files scoped to the property.

### Files
Non-secret files.

### Knowledge
Operational/internal/client-safe knowledge attached to the property.

### Connectors
Connector instances and mappings attached to the property.

### Activity
Unified event timeline.

### Access
Users/contacts/teams with property-specific access.

## Property health

Health must be explainable.

Suggested state model:
- healthy
- needs_attention
- degraded
- critical
- unknown
- maintenance

Health is derived from signals, not manually painted green/red without evidence.

Each state exposes contributing signals and timestamps.

Examples:
- website offline -> critical
- domain expires soon -> needs_attention
- monitoring connector stale -> unknown/needs_attention
- active scheduled maintenance -> maintenance

## Property status vs health

Status describes lifecycle:
- onboarding
- active
- paused
- retired
- archived

Health describes current operational condition.

Do not conflate them.

## Ownership

A property can have:
- accountable staff owner
- operational team
- client-side contacts
- technical contacts
- approvers

## Client visibility

Not every internal property must be visible in the Client Portal.

Visibility policy controls:
- hidden from portal
- visible summary only
- normal portal access
- restricted to explicitly granted client users

## Notifications

Potential events:
- property created
- ownership changed
- health degraded
- health critical
- recovered
- renewal approaching
- maintenance scheduled/started/completed
- connector disconnected
- credential rotation due

Delivery depends on severity and user preferences/policy.

## Automations

Triggers:
- property created
- property type changed
- health changed
- expiry threshold reached
- connector state changed
- maintenance window reached

Actions:
- create task
- create incident
- notify staff/client
- WhatsApp client contact
- launch workflow
- request approval
- invoke connector

## API

First-class endpoints for:
- CRUD
- hierarchy
- health
- services
- projects
- access
- connectors
- monitoring summary
- activity

API consumers must not gain vault secret values through ordinary property reads.

## MCP candidates

- search_properties
- get_property
- get_property_health
- list_property_children
- list_expiring_properties
- list_property_services
- get_property_support_summary

Write tools such as update_property require explicit scopes.

## Plugins

Plugins can contribute:
- property types
- type-specific fields
- tabs
- health signal providers
- actions
- reports
- automation triggers/actions
- MCP tools

Plugin-contributed fields must remain namespaced and portable.

## Connectors

A connector instance may attach to:
- one property
- multiple related properties where provider semantics require it
- an organisation with child property mappings

Examples:
- one OJS installation connector mapping several journal properties
- one WordPress connector for one website
- monitoring connector tracking several properties
- Chatwoot inbox mapped to organisation with property context

## Security

- property grants are explicit
- parent inheritance must be inspectable
- cross-organisation property access is denied
- sensitive technical metadata can require elevated permission
- secret material stays in Vault

## Responsive/PWA

### Mobile property workspace
Priority order:
- identity/status
- health/attention
- active work
- services
- upcoming renewal
- support/maintenance
- activity

Hierarchy uses drill-down navigation rather than cramped trees.

Offline:
- safe summaries may be cached
- health must show last checked timestamp
- no credential values cached
- connector actions disabled offline

## Acceptance criteria

- Properties can form safe parent/child hierarchies.
- Property health is explainable and separate from lifecycle status.
- All major work can associate with a property without requiring one.
- Client visibility and property access are separately controlled.
- Connector mappings do not become canonical property identity.
- Mobile provides a functional property workspace.
- Vault values never leak into normal property responses/caches.

## Demo data

Use a university organisation with:
- Main Website
- Journals parent property
- three journal children
- domain
- server/hosting property

Include one healthy property, one expiring domain, one degraded journal connector, one property in maintenance, associated projects/services, and property-scoped contacts.

## Lovable build slices

1. Property list + filters + demo hierarchy.
2. Create/edit property + type handling.
3. Property Overview.
4. Parent/child hierarchy UX.
5. Services/projects/support related panels.
6. Health/monitoring summary.
7. Access and portal visibility.
8. Connector and Vault/File metadata views.
9. Responsive/PWA pass.
