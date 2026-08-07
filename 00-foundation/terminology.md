# Re:Solve Terminology

This document defines canonical product language. Feature specs must reuse these terms unless a deliberate Product Bible decision changes them.

## Workspace
The top-level Re:Solve installation boundary. The first deployment has exactly one Workspace even though multi-workspace SaaS behavior is not required.

## Operating Entity
A legal/operational business using Re:Solve to deliver services and issue commercial documents. Airix Media is an Operating Entity in the first deployment, not an ordinary client Organisation.

## Brand
A customer-facing identity belonging to an Operating Entity, controlling approved portal/document/communication identity.

## Principal
Any actor that can receive authorization or perform a Re:Solve action.

Principal types may include Human User, Service Account, API Client, MCP Client, Plugin and Connector.

## User
An authenticated human identity. A User may operate as staff, client member or contractor depending on memberships/grants.

## Organisation
A client, prospect, partner, vendor or other relationship entity represented in Re:Solve.

`Client` is a lifecycle/business relationship state, not a separate database identity from Organisation.

## Contact
A person associated with an Organisation or, where appropriate, acting independently. Contact and User are related but not identical.

## Membership
A User's relationship to an Organisation/Workspace context including role, permissions, status and scope.

## Team
A group of Users used for assignment, routing, ownership, notifications, reporting or access defaults. Team is not an HR employee-management record.

## Account Team
Named operational responsibilities for a client Organisation, such as Account Owner, Technical Owner, Finance Owner or Delivery Owner.

## Role
A named bundle of permissions.

## Permission
A stable capability identifier granted to a Principal under a scope.

Canonical grammar is `domain.action` or `domain.resource.action`.

## Access Grant
An explicit permission/role assignment scoped to a Workspace, Organisation, Property, Project, Vault Item or another protected resource.

## Property
A first-class digital or operational asset that an Organisation owns, operates, publishes, hosts, manages or depends on.

Examples include Website, Journal, OJS Installation, Domain, Server, Hosting, Store and Application.

Properties may be nested and may also have typed relationships.

## Property Type
A configurable classification describing a Property's operational meaning and expected capabilities.

## Property Relationship
A typed relationship such as parent/child, hosted on, published by, domain for, depends on or monitored by.

## Monitoring Signal
A time-bound observation from a native Re:Solve probe or external Monitoring Connector.

## Monitor
A configured native/external check of a Property target.

## Property Posture
A Re:Solve-derived, explainable operational health state assembled from monitoring, renewals, connectors, incidents, backups, application signals and other current evidence.

## Renewal / Expiry Obligation
A first-class obligation to renew, verify or act on an expiring Domain, Hosting service, Certificate, Contract, Client Service, license or other managed dependency.

## Incident
An operational event representing service degradation, outage, security issue or another condition requiring coordinated response.

## Service Catalogue Item
A reusable definition of a service offered by an Operating Entity.

## Client Service
An active service relationship between an Operating Entity and a client Organisation. It may define scope, price, billing cadence, SLA, properties, support entitlement, renewal, owner and status.

Client Service Consumption/credits/hours-used metering is not a core Re:Solve feature.

## Support Entitlement
The support level a client/service/property is entitled to receive, potentially including SLA, channels, categories, business hours and escalation.

## Lead
An early potential commercial relationship that has not matured into a qualified Opportunity. A Lead may exist before a complete Organisation is known.

## Opportunity
A qualified potential sale represented within a Pipeline.

## Pipeline
A configurable sequence of commercial stages.

## Proposal
A first-class commercial record describing an offered solution, scope, terms and/or price before acceptance.

## Estimate / Quote
A priced commercial offer or estimate. Display terminology may vary by deployment while the underlying record remains semantically clear.

## Contract
A first-class commercial agreement record. Signing may be executed through a Signature Connector while Re:Solve retains contract lifecycle and final snapshot references.

## Document Template
A versioned template used by Document Studio to render a supported business document.

## Document Version
A rendered/draft version associated with a business record.

## Final Snapshot
An immutable representation of the exact proposal/estimate/contract or other document content accepted/executed by a recipient.

## Project
A bounded body of work for an Organisation, normally including outcomes, dates, participants, tasks, milestones, deliverables, files and client-facing visibility.

Re:Solve Projects do not include Timesheet/Time Tracking functionality.

## Task
A unit of actionable work assigned to responsible Users/Teams with status, priority, dates, dependencies and context.

## Recurring Task
A recurrence definition that creates ordinary Task occurrences on a controlled schedule.

## Milestone
A significant Project checkpoint or phase boundary.

## Deliverable
A defined output intended for completion, delivery, review or acceptance.

## Client Action
An explicit action required from a client before work can progress/close.

