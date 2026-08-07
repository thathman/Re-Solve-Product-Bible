# Organisations and Contacts

## Purpose
Organisations and Contacts form Re:Solve's relationship spine. They represent external clients, prospects, partners, vendors and the people related to them.

**Operating Entities are separate.** Airix Media/the business operating Re:Solve must not be modeled as an ordinary client Organisation merely to reuse CRM records.

## Core concepts
### Organisation
Client, prospect, partner, vendor, institution or other relationship entity.

### Contact
A person. Contact is not identical to authenticated User.

### Membership
A User's relationship to an Organisation, with role/status/permissions and optional Property scope.

### Relationship / lifecycle state
Examples: Prospect, Onboarding, Active Client, At Risk, Paused, Offboarding, Former/Archived, Partner, Vendor.

Lifecycle state is distinct from Billing/Project/Property state.

### Account Team
Named operational responsibilities such as Account Owner, Technical Owner, Delivery Owner and Finance Owner. These are assignment roles, not HR records.

## Organisation List
Use canonical DataTable/Saved Views.

Useful columns:
- Organisation/reference;
- relationship/lifecycle;
- Account Owner;
- primary Contact;
- active Properties/Projects/Services;
- Client Health;
- outstanding receivable summary;
- next Renewal;
- Support/Incident context;
- last meaningful activity.

Curated views:
- All
- Active Clients
- Prospects
- Onboarding
- Needs Attention
- Renewals
- At Risk
- Former/Archived
- Saved Views

## Organisation 360
### RecordHeader
Name, human reference, relationship state, Client Health/Attention, Account Team, tags and registered actions.

Actions may include add Contact/Property, create Opportunity/Project/Request/Invoice, start onboarding/offboarding, send operational message, share authorized Vault Item or open Support summary.

### Overview
- relationship summary;
- Account Team;
- Client Health reasons/freshness;
- Attention;
- primary Contacts;
- onboarding/offboarding state;
- current Projects/Requests;
- Properties/Posture;
- active Client Services;
- Billing/receivables;
- Renewals;
- Support/Incidents;
- latest meaningful Activity.

### Contacts
Memberships, client roles, Portal state, billing/technical/approver designations and Property scope.

### Properties
Property hierarchy, Posture, Renewals and Incidents.

### Projects / Requests
Current/completed work and structured Requests.

### Commercial
Opportunities, Proposals, Estimates, Contracts and Client Services.

### Billing
Invoices, Payments, Statements, recurring Billing and Credits/Refunds according to permission.

### Support
Provider-neutral Chatwoot context and entitlement.

### Documents / Files / Vault / Knowledge
Respect each platform's access model. Protected documents cannot leak through ordinary Files.

### Collaboration / Activity
Shared Comments/Mentions/Following plus human-readable Activity. Audit remains separate.

### Access
Portal Memberships, invitations, roles and Property grants.

### Connectors / Data Quality
Mappings, provenance/freshness and relevant duplicate/missing-data issues.

## Creation
Keep initial Organisation creation lightweight:
- name;
- relationship type/state;
- owner/Account Team default;
- optional primary Contact/source.

Additional onboarding data can follow later.

Duplicate detection warns using multiple signals such as similar name, domain, billing identity and explicit external mappings. Never silently merge.

## Lead conversion
A Lead may exist before a complete Organisation/Contact exists.

Qualification should:
1. search potential Organisation/Contact matches;
2. let user choose/link/create where ambiguous;
3. preserve Lead/Opportunity provenance;
4. avoid duplicates;
5. keep external identities in mappings.

Email alone is never universal canonical identity.

## Contact Workspace
May include identity/channels, Organisation relationships, Property access, Projects, communication preferences, Portal/access state, Collaboration/Activity and external mappings.

A Contact can relate to multiple Organisations and have multiple email/phone identities.

