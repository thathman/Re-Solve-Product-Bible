# Re:Solve Demo Data Blueprint

## Purpose
Demo data is not filler. It exercises relationships, permissions, states, hierarchy, notifications, Attention, monitoring, documents and operational workflows realistically.

Never use real credentials, production secrets, private customer data or identifiable real client/staff fixtures.

## Principles
- Airix Media may be used as the first Operating Entity because it represents the intended deployment context.
- All demo people and external client Organisations are fictional.
- Prefer one coherent fictional universe over unrelated filler.
- Reuse names/IDs across slices.
- Include healthy, warning, blocked, overdue, pending, archived, stale and empty-state examples.
- Include a restricted client user and broader organisation admin.
- Vault values are obviously fake placeholders and are never indexed generically.

## Workspace
**Re:Solve Demo Workspace**

## Operating Entity
**Airix Media**

Brand: Airix Media
Default currency/configuration may be chosen for development examples without implying core jurisdiction lock-in.

## Staff demo identities
- Amina Bello — Owner / Platform Administrator
- Chidi Okafor — Account Manager
- Tosin Adeyemi — Technical Operations
- Ifeoma Obi — Finance
- Mariam Sule — Project Coordinator

These identities are fictional.

## Client Organisations

### Westbridge University
Client code: `WBU`
Status: Active
Relationship owner: Chidi Okafor

Contacts:
- Dr. Nneka Okorie — Organisation Admin, Billing Contact, Project Approver
- Samuel Mensah — Journal Manager, restricted to Journals subtree
- Fatima Sani — Technical Contact
- Kojo Boateng — Finance Contact, billing visibility only
- Amara Eze — Editor, restricted to one Journal Property

Properties:
```text
Westbridge University
├── Main Website
├── WBU Journals
│   ├── Westbridge Journal of Social Research
│   └── Westbridge Business Review
├── westbridge.example Domain
└── Primary Hosting
```

Suggested posture:
- Main Website — Healthy
- WBU Journals — Healthy
- Social Research Journal — Attention: maintenance/update due
- Business Review — Degraded: slow response/certificate warning
- Domain — Renewal due within 30 days
- Hosting — Healthy

### Meridian Research Review
Client code: `MRR`
Status: Active
Smaller organisation with one journal Property. Use for simple Portal/Billing scenarios.

### Eastfield Research Institute
Client code: `ERI`
Status: Onboarding
Use for incomplete onboarding, credential/file requests and first-use states.

### Northstar Civic Foundation
Client code: `NCF`
Status: Former/Archived
Use for offboarding, revoked Portal access, historical documents/invoices and completed projects.

## Permission test identities
- Staff Owner — broad administration.
- Account Manager — assigned client/project management without platform-security or broad Vault reveal.
- Finance User — billing focus with limited technical access.
- Technical Operator — Properties/Monitoring with scoped Vault access/request capability.
- Client Organisation Admin — organisation-level client administration.
- Client Property User — one Property subtree only.
- Client Billing User — Billing but no technical/Vault access.

## Projects

### Westbridge Main Website Redesign
Status: Active
Progress: about 65 percent.

Milestones:
- Discovery — complete
- Design — complete
- Development — active
- Content Migration — blocked by client
- Launch — upcoming

Include overdue Client Action, upcoming milestone, approved Deliverable, Deliverable awaiting review, Change Request and Risk.

### Social Research Journal Platform Upgrade
Status: Active
Property: Westbridge Journal of Social Research

Include backup milestone, staging validation, client approval gate and release window.

### Meridian Journal Setup
Status: Completed
Use for completed/history states.

No demo Timesheets or Time Entries.

## Requests
Examples:
- Westbridge: `Update editorial board page` — triage -> accepted Task.
- Westbridge: `Add new journal` — triage -> Opportunity/Project planning.
- Eastfield: `Provide onboarding credentials` — waiting on client.
- Meridian: `Change billing contact` — completed.

## Sales/commercial
Opportunities:
- Westbridge Annual Support Renewal — Negotiation
- Eastfield Journal Platform Setup — Proposal Sent
- Meridian Publishing Support Expansion — Qualified

Proposal/estimate states:
- draft
- sent
- accepted
- expired

Contracts:
- active
- awaiting signature
- historical/executed

## Document Studio
Demo documents:
- Westbridge Annual Support Proposal — sent, secure external link
- Eastfield Journal Setup Estimate — accepted
- Westbridge Support Contract — executed through demo SignatureConnector reference
- project status report
- account statement

Accepted/executed examples have immutable Final Snapshot metadata.

