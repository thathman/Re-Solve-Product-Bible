# Settings

## Purpose
Settings is the control plane for Re:Solve. It exposes configuration deliberately with ownership, validation, audit, diagnostics, permissions and safe defaults.

Settings must not become a miscellaneous dumping ground. Every setting belongs to a domain, has a scope and defined consequences.

## Information architecture
Top-level Settings groups:
1. General / Workspace
2. Operating Entities & Brands
3. People & Access
4. Client Portal
5. CRM
6. Clients & Lifecycle
7. Properties
8. Monitoring & Renewals
9. Projects
10. Sales & Documents
11. Billing & Spend
12. Support
13. Requests & Forms
14. Notifications
15. Communications
16. Àríyá / AI
17. Vault
18. Files
19. Automations
20. Data & Customization
21. Plugins
22. Connectors
23. API & MCP
24. Security & Privacy
25. System

Settings navigation should be searchable and simple. On desktop use a clear settings sidebar/index; on mobile use an index/drill-down flow rather than another dense permanent sidebar.

## Shared setting contract
Every setting should define:
- scope: Workspace, Operating Entity, Brand, user, team, client default, Property Type, plugin or connector instance;
- current/inherited/default value;
- validation;
- required permission;
- sensitivity;
- immediate/save/review-changes behavior;
- audit requirement;
- whether existing records are affected;
- rollback/recovery where applicable;
- health/diagnostic state.

## Save model
Use:
- immediate save for low-risk personal preferences;
- explicit Save for grouped configuration;
- Review changes for high-impact settings;
- test-before-save for provider connections;
- step-up for highly sensitive changes.

Unsaved material changes must be visible and protected against accidental loss.

## Configuration health
Major sections can report configured, partially configured, needs attention, disabled, degraded or healthy. Settings Home should prioritize action needed rather than show identical cards for every section.

# A. General / Workspace
- Workspace name/code
- locale/timezone/date/number formats
- base/enabled currencies
- default ownership/archive behavior
- system identity
- default record references/numbering links
- default retention links
- feature defaults that do not belong to another domain

One Workspace always exists even when multi-workspace SaaS is not enabled.

# B. Operating Entities & Brands

## Entities
- legal/trading name
- registration/tax identifiers where applicable
- addresses/contact details
- default currency/locale
- commercial/document identity
- billing/remittance identity
- default Brand
- status

## Brands
- logo variants
- favicon/app icon
- approved accent token
- Portal/auth identity
- email identity
- Document Studio theme
- support identity
- sender identity mappings
- accessibility preview

Brand customization cannot override core semantic accessibility.

# C. People & Access

## Staff / Human Users
- active/invited/suspended
- role/team memberships
- last sign-in
- MFA state
- security/session summary
- deactivate/reactivate
- responsibility reassignment before deactivation

This is access administration, not HR. Do not add payroll, leave, attendance, recruitment, employee reviews or Timesheets.

## Teams
- name/purpose
- lead/owner if useful
- members
- assignment/routing eligibility
- access defaults
- notification defaults

## Roles / Permissions
- system/custom roles
- clone/compare
- capability matrix
- high-risk permission warnings
- assigned principals/users
- effective-permission explanation

Canonical permission grammar: `domain.action` or `domain.resource.action`.

## Invitations / Sessions
- expiry/resend/revoke
- default role/team
- active sessions/devices
- revoke/reauthentication
- privileged-action step-up duration

# D. Client Portal
- Portal enabled
- default visible destinations
- Home defaults
- client-safe terminology
- support entry behavior
- Portal announcement/banner
- client roles/permissions
- invitations/self-registration/domain policy
- client-admin invitation rights
- Branding/Operating Entity defaults
- Vault destination shown only when authorized
- Requests destination policy
- optional Portal Àríyá policy

# E. CRM
- lead sources
- pipelines/stages/probability
- activity types
- loss reasons
- cadences/activity-plan defaults
- follow-up/reminder defaults
- segmentation
- import policy
- duplicate matching
- custom fields/taxonomies
- sales forecast defaults

