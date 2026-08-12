# Settings

## Purpose
Settings is the control plane for Re:Solve. It exposes configuration deliberately with ownership, validation, Audit, diagnostics, permissions and safe defaults.

Settings must not become a miscellaneous dumping ground. Every setting belongs to a domain, has a scope and defined consequences.

## Information architecture
Top-level searchable groups:
1. General / Workspace
2. Operating Entities & Brands
3. People & Access
4. Client Portal
5. CRM / Clients
6. Properties / Monitoring / Renewals
7. Projects / Tasks / Delivery
8. Sales / Services / Proposals / Contracts
9. Billing / Spend / Adjustments
10. Forms / Requests / Reviews
11. Communications / Email
12. Documents / PDF Signatures
13. Notifications
14. Ariya / AI
15. Files / Vault
16. Automations
17. Data & Customization
18. Plugins / Connectors
19. API & MCP
20. Security & Privacy
21. System / Setup / Health

Settings navigation is searchable. Desktop uses a clean Settings index/sidebar; mobile uses index/drill-down. Search should deep-link directly to a setting such as `late fee`, `SMTP`, `PDF signature`, or `Portal invite`.

## Shared setting contract
Every setting declares scope (Workspace, Operating Entity, Brand, user, Team, client default, Property Type, plugin/connector instance), effective/inherited/default value, validation, permission, sensitivity, save/review behavior, Audit requirements, effect on existing records, rollback/recovery and health/diagnostics where applicable.

## Save model
Use immediate save for low-risk personal preferences; explicit Save for grouped config; Review Changes for high-impact settings; test-before-save for providers; step-up for highly sensitive changes.

## Configuration health
Major groups may report configured, partial, attention required, disabled, degraded or healthy. Unknown/stale must not be called healthy.

# A. General / Workspace
- Workspace name/code;
- locale/timezone/date/number formats;
- base/enabled currencies;
- default archive/retention links;
- system identity;
- numbering framework defaults;
- module visibility/defaults where not domain-specific.

# B. Operating Entities & Brands
## Entity identity
- legal/trading name;
- registration/tax identifiers;
- addresses/contact details;
- default currency/locale;
- billing/remittance identity;
- status/default Brand.

## Brand
- logos/app icons;
- approved tokens;
- Portal/auth identity;
- email identity;
- Document Studio theme;
- support identity;
- sender mappings.

## Operating Entity communication shell
Configurable independently:
- universal email HTML head/approved style tokens;
- email header;
- automated/system signature;
- email footer/legal text;
- default sender/reply-to;
- document header/footer/brand;
- default document signatory policies.

# C. People & Access
## Staff / Human User profile
Access/security settings plus operational identity:
- active/invited/suspended;
- Roles/Teams/scopes;
- sessions/MFA/security;
- **personal HTML Email Signature** editor/source with sanitization/preview;
- **personal Document/PDF Signature** asset;
- printed signatory name/title;
- which Operating Entities/document families the user may sign for;
- email/document signature enabled state.

Email signature and PDF signature are separate fields/contracts. These are business identity/signing settings, not HR fields.

## Teams / Roles / Permissions / Invitations / Sessions
Use scoped canonical capabilities, effective-access explanation, step-up/Approval for high-risk changes and responsibility reassignment before deactivation.

# D. Client Portal
- Portal enabled;
- default navigation/module visibility;
- client-safe terminology;
- Home/Needs Your Attention defaults;
- client roles/permissions;
- invitation policy;
- **default invitation trigger: Proposal acceptance/commercial commitment**;
- manual earlier invitation policy;
- Membership state/invitation expiry/resend/revoke;
- `Preview as Client` permission/policy;
- Organisation admin invitation rights;
- support/live-chat path through Ariya/Chatwoot;
- optional Portal Ariya policy;
- Brand/Operating Entity defaults.

No public registration is implied.