## Services
Catalogue:
- Managed Website Support
- Managed Journal Platform Support
- Platform Upgrade Service
- Website Redesign
- Domain Management
- Hosting Management
- Monitoring & Maintenance
- Journal Setup

Client Services:
- Westbridge Managed Website Support — Active
- Westbridge Journal Platform Support — Active
- Westbridge Domain Management — Renewal Upcoming
- Meridian Journal Support — Active

Do not seed Client Service Consumption/remaining-hours/credits.

## Billing
Invoices:
- draft
- issued/unpaid
- partially paid
- overdue
- paid
- void/cancelled where supported

Payments:
- verified provider payment
- offline/bank payment awaiting reconciliation
- failed provider attempt

Receipts:
- generated from verified payment

Credit note:
- applied to historical invoice

Payment schedule:
- one proposal/contract with deposit + milestone payment plan

Do not hard-code a payment gateway into core records.

## Operational spend
Examples:
- domain renewal vendor cost
- hosting recurring vendor cost
- project billable stock-image/service expense

No payroll/employee expense-management assumptions.

## Support references
Chatwoot remains truth.

Safe Re:Solve references:
- Westbridge Main Website — resolved outage conversation
- Social Research Journal — open email-delivery support conversation
- Business Review — waiting on client

Do not seed full duplicate support message history.

## Monitoring and Property Posture
Native demo signals:
- successful HTTP check
- slow response warning
- certificate nearing expiry
- consecutive-failure outage/recovery sequence
- domain renewal approaching
- heartbeat/backup stale example
- maintenance window

External signal examples:
- Cloudflare connected zone/registration state
- optional Uptime Kuma source marked external/optional

Connector failure and confirmed target outage must be separate states.

## Renewals
Examples:
- westbridge.example Domain — expires in 25 days, auto-renew unknown/client decision needed
- Primary Hosting — expires in 70 days
- Support Contract — renewal in 60 days
- certificate — expires in 18 days

## Attention
Include:
- overdue client action
- pending approval
- overdue invoice
- domain renewal
- degraded Property
- stale backup/heartbeat
- connector authentication issue
- Vault access request
- onboarding blocker
- proposal expiring

## Notifications
Diverse events spanning informational to critical:
- task assigned
- approval requested/completed
- invoice due/payment received
- project milestone
- client action overdue
- Property warning/outage/recovery
- renewal reminder
- connector degraded
- Vault request
- mention

## Approvals
- Homepage Deliverable — approved
- production upgrade window — pending
- support renewal Proposal — pending
- Vault access request — pending

## Files
Ordinary:
- project brief
- content migration spreadsheet
- invoice PDF
- meeting notes
- brand assets

Protected content belongs in Vault instead of retaining ordinary File access.

## Secure Vault
Metadata-only demo items:
- Website Admin Credential — Westbridge Main Website
- Journal Server Access — WBU Journals
- Domain Registrar Access — westbridge.example
- Signed Support Contract — Westbridge University
- Confidential Renewal Proposal — Westbridge University

All secret values are obviously fake development placeholders.

## Knowledge
- Journal Platform Upgrade SOP
- Client Launch Checklist
- Domain Renewal Procedure
- Westbridge Website Editorial Workflow — client-visible
- Social Research Production Checklist — Property scoped

Do not duplicate Chatwoot support KB.

## Collaboration
Examples:
- internal note on an at-risk Project
- client-visible comment on a Deliverable
- mention of Account Manager on renewal
- followed Property/Incident

## Saved views
Examples:
- My Active Clients
- Properties Needing Attention
- Renewals Next 30 Days
- Overdue Invoices
- Projects Waiting on Client

## Data quality
Examples:
- possible duplicate Contact
- stale Connector mapping
- missing renewal owner
- expired Portal invitation

## Connector instances
- Chatwoot — managed support
- WhatsApp/Baileys — operational messaging
- Bachs-style demo payment provider instance without real credentials
- OpenRouter-style AI provider reference
- Cloudflare — domain/DNS/health
- Documenso — signatures
- Westbridge Journal Platform connector
- Airix Media WordPress demo
- optional Uptime Kuma demo source for connector compatibility only

Credentials are secure references.

## Slice data policy
Each build slice seeds only the subset needed, while keeping canonical names/IDs consistent so later slices compose into one coherent demo environment.

## Reset behavior
Development supports resetting demo business data to a known state without touching developer/system configuration.

## Never seed
- real passwords/API keys
- real staff/client personal data
- real financial account identifiers
- real production webhook secrets
- confidential production documents