# F. Clients & Lifecycle
- client lifecycle statuses
- onboarding templates
- offboarding templates
- Account Team responsibility labels
- relationship review cadence/defaults
- client-health rules/thresholds
- former-client archive policy

Health must remain explainable rather than opaque scoring.

# G. Properties
- Property Types
- relationship types
- statuses
- client-visible state mapping
- custom fields
- hierarchy/inheritance rules
- maintenance defaults
- archive behavior

# H. Monitoring & Renewals

## Native monitoring
- enabled/default monitor policy
- default intervals/timeouts
- failure/recovery thresholds
- monitor retention
- maintenance behavior
- probe/worker registration policy
- client-notification defaults

## Property Posture
- evidence categories
- posture thresholds/rules
- stale-source policy
- client-safe posture mapping

## Renewals
- obligation types
- reminder windows
- ownership defaults
- unknown auto-renew policy
- verification requirements
- client decision/payment workflow

External sources such as Cloudflare or optional Uptime Kuma are configured under Connectors, not hard-coded here.

# I. Projects
- statuses
- priorities
- task types
- recurring task defaults
- templates
- milestones/deliverable defaults
- approval behavior
- Client Action defaults
- Change Request defaults
- client visibility
- cost/commercial display policy

**No Time Tracking/Timesheet settings exist.**

# J. Sales & Documents

## Service Catalogue
- categories
- pricing models
- default taxes
- billing cadence
- default Project template
- default Support Entitlement
- Property applicability

No Client Service Consumption/allowance-meter settings.

## Proposal / Estimate / Quote
- numbering
- validity/expiry
- templates
- optional/add-on item behavior
- discounts/taxes
- acceptance policy
- Secure External Access policy
- reminders

## Contracts
- numbering
- templates
- SignatureConnector
- signature/expiry/renewal policy
- deposit requirements
- client visibility

## Document Studio
- template management
- brand/entity defaults
- web/PDF output
- A4/Letter defaults
- variable catalogue
- version/final-snapshot policy
- external-view policy
- retention

# K. Billing & Spend

## Invoices
- numbering
- due/payment terms
- line defaults
- notes/terms
- Document Studio template

## Taxes / Currencies
- tax definitions/effective dates
- inclusive/exclusive behavior
- exemptions
- currency/rounding/exchange policy

## Payment providers
Payment capability is connector-based. Show installed/configured PaymentConnector instances with environment, methods/currencies, connection/webhook health and reconciliation behavior.

## Recurring billing / Subscriptions
- cadence
- renewal generation
- pause/cancel timing
- proration/trial only where product requires
- payment failure/grace policy

## Deposits / payment schedules
- deposit defaults
- milestone/installment rules
- conversion to invoice schedule

## Credit control
- overdue thresholds
- reminder/escalation
- account hold/deposit policy where enabled
- client-safe messaging

## Receipts / Credit Notes / Refunds / Statements
- numbering
- templates
- generation/approval
- client notification

## Spend / Expenses
- categories
- approval policy
- billable-expense conversion policy
- recurring vendor cost categories

No payroll/employee expense/HR assumptions.

# L. Support
Chatwoot remains the support engine.

Settings expose Re:Solve-specific:
- Chatwoot connector shortcut/health
- mappings
- Support Plans/Entitlements
- SLA/commercial context
- business hours
- categories/routing context
- client-safe support summary policy
- incident relationship

Do not reproduce Chatwoot's full inbox/agent/team/Captain administration.

# M. Requests & Forms

## Requests
- request types/categories
- statuses
- default owner/team
- Portal/public availability
- triage routing
- conversion options
- SLA/response expectations where applicable

## Forms
- form templates
- public/Portal/secure-link policy
- submission retention
- spam/abuse protection
- file policy
- routing
- mapping into core/custom fields

# N. Notifications
- channels
- event policies
- recipient defaults
- priority
- grouping/dedupe
- templates
- digests
- quiet hours
- mandatory events
- retries/failure
- retention
- Test Center