# E. CRM / Clients
- Lead sources;
- Opportunity pipelines/stages/probabilities;
- activity types/loss reasons;
- cadences/follow-up;
- segments;
- duplicate matching/merge policy;
- Client lifecycle/onboarding/offboarding;
- Account Team responsibility labels;
- relationship review cadence;
- client-health rules;
- custom fields/taxonomies.

# F. Properties / Monitoring / Renewals
## Properties
Property Types, relationships, statuses, client-safe mapping, custom fields, hierarchy and archive behavior.

## Native Monitoring
Enabled/default monitor policy, intervals/timeouts, failure/recovery thresholds, retention, maintenance, probe registration, client notification defaults.

## Property Health/Posture
Evidence categories, stale-source rules, posture mapping, client-safe exposure and optional status-page policy.

## Renewals
Obligation types, reminder windows, ownership, auto-renew state, verification, client decision/payment workflow.

# G. Projects / Tasks / Delivery
- Project statuses/priorities/templates;
- Task types/defaults/recurrence;
- Milestone/Deliverable/Approval defaults;
- Requests/Change Requests;
- client visibility;
- Saved Views/default Task views;
- Project financial display policy.

No `My Work` setting namespace, Timesheets or work timers exist.

# H. Sales / Services / Proposals / Contracts
## Service Catalogue
- categories;
- pricing basis `flat`, `quantity`, `duration`;
- quantity units;
- duration units/defaults (day/week/month/quarter/year);
- taxes;
- recurring/renewal eligibility;
- default Project Template/Support Entitlement;
- Property applicability;
- Price Books/Rate Cards;
- Service Packages/options.

## Proposals
There are no separate Quote/Estimate settings.

Configure:
- numbering;
- default presentation style;
- validity/expiry;
- templates;
- packages/options/add-ons;
- line/document discount rules;
- taxes;
- acceptance policy/evidence;
- Portal invitation trigger;
- Secure External Access;
- reminders;
- downstream Contract/Project/Invoice/Recurring Arrangement behavior;
- Proposal view evidence policy.

## Contracts
Numbering, templates, counterparty SignatureConnector, expiry/renewal, deposit requirements, client visibility.

# I. Billing / Spend / Adjustments
## Invoices
- numbering;
- due/payment terms;
- line defaults;
- signed Document Studio template/signatory rule.

## Taxes / Currencies
Tax definitions/effective dates, inclusive/exclusive behavior, exemptions, currency/rounding/exchange policy.

## Discounts / Adjustments / Late fees
- allowed Adjustment types;
- fixed/percentage calculation rules;
- grace period;
- once/recurring policy;
- caps;
- eligible Invoice states;
- Approval/waiver rules;
- client-safe notice wording;
- write-off policy.

A policy creates real Adjustment records; it never mutates Payment truth.

## Payment providers / reconciliation
Connector-based provider instances, methods/currencies, webhook/connection health, verification and reconciliation behavior.

## Recurring / deposits / schedules / credit control
Cadence, generation/issue policy, pause/cancel, deposits/installments, dunning/escalation/account-hold policy.

## Receipts / Credits / Refunds / Statements
Numbering, signed templates, approval/generation and client notification.

## Spend
Expense categories, approval, billable conversion, recurring vendor cost categories. No payroll/employee-expense assumptions.

# J. Forms / Requests / Reviews
## Requests
Types, statuses, default owner/team, Portal/public access, routing/conversion and response expectations.

## Forms
Templates, public/Portal/Secure External policy, Form Request deadlines/expiry, retention, abuse/file policy, routing, custom-field mappings.

## Review Requests
- eligible triggers such as Project complete/Support resolved/full Payment/manual;
- delay/reminder policy;
- destinations: Google/Facebook/Clutch/Trustpilot/custom;
- template;
- tracking/evidence policy.

# K. Communications / Email
## Connected Mailboxes
Provider Connector, inbound/outbound state, sender identity, sync direction, health/freshness, retention.

## Email composition
- universal head/styles;
- Operating Entity/Brand header;
- template body/subject/variables;
- staff HTML signature or entity/system signature;
- footer/legal content;
- preview/test.

