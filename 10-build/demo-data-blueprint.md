# Re:Solve Demo Data Blueprint

## Purpose
Demo data is not filler. It must exercise the product's relationships, permissions, states, hierarchy, notifications, and operational workflows so each Lovable slice can be reviewed realistically.

Do not use real credentials, production secrets, or private customer data.

## Demo data principles
- Use realistic but fictionalized Airix-style organisations and properties.
- Prefer a small coherent universe over dozens of unrelated examples.
- Reuse the same organisations, contacts, properties, projects, invoices, support references, files, and notifications across slices.
- Include healthy, warning, blocked, overdue, pending, archived, and empty-state examples.
- Include at least one user with restricted property scope and one client admin with broader organisation scope.
- Vault demo values must be placeholders and must never contain real secrets.

## Canonical demo universe

### Internal operating organisation
**Airix Media**
Purpose: staff/admin side of Re:Solve.

Suggested staff identities:
- Hendrix Nwaokolo — Owner / Platform Administrator
- Ada Eze — Account Manager
- Tunde Bello — Technical Operations
- Kemi Lawal — Finance
- Mariam Yusuf — Project Coordinator

These names are demo-only identities.

## Client organisations

### Kampala University
Client code: `KU`
Status: Active
Relationship owner: Ada Eze
Billing contact: Dr. Sarah Kato
Portal administrators: Dr. Sarah Kato, Peter Mugisha

Properties:
- Kampala University Main Website
- KU Journals
  - Kampala Journal of Arts & Social Sciences
  - Kampala Journal of Business & Management
- ku.ac.ug domain
- Main Hosting Account

Use this organisation to demonstrate hierarchy, OJS-related properties, support context, multiple contacts, projects, billing, monitoring, files, and property-scoped access.

### Meridian Development Review
Client code: `MDR`
Status: Active
Smaller organisation with one primary journal property.
Use for simpler portal and billing scenarios.

### Eastern Research Institute
Client code: `ERI`
Status: Onboarding
Use for first-use/empty-state and incomplete onboarding scenarios.

### Northstar Foundation
Client code: `NSF`
Status: Archived or Former Client
Use for archived records, revoked portal access, completed projects, and historical invoice scenarios.

## Contacts and memberships

### Kampala University
- Dr. Sarah Kato — Organisation Admin, Billing Contact, Project Approver
- Peter Mugisha — Technical Contact, Organisation Admin
- Grace Nambasa — Journal Manager, access limited to KU Journals subtree
- Daniel Okello — Finance Contact, billing visibility only
- Lydia Achieng — Journal Editor, access limited to one child journal

Demonstrate:
- one contact with multiple roles
- one contact with restricted property access
- one contact with no billing access
- one contact with no Vault access

## Property hierarchy example

```text
Kampala University
├── Kampala University Main Website
├── KU Journals
│   ├── Kampala Journal of Arts & Social Sciences
│   └── Kampala Journal of Business & Management
├── ku.ac.ug Domain
└── Main Hosting Account
```

Suggested property health:
- Main Website — Healthy
- KU Journals — Healthy
- KJASS — Warning: plugin update/maintenance due
- KJBMS — Degraded: slow response or certificate warning
- Domain — Renewal due within 30 days
- Hosting — Healthy

## Projects

### KU Main Website Redesign
Status: Active
Progress: ~65%
Milestones:
- Discovery — complete
- Design — complete
- Development — active
- Content migration — blocked by client
- Launch — upcoming

Include:
- overdue client action
- upcoming milestone
- one approved deliverable
- one deliverable awaiting review
- one change request
- one risk

### KJASS OJS Upgrade
Status: Active
Property: KJASS
Include:
- technical checklist
- backup milestone
- staging validation
- client approval gate
- release window

### MDR Journal Setup
Status: Completed
Use for completed project views and historical activity.

## Sales and commercial

Opportunities:
- KU Annual Support Renewal — Negotiation
- ERI Journal Platform Setup — Proposal Sent
- MDR Publishing Support Expansion — Qualified

