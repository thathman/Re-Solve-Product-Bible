# Re:Solve Domain Model

## Purpose

This document defines the initial conceptual domain model for Re:Solve. It describes product relationships and ownership without prematurely locking implementation details such as database schema, ORM, or backend framework.

## Domain Map

```text
Workspace
├── Users
├── Roles / Permissions
├── Teams
├── Organisations
│   ├── Contacts
│   ├── Memberships
│   ├── Properties
│   ├── Client Services
│   ├── Opportunities
│   ├── Projects
│   ├── Commercial Records
│   ├── Billing Records
│   ├── Support Context
│   ├── Files
│   ├── Vault Items
│   └── Connector Mappings
├── Knowledge
├── Notifications
├── Automations
├── Plugins
├── Connectors
├── API / MCP Clients
├── Audit
└── System Configuration
```

## 1. Identity and Access Domain

### Workspace

Top-level operational boundary for an installation or tenant if multi-workspace behavior is later required.

### User

Authenticated identity.

### Organisation Membership

Links a user to an organisation with status, role, permissions, and potentially explicit scope.

### Team

Operational grouping of users.

### Role

Named permission bundle.

### Permission

Stable capability identifier.

### Access Grant

Explicit scoped permission assignment that may target an organisation, property, project, vault item, or other protected resource.

Potential attributes:
- principal
- scope type
- scope id
- permissions/role
- inheritance behavior
- source
- starts at
- expires at
- revoked at

## 2. Organisation and CRM Domain

### Organisation

Central business entity representing a prospect, client, partner, vendor, or other organisation.

Important state dimensions may include:
- relationship type
- lifecycle status
- account owner
- health
- risk
- tags
- segments
- billing profile
- portal status

### Contact

Person associated with an organisation.

### Lead

Potential commercial relationship not yet qualified.

### Opportunity

Qualified commercial opportunity.

### Pipeline

Configurable commercial process.

### Pipeline Stage

Ordered stage within a pipeline.

### Activity

User-readable interaction or business timeline item.

Examples:
- call
- meeting
- email
- note
- status change
- payment received
- project started

## 3. Property Domain

### Property

Central asset/entity representing digital or operational infrastructure.

Core properties should remain generic enough to support extensible types.

Potential base attributes:
- organisation
- name
- type
- status
- description
- owner/team
- parent
- primary URL/identifier
- environment
- health summary
- lifecycle dates
- tags
- custom fields

### Property Relationship

Supports typed relationships beyond parent-child.

### Property Access Grant

Scopes access to property and optionally descendants.

### Property Health

Derived or cached operational health assembled from monitoring, renewals, connectors, incidents, and manual status.

### Property Renewal

Tracks renewal/expiry obligations such as domain, hosting, maintenance, license, or service renewal.

## 4. Service Domain

### Service Catalogue Item

Reusable definition of a service Re:Solve's operating organisation offers.

Potential fields:
- name
- category
- description
- pricing model
- default price
- currency
- billing frequency
- taxable
- default SLA
- default deliverables
- active/inactive

### Client Service

Instantiated service relationship for an organisation.

Links may include:
- organisation
- service catalogue item
- properties
- contract
- project/template
- billing schedule
- support entitlement
- owner
- start/end/renewal

### Service Entitlement

Defines included service/support rights, limits, frequency, and SLA behavior.

## 5. Project and Delivery Domain

### Project

Bounded body of work for an organisation.

May link to:
- organisation
- properties
- services
- opportunity
- proposal/estimate
- contract
- invoices

### Project Member

Participant and project-level role.

### Task

Actionable work unit.

### Subtask / Checklist Item

Smaller completion elements under tasks where appropriate.

### Milestone

Significant project checkpoint.

### Deliverable

Output intended for completion, delivery, review, or approval.

### Client Action

Explicit dependency owned by client.

### Approval Request

Generic approval record.

Potential target types:
- deliverable
- proposal
- estimate
- contract
- change request
- expense
- other plugin-defined records

### Approval Decision

Decision event with outcome, actor, comment, timestamp, and optional change request detail.

### Change Request

Request to alter scope, output, timing, or implementation.

### Risk / Issue

Project risk, blocker, decision, or issue requiring tracking.

### Time Entry

Recorded work time where time tracking is enabled.

### Expense

Project or operational expense where enabled.

## 6. Commercial Domain

### Proposal

Structured commercial proposal.

### Estimate / Quote

Priced offer/estimate.

### Contract

Commercial agreement metadata and lifecycle.

### Signature Envelope Reference

Connector-owned signing transaction reference linked to a commercial document.

### Commercial Template

Reusable proposal, estimate, contract, terms, or content template.

## 7. Billing Domain

### Invoice

Receivable record.

### Invoice Line

Individual billed item.

### Payment

Confirmed payment record.

### Payment Allocation

Links a payment to one or more invoices/receivables.

### Payment Attempt / Provider Event

External payment-provider lifecycle event or attempt.

### Credit Note

Reduces or reverses invoice value.

### Refund

Tracks confirmed refund lifecycle.

### Receipt

Verified proof-of-payment artifact linked to confirmed financial events.

### Subscription

Recurring commercial billing agreement owned by Re:Solve.

### Provider Subscription Mapping

Connector mapping between Re:Solve subscription and external provider subscription.

### Reconciliation Record

Tracks matching between expected Re:Solve financial records and external provider/bank events.

## 8. Support Operations Domain

Chatwoot owns message/conversation truth.

Re:Solve may own:

### Support Mapping

Links organisation/contact/property/service context to Chatwoot identifiers.

### Support Entitlement

Defines allowed support scope and SLA.

### Support Summary

Derived/cached metrics and conversation state for operational display.

### Incident

Operational incident that may be related to Chatwoot conversations but remains a Re:Solve operational record.