## Request
A structured ask requiring triage before or while it is fulfilled. A Request may convert/link to a Task, Project, Change Request, Approval, Opportunity/Estimate, Chatwoot support conversation, Vault access request or other record.

## Approval
A structured decision request with outcomes such as approve, reject or request changes.

## Change Request
A structured request to alter agreed project/service scope, timing, deliverables or implementation.

## Reminder
A lightweight future attention instruction for a User, optionally attached to a record.

## Cadence / Activity Plan
A reusable sequence of follow-up steps for Sales, onboarding, renewals or client-success processes, built on shared Automation/Action primitives.

## Invoice
A first-class billing record requesting payment.

## Payment
A confirmed monetary transaction or recorded payment event allocated against invoices/receivables.

## Payment Provider
An external provider that moves/confirms money behind a PaymentConnector capability.

Provider packages may be delivered as Plugins that register Connector implementations.

## Subscription
A recurring commercial billing arrangement owned by Re:Solve and distinct from provider-specific subscription objects.

## Recurring Service
A Client Service with recurring billing/renewal behavior. It does not imply consumption metering.

## Credit Note
A financial record reducing/reversing all or part of an Invoice.

## Receipt
A proof-of-payment document generated from confirmed Payment truth.

## Expense
An operational/client/project/vendor cost record where enabled. Expenses do not imply payroll/HR.

## Support Conversation
A support interaction whose conversation/message truth lives in Chatwoot. Re:Solve retains references/context/summaries/metrics as needed.

## Notification
A durable user-awareness item generated from an event and delivered through one or more channels according to policy/preferences.

## Attention Item
A current condition that still requires awareness/action. Attention remains unresolved until its source condition is resolved, not merely because a Notification was read.

## Domain Event
A structured fact that something meaningful happened in Re:Solve.

## Automation
A configured workflow triggered by event, schedule, manual invocation, webhook, connector condition or another approved trigger, executing controlled actions.

## Action
A registered business operation with permissions, context, risk class, confirmation/approval policy and interface availability.

## Plugin
An installable extension that adds business/product capability through supported extension points.

## Connector
An integration implementation connecting Re:Solve to an external system/provider.

## Connector Type
The reusable provider/capability definition such as Chatwoot, Cloudflare, Bachs or OJS.

## Connector Instance
A configured connection to a specific external account/system/site.

## Connector Mapping
A first-class relationship between a Re:Solve record and an external provider identifier.

## Integration Event
An inbound/outbound external event processed with verification, idempotency, retry, status and audit metadata.

## Data Provenance
Metadata describing a fact's source, authority, freshness, sync/import/run and derived/native status.

## Secure Vault
The protected subsystem for controlled storage/sharing of confidential information and files.

## Vault Item
A protected confidential record such as credential, secret, note, document or file.

A protected confidential document is a Vault Item rather than simultaneously an ordinary File record with a second access path.

## File
A managed ordinary binary/document object with metadata, relationships, storage abstraction and versioning where required.

## Knowledge Article
A structured Re:Solve knowledge record for internal or controlled client use, separate from Chatwoot Support Knowledge.

## Comment
A collaboration item attached to a supported record with explicit visibility.

## Mention
A reference to an authorized User/Team inside Collaboration.

## Follow / Watch
A user's subscription to meaningful updates for a record. Following does not grant access.

## Activity
A human-readable business timeline event. Activity is optimized for understanding.

## Audit Event
An append-only accountability/security record of a consequential action. Corrections create new evidence rather than mutating history.

## Saved View
A saved filter/sort/column/presentation definition that may be private, team-shared, workspace-shared or system-provided.

## Secure External Access
A narrow, revocable, expiring external grant used for a specific document/view/action without requiring a full Portal account.

## API Client
A non-human Principal authorized to use Re:Solve APIs through scoped credentials.

## MCP Client
An AI/agent Principal authorized to access approved Re:Solve MCP tools/resources under explicit scope/audit rules.

## MCP Tool
A controlled Re:Solve operation exposed through Model Context Protocol.

## Àríyá
The user-facing name of Re:Solve's built-in AI operator. Àríyá is independent from Chatwoot Captain.

Internal technical concepts may use AI Provider, AI Profile, AI Run, AI Tool and AI Connector terminology.

## Admin OS
The staff-facing Re:Solve experience.

## Client Portal
The authenticated client-facing Re:Solve experience.

## Product Bible
The canonical specification set defining Re:Solve product truth, behavior, flows, rules, states, acceptance criteria and planned build slices.

## Explicit exclusions
The following are not Re:Solve product domains:
- HR management
- payroll
- recruitment
- leave/attendance
- employee performance reviews
- timesheets/time tracking
- Client Service Consumption/credit-hour usage metering
