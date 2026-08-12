# Re:Solve Domain Model

## Purpose
This document defines the conceptual Re:Solve domain model without locking database schema, ORM or backend framework.

## Domain map

```text
Workspace
├── Operating Entities / Brands
├── Principals / Roles / Access Grants
├── Human Users / Teams
├── Organisations / Contacts / Memberships
│   ├── Opportunities
│   ├── Properties / Property Health
│   ├── Client Services / Recurring Arrangements
│   ├── Projects / Tasks / Requests / Approvals
│   ├── Proposals / Contracts
│   ├── Billing / Adjustments / Payments
│   ├── Forms / Form Requests / Submissions
│   ├── Communications
│   ├── Files / Vault / Knowledge
│   └── Portal Access
├── Attention / Notifications / Activity / Audit
├── Documents / Signed PDF Snapshots
├── Monitoring / Renewals / Incidents
├── Automations / Actions / Reminders / Calendar
├── Saved Views / Custom Fields / Taxonomy
├── Imports / Exports / Data Quality
├── Plugins / Connectors / API / MCP
├── Ariya / AI
└── System Configuration / Installation State
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
Links a User to an Organisation with state, role/capabilities and scope. Canonical lifecycle is conceptually `invited -> active -> suspended -> revoked`; no Membership exists before invite.

Portal Membership is normally invited after Proposal acceptance/commercial commitment. A Contact is not a Portal identity by itself.

### Team / Role / Permission / Access Grant
Operational grouping and scoped authorization. These are access/work concepts, not HR records.

## 3. Organisation and CRM
### Organisation
Central relationship entity representing prospect, client, partner, vendor or another organisation.

### Contact
Canonical person associated with one or more Organisations through explicit relationships.

### Lead
Early commercial lead that may exist before complete Organisation/Contact records are established.

### Opportunity / Pipeline / Stage
Qualified commercial opportunity and its configurable sales process.

### Account Team Assignment
Named business responsibility such as Account Owner or Technical Owner. Not HR.

## 4. Property, Monitoring and Operations
### Property
First-class digital/operational asset owned by one Organisation.

### Property Relationship / Access Grant
Typed relationships and scoped access.

### Monitor
Configured native/external check definition.

### Monitoring Signal
Observed result with source, timestamp, freshness and evidence.

### Property Health / Posture
Derived explainable current health assembled from monitoring signals, obligations, incidents and connector evidence.

### Renewal / Expiry Obligation
First-class obligation for Domain, Hosting, Certificate, Service, Contract, license or another managed dependency.

### Maintenance Window
Planned operational maintenance/suppression context.

### Incident
Operational service-impact event related to one or more Properties/signals/support references, with start/recovery/duration/evidence.

## 5. Service Catalogue and recurring relationships
### Service Catalogue Item
Reusable service/product offering.

Key commercial dimensions may include:
- name/code/category;
- descriptions;
- pricing basis: `flat`, `quantity`, or `duration`;
- default amount/currency;
- quantity unit where applicable;
- duration unit/default duration where applicable (`day`, `week`, `month`, `quarter`, `year`);
- tax behavior;
- renewal/recurring eligibility;
- default Project/onboarding template;
- Support Entitlement;
- Property applicability.

### Price Book / Rate Card
Reusable effective-dated pricing for an Operating Entity, client class or specific Organisation. Accepted historical pricing remains stable.

### Service Package
Commercial bundle/option composed from Catalogue items while activation can still create clear underlying Client Service relationships.

### Client Service
Client-specific service relationship linking Organisation, Catalogue item, Properties, Proposal/Contract, price/currency, Support Entitlement, delivery and renewal.

### Recurring Arrangement
Commercial/operational recurrence such as maintenance, hosting or retainer. It defines frequency, effective dates, linked service lines, next billing/renewal behavior and lifecycle. It is distinct from a duration-priced one-time line and from an external provider subscription mapping.

### Service Entitlement
Defines included rights/scope/SLA, not usage-credit consumption.

## 6. Projects and Delivery
### Project
Bounded body of work linked to Organisation, Properties, Client Services and relevant commercial/billing records.

### Project Template
Reusable delivery blueprint for Milestones, Tasks, Approvals, default durations, visibility and contextual resources.

### Task / Recurring Task Definition
Canonical actionable human work. The former `My Work` concept is not a separate domain; personal views are Task/work projections.

### Milestone / Deliverable / Client Action
Delivery checkpoints, outputs and explicit client dependencies.

### Approval Request / Approval Decision
Generic approval workflow and evidence.

### Change Request / Risk / Issue
Structured delivery-change/risk records.

### Expense
Operational/project/client cost record. No labor-time costing is required.

## 7. Requests and Forms
### Request
Structured ask awaiting/under triage or fulfilment.

### Request Type
Configurable request classification/intake behavior.

### Form Template / Form Version
Reusable structured form definition and immutable version lineage.

### Form Request / Assignment
Specific invitation/assignment of a Form to a recipient/context with related Organisation/Project/Property, due date, expiry and access mode.

### Submission
Submitted answers and linked Files, preserving the exact Form Version and provenance.

### Form Mapping / Routing
Explicit mapping from Submission data into authoritative domain records through validation/Action Registry/Automation.

Forms power discovery, Project questionnaires, onboarding, surveys, feedback, review requests and other structured intake without becoming a shadow CRM/Project engine.

## 8. Commercial domain
### Proposal
The single first-class commercial-offer record. `Quote` and `Estimate` are presentation styles/migration aliases, not separate current domains.

A Proposal may contain narrative sections, scope, deliverables, options/packages, line items, optional items, flat/quantity/duration pricing, discounts, taxes, terms, validity, attachments, comments and acceptance evidence.

### Proposal Revision / Decision
Sent commercial content is versioned. Acceptance/decline applies to an exact immutable revision and stores decision evidence/snapshot.

### Contract
Agreement lifecycle/metadata linked to Organisation, Proposal, Services, Project and Billing as appropriate.

### Commercial Approval
Approval for exceptional discounts, payment terms, high-risk actions or nonstandard commercial conditions.

## 9. Documents and signatures
### Document Template / Template Version
Reusable Operating Entity/Brand-aware structure and variable contract.

### Document Draft / Document Version
Rendered editable/review representation tied to authoritative business data.

### Final Signed PDF Snapshot
Immutable exact issued PDF containing/storing:
- business/document reference;
- rendered bytes/version;
- template/brand version;
- issuer/signatory and title;
- immutable signature snapshot;
- issued timestamp;
- cryptographic hash;
- verification reference/code;
- recipient/delivery evidence;
- counterparty signatures where required.

Every final generated PDF is issuer-signed. Counterparty e-signature is additional where the business record requires it.

### Staff Email Signature / Staff Document Signature
Separate profile configurations. HTML email signature does not double as PDF signature.

### Signature Envelope Reference
Optional external SignatureConnector transaction for counterparty/legal signing or future cryptographic signing integrations.

### Secure External Access Grant
Narrow expiring/revocable guest access to a specific document/action.

## 10. Billing, Adjustments and Spend
### Invoice / Invoice Line
Receivable record and line items. Lines can preserve flat, quantity or duration pricing semantics from Proposal/Service source.

### Invoice/Commercial Adjustment
Append-only or controlled adjustment representing late fee, penalty, service charge, discount correction, credit/write-off or another approved amount-due change. It records type, calculation basis, reason, source, actor and timestamp.

### Payment / Payment Allocation
Confirmed monetary transaction/evidence and allocation. Payment does not carry late fees/penalties as mutations.

### Payment Attempt / Provider Event
Provider lifecycle attempt/event.

### Credit Note / Refund / Receipt
Financial correction/refund/proof-of-payment records.

### Billing Schedule / Provider Subscription Mapping
Recurring financial behavior; distinct from Client Service and Recurring Arrangement.

### Reconciliation Record
Expected-versus-external financial matching.

### Payment Schedule / Deposit
Planned installment/deposit terms linked to Proposal/Contract/Billing.

### Account Statement
Generated from authoritative Billing truth through Document Studio.

### Expense / Recurring Cost
Operational/vendor cost tracking where enabled. No payroll.

## 11. Communications
### Connected Mailbox
Provider-neutral email mailbox/inbox configuration and sync authority.

### Communication Thread / Message
Inbound/outbound business communication with real external identifiers/thread headers, sender/recipients, Organisation/Contact and related-record links, Files and provenance.

### Message Template / Template Version
Declared-variable body content used within universal email composition.

### Sender Identity
Workspace/Operating Entity/Brand/system sender identity.

### Staff HTML Email Signature
Per-staff sanitized HTML signature applied separately from system/Operating Entity signature.

### Delivery Attempt
Provider delivery evidence/retry/failure state.

### Inbox Triage
Uncertain/unrouted inbound communication awaiting classification/linking.

### Review Request
Operational request for client feedback/review with destination, recipient, related record, reminders, click/evidence and status.

### Announcement
Controlled operational notice, not bulk marketing.

Portal live chat uses Ariya and Chatwoot rather than a duplicate Communication-message console.

## 12. Support operations
Re:Solve owns its provider-neutral Support records/context and may bridge human live conversation through Chatwoot. Ariya can classify/route inbound email or Portal chat into Support under policy. Chatwoot Captain remains a separate system AI.

## 13. Notification, Attention, Collaboration and Activity
Notification = awareness/delivery. Attention = unresolved actionable condition. Comment/Internal Note/Mention/Follow = collaboration. Activity = readable timeline. All remain distinct from Audit.

## 14. Files and Vault
File/File Version/File Link/File Request/Share represent ordinary managed files. Vault Item/Secret Version/Vault File/Grant/Access Event represent protected confidential content. Protected content must not retain an ordinary bypass path.

## 15. Knowledge
Knowledge Space, Article, Category, Revision, Source and Access Policy. Re:Solve Knowledge remains separate from Chatwoot support Knowledge.

## 16. Actions, Automations, Reminders and Calendar
Action Definition centralizes consequential operations across UI/API/MCP/Ariya/Automations. Automation Workflow/Run, Reminder, Cadence, Scheduled Job and Calendar/Event provide orchestration/time context.

## 17. Views and extensibility
Saved View, Favorite/Recent, Custom Field Definition/Value, Tag/Taxonomy and controlled future custom/plugin records extend the OS without replacing core domains.

## 18. Data provenance, import and quality
Provenance Metadata, Import/Migration Batch, Export Job, Data Quality Issue and Merge Record preserve source/authority/freshness and audited reconciliation.

## 19. Plugin, Connector, API and MCP
Plugins add capability. Connectors integrate external systems. API/MCP expose curated scoped resources/actions; neither grants arbitrary SQL/Vault access.

## 20. Ariya / AI
AI Provider Configuration/Profile/Session/Tool/Run/Usage records support Ariya.

Ariya is the intelligence fabric across authorised domains with operating modes Ask, Draft, Act, Watch, Investigate and Recommend. It consumes controlled tools/evidence and never expands caller authority.

## 21. Setup and System
### Installation / Setup State
Tracks uninitialized/in-progress/locked setup state, migration/readiness checks and bootstrap evidence. Successful setup locks bootstrap ownership creation.

### System Health / Job / Worker / Backup / Update records
Support ongoing operations after installation.

## 22. Audit
Audit Event is append-only accountability/security evidence with actor Principal, action, target, scope/context, timestamp, source/interface, correlation, summarized change and outcome.

## 23. Settings
Typed/scoped definitions rather than an unstructured global blob. Scopes may include Workspace, Operating Entity, Brand, user profile, Organisation default, Property Type, plugin or connector instance.

## Cross-domain principles
- Organisation is the major relationship root for clients/prospects/vendors.
- Operating Entity represents the business doing the work.
- Property is the major operational asset context.
- Proposal is the canonical commercial offer.
- Tasks is the canonical human work surface/domain.
- Payment is transaction evidence; adjustments change amount due separately.
- every issued PDF is signed and immutable.
- Ariya consumes authorised truth across the OS and acts only through controlled capabilities.
- external identifiers live in mappings; provider SDK concepts stay behind Connectors.
- derived/synced/AI data exposes provenance/freshness where material.

## Explicit exclusions
Do not create core domains for HR, payroll, attendance/leave/recruitment, employee performance management, Timesheets/Time Tracking/work timers, Client Service Consumption/credit-hour usage metering, or the distant-future CMS during the current run.
