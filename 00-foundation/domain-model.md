# Re:Solve Domain Model

## Purpose
This document defines the conceptual Re:Solve domain model without locking database schema, ORM or backend framework.

## Domain map

```text
Workspace
├── Operating Entities
│   └── Brands
├── Principals
│   ├── Human Users
│   ├── Service Accounts
│   ├── API Clients
│   ├── MCP Clients
│   ├── Plugins
│   └── Connectors
├── Roles / Permissions / Access Grants
├── Teams
├── Organisations
│   ├── Contacts
│   ├── Memberships
│   ├── Account Team
│   ├── Properties
│   ├── Client Services
│   ├── Opportunities
│   ├── Projects
│   ├── Requests
│   ├── Commercial Records
│   ├── Billing Records
│   ├── Support Context
│   ├── Files
│   ├── Vault Items
│   ├── Knowledge
│   └── Connector Mappings
├── Attention
├── Notifications
├── Collaboration / Activity
├── Approvals
├── Documents
├── Monitoring / Renewals / Incidents
├── Automations / Actions / Reminders
├── Saved Views / Favorites / Recents
├── Custom Fields / Taxonomy
├── Imports / Exports / Data Quality
├── Plugins / Connectors
├── Àríyá / AI
├── Audit
└── System Configuration
```

## 1. Workspace, Operating Entity and Brand
### Workspace
Top-level installation boundary. A first deployment has exactly one Workspace.

### Operating Entity
Business/legal entity operating within Re:Solve and owning client/commercial relationships, document/billing identity and sender configuration.

### Brand
Customer-facing identity belonging to an Operating Entity.

## 2. Identity and Access
### Principal
General authorization actor. Principal subtypes include Human User, Service Account, API Client, MCP Client, Plugin and Connector.

### Human User
Authenticated person. Staff/client/contractor behavior is derived from memberships/access rather than separate authentication species.

### Organisation Membership
Links a User to an Organisation with status, role, permissions and scope.

### Team
Operational grouping for assignment/routing/ownership/access defaults. It is not an HR record.

### Role
Named permission bundle.

### Permission
Stable capability using canonical grammar `domain.action` or `domain.resource.action`.

### Access Grant
Explicit scoped authorization assignment targeting a Principal and resource scope.

Potential fields:
- principal
- scope type/id
- permissions/role
- inheritance
- source/grantor
- starts/expires
- revoked

## 3. Organisation and CRM
### Organisation
Central relationship entity representing prospect, client, partner, vendor or another organisation.

Important dimensions:
- relationship/lifecycle
- account team
- health/risk
- tags/segments
- billing profile
- portal state
- Operating Entity relationship

### Contact
Person associated with an Organisation.

### Lead
Early commercial lead that may exist before complete Organisation/Contact records are established.

### Opportunity / Pipeline / Stage
Qualified commercial opportunity and its configurable sales process.

### Account Team Assignment
Named operational responsibility such as Account Owner or Technical Owner. Not HR.

### Client Lifecycle / Relationship Review
Cross-domain onboarding/active/offboarding state and periodic account-review records.

## 4. Property and Operations
### Property
First-class digital/operational asset.

Base attributes may include Organisation, name, type, status, description, owner/team, parent, URL/identifier, environment, posture summary, lifecycle dates, tags and custom fields.

### Property Relationship
Typed relationship beyond parent-child.

### Property Access Grant
Property/descendant access scope.

### Monitor
Configured native/external check definition.

### Monitoring Signal
Time-bound observed result from a probe/connector.

### Property Posture
Derived explainable health state assembled from current evidence.

### Renewal / Expiry Obligation
First-class obligation for Domain, Hosting, Certificate, Service, Contract, license or other managed dependency.

### Maintenance Window
Planned operational maintenance/suppression context.

### Incident
Operational service-impact event related to one or more Properties/signals/support references.

## 5. Service Domain
### Service Catalogue Item
Reusable service offering.

Fields may include name, category, description, pricing model, default price/currency, billing frequency, taxable behavior, default SLA, default deliverables and property applicability.

### Client Service
Instantiated service relationship linking Organisation, catalogue item, properties, contract, billing, support entitlement, owner, start/end/renewal and status.

### Service Entitlement
Defines included rights/scope/SLA, not usage-credit consumption.

**There is no core Client Service Consumption meter.**

## 6. Projects and Delivery
### Project
Bounded body of work linked to Organisation, Properties, Services and relevant commercial/billing records.

### Project Member
Participant/project-level responsibility.

### Task / Recurring Task Definition
Actionable work plus optional recurrence template that generates ordinary task occurrences.

### Milestone / Deliverable / Client Action
Delivery checkpoints, outputs and explicit client dependencies.

### Approval Request / Approval Decision
Generic approval workflow and decision evidence.

### Change Request
Structured change to scope/timing/deliverables.

### Risk / Issue
Project risk/blocker/decision tracking.

### Expense
Optional operational/project/client cost record.

**No Time Entry or Timesheet domain exists.**

## 7. Requests
### Request
Structured ask awaiting/under triage or fulfillment.

### Request Type
Configurable request classification/intake behavior.

### Request Conversion/Link
Traceability from Request to resulting Task, Project, Change Request, Approval, Opportunity/Estimate, Chatwoot support reference, Vault request or plugin record.

## 8. Commercial and Document Domain
### Proposal / Estimate / Quote / Contract
First-class commercial records.

### Document Template / Template Version
Reusable branded structure/merge schema.

### Document Draft / Document Version
Rendered/editable representation tied to a business record.

### Final Snapshot
Immutable exact content accepted/executed by a recipient.

### Signature Envelope Reference
External SignatureConnector transaction mapping.