### SLA Policy

Defines response/resolution expectations where Re:Solve needs operational awareness independent of Chatwoot internals.

## 9. Communications Domain

### Message Template

Reusable message content for email, WhatsApp, SMS, push, or other channels.

### Outbound Message

Operational message initiated by Re:Solve.

### Delivery Attempt

Tracks provider/channel delivery status.

### Sender Identity

Configured sending identity/account/channel.

WhatsApp/Baileys belongs here rather than the managed-customer-support domain.

## 10. Notification Domain

### Notification

User awareness record.

### Notification Event

Source event that generated one or more notifications.

### Notification Delivery

Per-channel delivery attempt/state.

### Notification Preference

User preference by event/category/channel.

### Notification Policy

System/default rules controlling mandatory delivery, escalation, priority, digest behavior, and fallback.

### Digest

Grouped notification summary for a time interval.

## 11. File Domain

### File

Managed file metadata.

### File Version

Versioned binary/document revision where versioning applies.

### File Link

Relationship between a file and any supported business record.

### File Share

Controlled sharing state where needed.

Files may be ordinary or confidential. Confidential files may be governed by Vault controls.

## 12. Secure Vault Domain

### Vault Item

Protected confidential record.

Potential types:
- credential
- secret
- note
- document
- file
- recovery material

### Vault Secret Version

Version of protected secret material.

### Vault File

Confidential file attachment.

### Vault Grant

Explicit access grant.

### Vault Access Request

Request for temporary or privileged access.

### Vault Access Event

Audit-oriented access record for reveal/copy/download/share/revoke/etc.

### Vault Rotation

Rotation policy/history for credentials where applicable.

## 13. Knowledge Domain

### Knowledge Space

Logical grouping/security boundary.

### Knowledge Article

Structured knowledge item.

### Knowledge Category

Classification hierarchy.

### Knowledge Revision

Version history.

### Knowledge Source

External or uploaded source used by Re:Solve AI/search where supported.

### Knowledge Access Policy

Controls staff/client visibility.

## 14. Automation and Event Domain

### Domain Event

Structured internal event.

### Automation Workflow

Configured automation definition.

### Trigger

Event, schedule, manual, webhook, connector, or AI-triggered start condition.

### Condition

Rule controlling workflow path.

### Action

Controlled operation.

### Automation Run

Execution instance.

### Automation Step Run

Per-step execution state.

### Scheduled Job

System/plugin registered recurring work.

## 15. Plugin Domain

### Plugin Definition

Installable extension metadata and declared capabilities.

### Plugin Installation

Installed version/state.

### Plugin Configuration

Scoped configuration.

### Plugin Permission Grant

Approved capabilities.

### Plugin Migration

Versioned data/schema migration metadata.

### Plugin Extension Registration

Declared UI/API/event/job/search/report/MCP extensions.

## 16. Connector Domain

### Connector Definition

Reusable integration type.

### Connector Instance

Configured external connection.

### Connector Credential Reference

Reference to protected credentials without exposing raw secrets in normal configuration data.

### Connector Mapping

Maps Re:Solve records to external identifiers.

### Integration Event

Inbound/outbound connector event.

### Connector Health

Derived state describing connectivity/configuration/functionality.

### Connector Action

Declared operation offered by connector.

## 17. AI Domain

### AI Provider Configuration

Configured model/provider relationship for Re:Solve AI.

### AI Profile

Purpose-based model/tool/policy selection.

Examples:
- fast
- balanced
- reasoning
- drafting

### AI Conversation / Session

Contextual Re:Solve AI interaction where conversation persistence is supported.

### AI Tool

Controlled operation available to AI.

### AI Run

Auditable model invocation/action trace where required.

### AI Usage Record

Token/cost/provider/model usage metadata.

## 18. API / MCP Domain

### API Client

External client identity.

### API Token / Credential

Scoped credential.

### API Scope

Permission bundle for machine access.

### Webhook Subscription

Outbound event subscription.

### Webhook Delivery

Delivery attempt and retry state.

### MCP Client

Authorized agent identity.

### MCP Tool Registration

Tool definition and access policy.

### MCP Audit Event

Invocation record.

## 19. Audit Domain

### Audit Event

Immutable/semi-immutable accountability record.

Recommended dimensions:
- actor type/id
- action
- target type/id
- organisation
- property
- timestamp
- source/interface
- correlation id
- security metadata
- summarized changes
- outcome

## 20. Settings Domain

Settings should be scoped intentionally rather than stored as an unstructured global blob.

Potential scopes:
- system
- workspace
- organisation defaults
- user preferences
- module/plugin
- connector instance

A setting definition should specify:
- owner
- data type
- validation
- default
- sensitivity
- permissions
- audit requirement
- restart/reload behavior

## Cross-Domain Relationship Principles

### Organisation is a major relationship root

Most business records should be attributable to an organisation when relevant.

### Property is a major operational context

Technical/service records should attach to property where doing so improves understanding and permissions.

### Activity and Audit are separate

Activity = useful narrative for users.
Audit = accountability/security evidence.

### External identifiers live in mappings

Do not pollute core records with provider-specific fields when a connector mapping can hold them.

### Sensitive material is separated from ordinary metadata

Normal business records may reference protected Vault material but should not contain raw secrets.

### Derived data is distinguishable

Health scores, summaries, analytics, AI outputs, and cached connector data should be identifiable as derived/cached rather than authoritative source records.

## Deferred Decisions

The following should be specified later rather than assumed now:
- exact database schema
- exact multi-workspace/tenant implementation
- custom field architecture
- universal tagging architecture
- record versioning breadth
- accounting depth
- polymorphic relation implementation
- search indexing technology
- event transport technology
- object storage technology
- final auth provider architecture