## Communication and privacy
Operational email/WhatsApp/call/meeting references may appear when policy permits. Chatwoot support message history is not indiscriminately copied.

Contact preferences/consent/data-right workflows follow Privacy specification.

## Client Health
Derived, explainable relationship state informed by relevant evidence such as:
- onboarding blockers;
- Project risk/Client Actions;
- Property Posture/Incidents;
- Renewals;
- Support escalations;
- overdue receivables;
- commercial/service state;
- relationship follow-up.

Do not use an unexplained magic numeric score.

## Relationship Reviews
Periodic client/account review records can summarize Services, Properties, Projects, Renewals, Support, Billing, risks, opportunities and agreed actions.

## Data quality / merge
Data Quality may flag duplicates, stale Contacts, broken mappings, missing Account Team/renewal owner and expired Portal access.

Merge flows preserve relationships, Activity, external mappings, aliases and Audit. Ambiguous records require human review.

## Archive / offboarding
Prefer Archive over destructive deletion where operational/commercial history exists.

Offboarding coordinates access revocation, connector/support/monitoring handover, documents/files/Vault, Billing and retention through Client Lifecycle rather than simply changing one status.

## Permissions
Representative canonical capabilities:
- `organisations.read/create/update/archive/export`
- `organisations.members.manage`
- `contacts.read/create/update/archive`
- `clients.lifecycle.manage`
- `clients.access.manage`
- `clients.finance.read`
- `clients.vault_metadata.read`

Actual scope is always enforced server-side.

## Attention / Notifications / Reminders
Attention examples: onboarding blocked, client health at risk, important follow-up overdue, renewal with no owner, stale Contact/mapping.

Notifications remain for meaningful assignment/access/lifecycle changes. Routine CRUD does not spam users.

Users may create record Reminders and Follow Organisations/Contacts without gaining additional access.

## Automations
Examples:
- Organisation becomes client -> onboarding plan;
- onboarding complete -> Active;
- inactivity threshold -> Reminder/Attention;
- Portal access changed -> appropriate notification/audit;
- offboarding starts -> access review;
- duplicate/import issue -> Data Quality issue.

## API / MCP / Àríyá
APIs expose Organisations, Contacts, Memberships, Account Team, lifecycle summaries, access grants, Activity, custom fields and related summaries with provenance where material.

MCP candidates include search/get/create/update Organisation/Contact, list Organisation Properties, get_client_health, list_client_attention and get_onboarding_status.

Àríyá may create an account briefing with source evidence but cannot expose hidden finance/Vault/internal notes.

## Plugins / Connectors
Plugins may contribute approved tabs/fields/actions/relationships/health signals.
Connectors map external Chatwoot/OJS/WooCommerce/etc. identifiers separately from canonical identity and must declare sync authority.

## Responsive/PWA
Mobile Organisation 360 prioritizes identity, Attention/Health, Contacts, active work, Properties, Renewals and primary actions. Dense details become rows/cards/drill-down. Sensitive identity/access edits are normally online-only.

## Acceptance criteria
- Operating Entity and client Organisation remain distinct;
- one Contact can relate to multiple Organisations without duplication;
- lifecycle/onboarding/offboarding is visible without shadow copies;
- Account Team is operational ownership, not HR;
- Client Health is explainable;
- duplicate detection warns rather than auto-merges;
- Portal/Property access is explicit;
- sensitive related data is permission-gated;
- no HR, Timesheet or Client Service Consumption behavior appears.

## Lovable build slices
1. Organisation list + Saved Views.
2. lightweight create/edit + duplicate warning.
3. Organisation Overview + Account Team/Health demo.
4. Contacts + Memberships.
5. Contact Workspace + multi-Organisation relationships.
6. Properties/Projects/Requests relationships.
7. Billing/Support/Documents/Vault summaries.
8. Access/Portal management.
9. Collaboration/Activity + lifecycle states.
10. Data Quality/merge + mobile/PWA polish.