### Secure External Access Grant
Narrow expiring/revocable guest access to a specific document/action.

## 9. Billing and Spend
### Invoice / Invoice Line
Receivable record and line items.

### Payment / Payment Allocation
Confirmed monetary transaction and allocation.

### Payment Attempt / Provider Event
Provider lifecycle event/attempt.

### Credit Note / Refund / Receipt
Financial adjustment/refund/proof-of-payment records.

### Subscription
Recurring commercial billing agreement owned by Re:Solve.

### Provider Subscription Mapping
External provider mapping.

### Reconciliation Record
Expected-versus-external financial matching.

### Payment Schedule / Deposit
Planned installment/deposit terms linked to commercial/billing records.

### Account Statement
Generated client financial statement assembled from billing truth through Document Studio.

### Expense / Recurring Cost
Operational/vendor cost tracking where enabled. No payroll.

## 10. Support Operations
Chatwoot owns support conversation/message truth.

Re:Solve owns:
- Support Mapping
- Support Entitlement
- Support Summary
- Incident
- commercial/operational SLA context

## 11. Communications
### Message Template / Outbound Message / Delivery Attempt / Sender Identity
Shared operational messaging metadata for email, WhatsApp, SMS and other channels.

### Announcement
Controlled staff/client operational notice, distinct from marketing campaigns.

## 12. Notification and Attention
### Notification / Notification Delivery / Preference / Policy / Digest
Durable awareness and channel-delivery model.

### Attention Item
Current condition still requiring awareness/action.

Attention resolves from underlying condition, not merely notification-read state.

## 13. Collaboration and Activity
### Comment / Internal Note / Mention / Follow
Shared collaboration model with explicit audience and record scope.

### Activity
User-readable timeline event.

Activity is separate from Audit.

## 14. Files and Vault
### File / File Version / File Link / Share
Ordinary managed file domain.

### Vault Item / Secret Version / Vault File Content / Grant / Access Request / Access Event / Rotation
Protected confidential domain.

A protected confidential document is represented as a Vault Item and must not retain a parallel ordinary File access path.

Both domains may use the same provider-neutral storage infrastructure.

## 15. Knowledge
Knowledge Space, Article, Category, Revision, Source and Access Policy.

Re:Solve Knowledge is separate from Chatwoot support Knowledge.

## 16. Actions, Automations, Reminders and Cadences
### Action Definition
Registered business operation with permission, scope, risk/confirmation/approval, input/output and interface availability.

### Domain Event
Structured internal fact.

### Automation Workflow / Trigger / Condition / Step / Run
Controlled workflow orchestration.

### Reminder
Lightweight future attention instruction.

### Cadence / Activity Plan
Reusable sequence of follow-up steps using shared actions/automations.

### Scheduled Job
System/plugin recurring background work.

## 17. Views and Extensibility
### Saved View
Saved query/presentation state with private/team/workspace/system visibility.

### Favorite / Recent Record
Personal quick-access metadata; does not grant access.

### Custom Field Definition / Value
Typed deployment-specific field data.

### Tag / Taxonomy
Flexible labels versus controlled vocabularies.

### Custom Record Type
Advanced future extensibility, never a substitute for core domains.

## 18. Data Provenance, Import and Quality
### Provenance Metadata
Source, authority, freshness, connector/import/run and derived/native state.

### Import Batch / Migration Batch
Mapped validated ingestion job.

### Export Job
Permission-aware generated export.

### Data Quality Issue
Duplicate/stale/orphan/mapping/missing-data issue requiring review/fix.

### Merge Record
Audited merge decision preserving relationships/mappings/aliases.

## 19. Plugin and Connector
### Plugin Definition / Installation / Configuration / Permission Grant / Migration / Extension Registration
Installable product-capability extension lifecycle.

### Connector Definition / Instance / Credential Reference / Mapping / Integration Event / Health / Action
External-system integration lifecycle.

Optional provider plugins may register connector implementations.

## 20. Àríyá / AI
### AI Provider Configuration / Profile / Session / Tool / Run / Usage Record
Technical AI runtime records.

Àríyá is the user-facing assistant identity and consumes controlled Action/Data tools under caller permission.

## 21. API / MCP
API Client, API Credential/Scope, Webhook Subscription/Delivery, MCP Client, Tool Registration and MCP Audit Event.

## 22. Audit
### Audit Event
Append-only accountability/security evidence with actor Principal, action, target, scope/context, timestamp, source/interface, correlation, summarized changes and outcome.

## 23. Settings
Settings are typed/scoped definitions rather than an unstructured global blob.

Scopes may include Workspace, Operating Entity, Brand, user preferences, organisation defaults, property type, plugin and connector instance.

## Cross-domain principles
- Organisation is the major relationship root for clients/prospects/vendors.
- Operating Entity represents the business doing the work.
- Property is the major operational asset context.
- Attention is current actionable state; Notification is awareness/delivery.
- Activity is narrative; Audit is append-only accountability.
- External identifiers live in mappings.
- Provider-specific SDK concepts stay behind Connectors.
- confidential content stays behind Vault controls.
- derived/synced/AI data exposes provenance/freshness when material.
- Action Registry centralizes consequential operations across UI/API/MCP/Àríyá/Automations.

## Explicit exclusions
Do not create core domains for:
- HR
- payroll
- attendance/leave/recruitment
- employee performance management
- timesheets/time tracking
- Client Service Consumption/credit-hour usage metering

## Deferred technical decisions
Exact database schema, tenant implementation, polymorphic relation mechanics, search/indexing technology, event transport, object storage, monitoring-worker deployment and final auth-provider architecture remain implementation decisions.
