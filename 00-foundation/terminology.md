# Re:Solve Terminology

This document defines canonical product language. Feature specs and implementation must reuse these terms unless a later deliberate Product Bible decision changes them.

## Workspace
Top-level Re:Solve installation boundary. The first deployment has exactly one Workspace.

## Operating Entity
Legal/operational business using Re:Solve to deliver services and issue commercial documents. Airix Media is an Operating Entity in the first deployment, not an ordinary client Organisation.

## Brand
Customer-facing identity belonging to an Operating Entity, controlling approved Portal/document/communication identity.

## Principal
Any actor that can receive authorization or perform a Re:Solve action: Human User, Service Account, API Client, MCP Client, Plugin or Connector.

## User
Authenticated human identity. A User may operate as staff, client member or contractor depending on grants/Memberships.

## Organisation
Client, prospect, partner, vendor or other relationship entity. `Client` is a relationship/lifecycle state, not a separate identity from Organisation.

## Contact
Canonical business person record associated with one or more Organisations. Contact and User are related but not identical.

## Membership
A User's access relationship to an Organisation/Workspace context including role/capabilities, state and scope. Portal Membership is normally invited at commercial commitment, usually Proposal acceptance.

## Team / Account Team
Team groups Users for assignment/routing/ownership/access defaults. Account Team represents named client responsibilities. Neither is HR.

## Role / Permission / Access Grant
Role is a permission bundle. Permission uses canonical `domain.action` or `domain.resource.action`. Access Grant scopes capability to a protected context.

## Property
First-class digital/operational asset an Organisation owns, operates, publishes, hosts, manages or depends on: Website, Journal, OJS installation, Domain, Server, Hosting, Store, Application, etc.

## Property Type / Relationship
Configurable classification and typed relationship between Properties.

## Monitor / Monitoring Signal
Monitor is a configured native/external check. Monitoring Signal is a time-bound observation with source/freshness/evidence.

## Property Health / Property Posture
Re:Solve-derived explainable operational health assembled from Monitoring, renewals, Incidents, backups, application/Connector signals and other current evidence. `Property Health` is the business-readable concept; `Posture` may be used for the richer evidence model.

## Renewal / Expiry Obligation
First-class obligation to renew, verify or act on an expiring Domain, Hosting service, Certificate, Contract, Client Service, license or dependency.

## Incident
Operational event representing degradation/outage/security/other coordinated response with evidence and start/recovery lifecycle.

## Service Catalogue Item
Reusable product/service offering. It may define pricing basis, price/currency, tax, renewal behavior, default Project template, Support Entitlement and Property applicability.

## Pricing Basis
How a Catalogue/Proposal/Invoice line is measured:
- `flat` — fixed amount;
- `quantity` — quantity × unit price;
- `duration` — duration × rate.

Duration units include at least day, week, month, quarter and year. Duration pricing does not itself imply recurrence.

## Price Book / Rate Card
Effective-dated reusable pricing for Catalogue items by Operating Entity/client class/Organisation.

## Service Package
Commercial bundle/option composed from Catalogue items.

## Client Service
Active/client-specific service relationship between an Operating Entity and Organisation, with scope, price, Properties, Support Entitlement, renewal and status. No consumption-hours/credits meter exists.

## Recurring Arrangement
Recurring commercial/operational relationship such as hosting, maintenance or retainer, with cadence, dates, linked services/properties and billing/renewal behavior. It is distinct from one-time duration pricing and from a provider subscription mapping.

## Support Entitlement
Support level/scope a client/service/property is entitled to receive, potentially including SLA, channels/categories/business hours/escalation.

## Lead
Early potential commercial relationship before a qualified Opportunity.

## Opportunity
Qualified potential sale within a Pipeline.

## Pipeline
Configurable sequence of Opportunity stages.

## Proposal
**The single canonical commercial-offer record.** It may contain narrative scope, pricing, options, terms and acceptance evidence.

A Proposal may be rendered in detailed, quote-style or estimate-style presentation. `Quote` and `Estimate` are not separate current first-class records/modules.

## Quote / Estimate
Deprecated as separate product domains. These words may remain as client-facing presentation labels, import aliases or historical terminology for a Proposal.

## Proposal Revision / Decision
Versioned sent Proposal content and the exact accepted/declined evidence tied to one immutable revision.

## Contract
First-class commercial agreement record. Re:Solve retains lifecycle/final signed snapshot; counterparty signing may use a SignatureConnector.

## Commercial / Invoice Adjustment
Explicit amount-due change such as late fee, penalty, service charge, approved correction, write-off or other policy-based adjustment. It is separate from Payment.

## Document Template / Template Version
Reusable versioned Document Studio rendering definition.

## Document Draft / Version
Rendered/reviewable document representation tied to an authoritative business record.

## Final Signed PDF Snapshot
Immutable exact issued PDF including document/business revision, Template/Brand version, issuer/signatory snapshot, issue timestamp, cryptographic hash, verification reference and counterparty-signature evidence where required.

Every final generated PDF has issuer signature. Draft previews may remain unsigned and visibly marked DRAFT.

## Staff HTML Email Signature
Sanitized personal HTML signature configured on a staff User profile for email composition.