Proposals/estimates:
- one draft
- one sent
- one accepted
- one expired

Contracts:
- one active
- one awaiting signature
- one historical

## Service catalogue
Suggested services:
- Managed Website Support
- Managed OJS Support
- OJS Upgrade Service
- Website Redesign
- Domain Management
- Hosting Management
- Monitoring & Maintenance
- Journal Setup

Recurring service instances:
- KU Managed Website Support — Active
- KU OJS Support — Active
- KU Domain Management — Renewal Upcoming
- MDR OJS Support — Active

## Billing

Invoices:
- one draft
- one issued and unpaid
- one partially paid
- one overdue
- one paid
- one void/cancelled where supported

Payments:
- verified provider payment
- bank/offline payment awaiting reconciliation
- failed provider attempt

Receipts:
- one generated from verified payment

Credit note:
- one applied to a historical invoice

Do not hard-code a specific gateway into core records.

## Support references
Chatwoot remains source of truth.

Demo Re:Solve support context should include references such as:
- KU Main Website — resolved outage conversation
- KJASS — open support conversation about submission email delivery
- KJBMS — waiting on client response

Store only safe reference/context data needed by Re:Solve demo surfaces.

## Notifications
Create a diverse notification set:
- task assigned
- approval requested
- approval completed
- invoice due soon
- payment received
- project milestone upcoming
- client action overdue
- property warning
- domain renewal reminder
- connector degraded
- Vault access request
- mention

Priorities should span informational to critical.

## Approvals
Examples:
- Homepage design deliverable — approved
- KJASS production upgrade window — pending
- KU contract renewal proposal — pending
- Vault access request — pending

## Files
Normal files:
- project brief
- content migration spreadsheet
- invoice PDF
- meeting notes
- brand assets

Sensitive files should instead be represented in Vault metadata.

## Secure Vault
Demo metadata only:
- WordPress Admin Credential — KU Main Website
- OJS Server SSH Access — KU Journals
- Domain Registrar Access — ku.ac.ug
- Signed Support Contract — Kampala University
- Confidential Renewal Proposal — Kampala University

Secret values must be obviously fake placeholders and should not be included in screenshots or generic search indexing.

## Knowledge
Re:Solve internal/client knowledge examples:
- OJS Upgrade Standard Operating Procedure
- Client Launch Checklist
- Domain Renewal Procedure
- KU Website Editorial Workflow — client-visible
- KJASS Production Checklist — property-scoped

Chatwoot support KB content is not duplicated here.

## Monitoring
Signals:
- healthy uptime check
- slow response warning
- certificate nearing expiry
- domain renewal approaching
- recent successful backup
- failed backup requiring attention
- maintenance window scheduled

## Connector instances
Demo instances:
- Chatwoot — Airix Media managed support
- WhatsApp/Baileys — operational messaging
- Bachs — payment provider
- OpenRouter — Re:Solve AI
- Uptime Kuma — monitoring
- Documenso — signatures
- Kampala University OJS
- MDR OJS
- Airix Media WordPress

Credentials must be represented as secure references only.

## Permission test identities

### Staff Owner
Can administer all domains.

### Account Manager
Can manage assigned clients/projects but cannot administer platform security or reveal all Vault items.

### Finance User
Can view/manage billing but has limited project/support access.

### Technical Operator
Can manage properties/monitoring and request Vault access.

### Client Organisation Admin
Can administer client users and approved organisation-level records.

### Client Property User
Can access one property subtree only.

### Client Billing User
Can view billing but not project technical details or Vault.

## Slice data policy
Each build slice should seed only the minimum subset necessary for that slice, but use IDs/names consistent with this blueprint so later slices compose into one coherent demo environment.

## Reset behavior
Development should support resetting demo data to a known state without touching developer/system configuration.

## Data safety
Never seed:
- real passwords
- real API keys
- real client personal data
- real financial account identifiers
- real production webhook secrets
- confidential production documents