Attention is configured separately by domain rules; reading Notifications does not resolve Attention automatically.

# O. Communications

## Email
- provider connector
- sender identities
- from/reply-to
- verification/health
- test
- delivery/bounce diagnostics

## WhatsApp/Baileys
- instance/session
- approved operational categories
- destination/eligibility policy
- quiet hours
- retry/media policy
- test/reconnect
- audit

Not a client-customer support inbox.

## SMS
Optional connector.

## Announcements
- audience defaults
- allowed channels/surfaces
- expiry
- client/staff policy

Bulk marketing/campaign configuration belongs to specialist integrations/plugins.

# P. Àríyá / AI
- provider/AIConnector
- model profiles/routing
- features
- registered tools/actions
- read/write risk
- confirmation/approval
- Knowledge sources
- provider data-class policy
- usage/budgets/rate limits
- retention/audit
- Portal Àríyá
- disabled organisations/properties

User-facing name is always Àríyá. Chatwoot Captain remains separate.

# Q. Vault
- item types/categories
- classifications
- access policy
- client sharing
- temporary grants
- access requests/approvals
- reveal/copy/download policy
- step-up
- retention
- rotation/expiry defaults

# R. Files
- storage provider
- limits/types
- public/private defaults
- scan/processing policy
- versions
- retention/trash
- sharing

Protected confidential documents should route to Vault rather than preserve ordinary File access.

# S. Automations
- enabled/limits
- concurrency/run duration
- retries
- recursion protection
- schedule/timezone behavior
- failure/dead-letter policy
- Action Registry permissions
- AI-step policy

# T. Data & Customization

## Custom Fields
- supported record types
- field types
- validation
- dynamic display/required rules
- sensitivity
- Portal/API/search/report policy

## Tags / Taxonomy
- tag/category administration
- merge/archive
- scope

## Saved Views
- shared-view permission
- default views

## Imports / Exports
- allowed formats
- file limits
- duplicate rules
- dry-run requirements
- export scope/retention

## Data Quality
- issue types
- duplicate thresholds
- stale/missing/mapping rules

## Record lifecycle / numbering
- prefixes/sequences
- archive/trash/purge defaults
- retention/hold integration

# U. Plugins
- installed/sources
- permissions
- compatibility
- update/rollback
- development-source policy
- extension/navigation rules

# V. Connectors
- instances
- authentication
- mappings
- capability grants
- sync direction/authority/conflict policy
- health
- events
- retry/dead-letter
- credentials references
- rate limits
- diagnostics

Specific connector settings may include Chatwoot, Cloudflare, payment providers, OpenRouter, Documenso, optional Uptime Kuma, OJS, WordPress, WooCommerce, email/calendar/storage.

# W. API & MCP
- REST API
- API clients/tokens
- scopes
- webhooks
- rate limits
- MCP clients
- tool grants
- read/write policy
- confirmation/approval
- audit

# X. Security & Privacy
- authentication
- MFA
- password/session policy
- devices
- step-up
- IP/rate controls where used
- security events
- Secure External Access policy
- privacy/consent
- data-right workflows
- retention/legal/operational hold
- export/deletion/anonymization

# Y. System
- health
- jobs/queues
- Monitoring Worker health
- logs/diagnostics
- storage health
- backups
- updates
- feature flags
- delivery diagnostics
- redacted diagnostic bundle
- About/version

## Explicit exclusions
Settings must not contain or imply:
- HR
- payroll
- recruitment
- leave/attendance
- performance review
- Timesheets/Time Tracking
- Client Service Consumption/usage credits/hours remaining

## Acceptance criteria
- settings are searchable and domain-owned;
- high-risk settings expose consequences and audit;
- Operating Entity/Brand supports multi-brand future without complicating ordinary use;
- monitoring is native with external connectors optional;
- Àríyá is named consistently;
- navigation remains simple even though Settings is deep;
- excluded HR/timesheet/consumption features are absent.