## Inbound routing / Ariya
Configure allowed classifications, auto-route confidence threshold, eligible actions, Inbox Triage policy, Support/CRM/Project/Billing mapping and data-provider/privacy policy.

## Delivery
Retries/failure, bounce/delivery diagnostics, quiet hours, mandatory versus optional communication.

## Chatwoot
Portal live-chat/human handoff connector and health. Do not reproduce Chatwoot agent administration.

# L. Documents / PDF Signatures
## Document Studio
- template/version management;
- Brand/Operating Entity defaults;
- web/PDF output;
- A4/Letter;
- variable catalogue;
- retention/final snapshot;
- Secure External view policy.

## Mandatory issuer signature
Every final generated PDF is signed. Configure:
- default signatory by document family;
- named staff / issuing staff / record owner / entity-authorised signature mode;
- allowed staff signatories;
- signature snapshot rules;
- hash algorithm/version;
- verification URL/code/QR policy;
- public-safe verification fields.

Invoice and Receipt final PDFs are included.

## Counterparty signatures
Configure which Proposal/Contract/Approval document families require counterparty e-signature and which SignatureConnector is used.

# M. Notifications
Channels, event policies, recipient defaults, priority, grouping/dedupe, templates, digests, quiet hours, mandatory events, retries/failure, retention and test center.

# N. Ariya / AI
- provider/AIConnector/model profiles;
- feature/data-class routing;
- registered tools/actions;
- Ask/Draft/Act/Watch/Investigate/Recommend capabilities;
- read/write/autonomy limits;
- confirmation/Approval/step-up;
- Property Health monitoring tools;
- Communications/email classification thresholds;
- Knowledge sources;
- Vault secret-handle policy;
- usage/budgets/rate limits;
- retention/Audit;
- Portal Ariya;
- disabled Organisations/Properties/features.

Ariya remains subject to caller scope; settings cannot grant model-level bypass authority.

# O. Files / Vault
Storage, file requests, type/size/scan, versions, retention/trash/sharing and protected Vault classification/access/rotation/step-up.

# P. Automations
Enabled/limits, concurrency, retries, recursion, timezone, dead-letter, Action permissions, Ariya AI-step/Watch policy.

# Q. Data & Customization
Custom Fields, Tags/Taxonomy, Saved Views, configurable dashboards/module visibility, Imports/Exports, Data Quality, numbering, archive/trash/restore.

# R. Plugins / Connectors
Instances, auth, mappings, capability grants, sync direction/authority/conflict, health, events, retry/dead-letter, credential references, diagnostics and provider-specific configuration.

# S. API & MCP
API clients/tokens/scopes/webhooks/rate limits, MCP clients/tool grants/read-write policy/confirmation/Audit.

# T. Security & Privacy
Authentication, MFA, sessions, step-up, abuse/rate controls, security events, Secure External Access, consent/data rights, retention/holds/export/deletion review.

# U. System / Setup / Health
- first-run Setup state/readiness;
- installer locked/unlocked state;
- runtime/database/storage/job/worker health;
- migrations;
- logs/diagnostics;
- backups/restore tests;
- updates/version;
- delivery diagnostics;
- feature rollout state;
- redacted diagnostics bundle.

First-run Setup is a dedicated guided workflow. Post-install System Settings may inspect/repair configuration but cannot silently re-open owner bootstrap.

## Explicit exclusions
Settings must not contain or imply HR, payroll, recruitment, leave/attendance, performance review, Timesheets/Time Tracking/work timers, Client Service Consumption/usage credits/hours remaining, or current-run CMS configuration.

## Acceptance criteria
- settings are searchable and domain-owned;
- staff HTML email signature and PDF signature are separate;
- email head/header/body/signature/footer layers are independently configurable;
- Proposal is the only offer settings domain;
- duration pricing/discount/late-fee policies are explicit;
- every final PDF signatory rule is configurable but mandatory;
- Portal invitation defaults to commercial commitment;
- Ariya autonomy remains permission/Action constrained;
- first-run setup can be inspected but owner bootstrap cannot be reopened casually;
- excluded domains are absent.