## Staff Document/PDF Signature
Separate staff profile signature asset/name/title/authorization used for official PDF issuer signing. It is not the email signature.

## Project
Bounded body of delivery work for an Organisation including dates, participants, Tasks, Milestones, Deliverables, Files and client visibility. No Timesheet/work timer exists.

## Project Template
Reusable Project delivery blueprint for Milestones, Tasks, Approvals, defaults and supporting context.

## Task
Canonical unit/surface for actionable human work. **`My Work` is deprecated product terminology.** Personal views such as Focus/Today/Overdue are Task/work projections.

## Recurring Task
Definition that creates ordinary Task occurrences on a controlled schedule.

## Milestone / Deliverable / Client Action
Project checkpoint, defined output, or explicit client dependency.

## Request
Structured ask requiring triage/fulfilment and potentially linking/converting to Task, Project, Change Request, Approval, Opportunity/Proposal, Support or another authoritative record.

## Approval / Change Request
Structured decision request and structured change to agreed Project/Service scope/timing/deliverables.

## Form Template / Form Version
Reusable structured form definition and immutable historical version.

## Form Request / Assignment
A specific request for a recipient to complete a Form in a particular Organisation/Project/Property context with due/expiry/access conditions.

## Submission
Submitted answers and Files tied to the exact Form Version and provenance.

## Review Request
Operational request asking a client/contact for feedback or an external review, with destination/reminders/evidence. Completion is only recorded when supported by evidence.

## Reminder / Cadence
Future attention instruction and reusable follow-up sequence.

## Invoice
First-class receivable requesting payment.

## Payment
Confirmed monetary transaction/evidence allocated against receivables. Payment is not mutated to represent late fees/penalties/discounts.

## Payment Provider / PaymentConnector
External provider behind provider-neutral payment capability.

## Billing Schedule / Provider Subscription Mapping
Recurring Billing behavior and optional mapping to an external provider subscription.

## Credit Note / Refund / Receipt
Financial correction, returned-money record and proof-of-payment document generated from verified Payment truth.

## Expense
Operational/client/project/vendor cost record where enabled. No payroll/employee assumption.

## Connected Mailbox
Provider-neutral configured email mailbox/inbox with declared inbound/outbound/sync authority.

## Communication Thread / Message
Record-linked inbound/outbound communication carrying external message/thread identity and provenance.

## Inbox Triage
Uncertain/unrouted inbound Communications awaiting confirmation/routing, often with Ariya classification evidence.

## Support
Re:Solve's provider-neutral support/case/context domain. Portal human live conversation bridges through Chatwoot according to `Portal -> Ariya -> Chatwoot -> Ariya -> Client`.

## Chatwoot
External conversation/human-support transport. Chatwoot Captain remains separate from Ariya.

## Notification
Durable awareness item delivered through configured surfaces/channels.

## Attention Item
Current condition that still requires awareness/action. Reading a Notification does not resolve Attention.

## Domain Event / Automation / Action
Structured fact; configured workflow; and registered business operation with permissions/risk/confirmation/Approval policy.

## Watch
Ariya/Automation mode that continuously observes an explicit condition and reacts according to registered policy. A user's Follow/Watch subscription to record updates may still be described contextually; it never grants access.

## Plugin / Connector
Plugin adds product/business capability. Connector integrates an external system/provider.

## Data Provenance
Metadata describing source, authority, freshness, sync/import/run and derived/native/AI state.

## Secure Vault / Vault Item
Protected subsystem/item for confidential credentials, secrets, notes, documents or files. A protected document must not retain an ordinary File bypass.

## File / File Request
Ordinary managed binary/document and a structured request for an authorised recipient to upload one or more Files.

## Knowledge Article
Structured Re:Solve Knowledge record for internal/client use, separate from Chatwoot support Knowledge.

## Comment / Internal Note / Mention / Follow
Collaboration primitives with explicit audience/scope. Following never grants authority.

## Activity
Human-readable business timeline event.

## Audit Event
Append-only accountability/security evidence. Corrections create subsequent evidence rather than rewrite history.

## Saved View
Saved filter/sort/column/presentation definition with private/team/workspace/system visibility.

## Secure External Access
Narrow, revocable, expiring external grant for a specific document/Form/File/action without requiring full Portal account.

## API Client / MCP Client / MCP Tool
Scoped machine Principals and curated Model Context Protocol operations.

## Ariya (Àríyá)
Re:Solve's built-in intelligence fabric and user-facing AI operator. Ariya can **Ask, Draft, Act, Watch, Investigate and Recommend** within caller authority and source evidence. It is independent from Chatwoot Captain.

## Setup Mode / Installation State
First-run guarded product workflow/state used to bootstrap the initial Owner/Workspace/Operating Entity and verify dependencies. Successful setup becomes locked and cannot be casually reopened.

## Admin OS / Client Portal
Staff-facing and authenticated client-facing Re:Solve experiences. The Portal is not a reduced Admin clone.

## Product Bible
Canonical specification set defining product truth, behavior, flows, rules, states, acceptance criteria and build/phase governance.

## Explicit exclusions
Not current Re:Solve product domains: HR management, payroll, recruitment, leave/attendance, employee performance reviews, Timesheets/Time Tracking/work timers, Client Service Consumption/credit-hour metering, or the distant-future CMS during the current development run.
