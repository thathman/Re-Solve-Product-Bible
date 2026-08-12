# Re:Solve Revised Implementation Roadmap — 2026-08

## Status
Canonical implementation roadmap rebuilt from the Product Bible baseline at `v1.2.0.1` after the 2026-08 product-model review.

This roadmap preserves completed production work and reorganizes only the remaining work. It does **not** reopen Phase 1 or Phase 2, discard production data, or require already-proven foundations to be rebuilt for naming symmetry.

The roadmap is an orientation layer. Before each future phase begins, its complete atomic ledger must be created and shown to the owner per `phase-execution-protocol.md`.

## Completed foundation

### Phase 1 — Data Truth
Status: **Complete**.

Preserve the completed Data Truth pass, RLS/tenant isolation, seeded-data truth, runtime health, rollback and deployment evidence. DT-030 remains the historical non-blocking clean-reset proof item unless a later deployment requirement makes it real.

### Phase 2 — Support Operating Foundation
Status: **Complete**.

Preserve Support ownership, Platform primitives and Support lifecycle work already shipped. Later phases may extend Support through Communications, Chatwoot/Ariya, Files, SLA and Automations, but do not rebuild the existing authoritative lifecycle.

## Active transition

### Phase 3A — Client & Commercial Foundation
Historical ledger: `CCC-001...CCC-175` in the application repository.

Implemented production foundation already includes:
- Clients / Organisations / Contacts;
- CRM Leads and conversion;
- Properties and domains;
- Sales Quote foundation and client-decision evidence;
- Billing engineering foundation, migrations and rollback acceptance.

The Product Bible review changed the target commercial model materially: Proposal now unifies Proposal/Quote/Estimate; Opportunities, Service Catalogue, Contracts, Recurring Arrangements, signed commercial PDFs, Adjustments and the Portal commitment gate are first-class. Therefore pending legacy CCC work is not executed blindly.

Projects and the old `CCC-130...151` delivery scope move to Phase 5. Shared communication/document work is absorbed into the new commercial-completion ledger where required.

### Phase 3B — Commercial Completion
Prefix: `CCF`
Status: **Active next ledger**.

Purpose: finish the canonical commercial spine without discarding already-shipped truth:

`Lead -> Organisation/Contact -> Opportunity -> Proposal -> Acceptance -> Portal Invitation -> Contract/Recurring Arrangement where applicable -> Invoice/Adjustment -> Payment`

Scope:
- close and production-promote the current Billing release;
- Opportunities/Deals;
- Service Catalogue, Price Books/Rate Cards, packages and flat/quantity/duration pricing;
- migrate the shipped Quote foundation into the canonical Proposal experience while preserving IDs/history/evidence;
- Contracts and Recurring Arrangements;
- mandatory signed immutable commercial PDFs;
- minimum transactional email/document delivery required by commercial workflows;
- discounts, late fees, penalties, credits, write-offs, deposits and payment plans without mutating Payment truth;
- default Portal invitation at commercial commitment and secure guest pre-commitment flows;
- phase-wide security, money, migration, deployment and Admin/Portal browser acceptance.

Full atomic ledger: `10-build/phase-3b-commercial-completion.md`.

## Remaining phases

### Phase 4 — Admin & Client Portal Experience Reset
Planned prefix: `UXR`.

Purpose: establish the clean product shell before expanding delivery operations further.

Primary scope:
- redesign Admin shell/navigation around Home, Tasks, Clients, CRM, Sales, Delivery, Support, Billing, Forms, Calendar, Information, Reports, Automations and Settings;
- make Ariya persistent/contextual rather than an ordinary disconnected module;
- redesign record workspaces around identity/state/actions/context rather than card density;
- rebuild Portal Home around `Needs Your Attention` and a deliberately small client navigation model;
- Preview as Client, strictly read-only;
- module visibility/toggles and saved-view foundations required to control product breadth;
- responsive/mobile/accessibility/design-system consistency;
- preserve all existing authorization/data truth while replacing presentation.

Out of scope: broad new domain engines. This phase establishes the experience contract those engines use.

### Phase 5 — Delivery Operations & Client Journeys
Planned prefix: `DEL`.

Purpose: turn accepted commercial work into accountable delivery and a coherent client onboarding/service journey.

Primary scope:
- Projects lifecycle and Project Templates;
- Tasks as the universal staff execution surface;
- milestones, deliverables, dependencies, risks/issues and Change Requests;
- reusable Approval Policies and Approval Requests;
- Requests, including Portal Service Request -> Opportunity -> Proposal handoff;
- Renewals;
- Project Financial Plan / commercial health without time tracking;
- Forms engine, Form Requests/Assignments, project questionnaires and surveys where needed by delivery;
- File Requests;
- Booking/public scheduling for kickoff and client actions;
- Client Journeys / Onboarding Packs referencing real Contract, Invoice, Form, File Request, Booking, Approval, Task and Project records;
- Portal Projects/tasks/client-actions/approvals/journey surfaces;
- Ariya delivery context/actions.

### Phase 6 — Communications & Collaboration
Planned prefix: `COM`.

Purpose: make communications part of the operating record rather than disconnected notifications.

Primary scope:
- Connected Mailboxes and Shared Inbox/Triage;
- inbound/outbound email threading and record association;
- full staff HTML signature/profile behavior and Workspace/Operating Entity mail branding;
- expanded Email Template management and delivery evidence;
- Ariya inbound-email classification/routing with confidence/evidence;
- Support email ingestion and case/reply mapping;
- Portal -> Ariya -> Chatwoot -> Ariya live-chat path and human handoff;
- Review Requests and configurable destinations;
- internal Notes, Comments, mentions, Following and record collaboration;
- Calendar, reminders, cadences and recurring operational work;
- notification center/preferences/channel rules;
- communication-related Attachments through the shared Files platform.

### Phase 7 — Property Intelligence & Information
Planned prefix: `PIN`.

Purpose: make Re:Solve authoritative for managed digital-property posture and reusable operational information.

Primary scope:
- native Property Health/Monitoring engine;
- HTTP/HTTPS, TCP/ping, DNS, TLS/certificate, domain expiry, API/heartbeat and supported application checks;
- Health Incidents, maintenance windows, notification/Attention policy and optional client/public status views;
- Ariya monitoring Watch/Investigate/Recommend capabilities;
- Files platform and cross-record attachments;
- Knowledge platform;
- Secure Vault and secret-handle usage boundaries;
- client-safe Files/Knowledge/selected health visibility;
- backup/connector health evidence where authoritative integrations exist.

### Phase 8 — Ariya & Workflow Intelligence
Planned prefix: `AIW`.

Purpose: complete Ariya as the intelligence fabric and make repetitive operational work policy-driven.

Primary scope:
- Ariya `Ask`, `Draft`, `Act`, `Watch`, `Investigate`, `Recommend` across authorised domains;
- provenance/freshness/evidence links;
- permission-aware Action Registry execution and approval/risk tiers;
- Automations engine, schedules, triggers, conditions, actions, retries and execution history;
- shared Preview/Test/Dry-Run framework;
- Attention Engine expansion across completed domains;
- global search/command/activity experience;
- Reports and analytics with multi-currency truth;
- natural-language operational queries and automation creation;
- Portal-scoped Ariya with strict client-safe context.

### Phase 9 — Platform Governance & Data Extensibility
Planned prefix: `PGD`.

Purpose: let installations adapt safely without schema forks or destructive operational shortcuts.

Primary scope:
- Universal Template Center and dependency-aware `Where used?`;
- Custom Fields, taxonomy, tags/categories and record extensibility;
- universal Saved Views, favourites and recents;
- granular roles/capabilities and permission-aware UI;
- Archive -> Trash -> Restore -> Purge rules and Recycle Bin;
- Dependency/Impact Inspector;
- permission-aware Bulk Actions and impact preview;
- import/export/migration/data-quality tools;
- data provenance, retention, privacy/consent/data-rights;
- reference numbering/configuration and locale/timezone/date/currency presentation;
- Organisation/Contact dedupe/merge and other controlled reconciliation utilities;
- System/Settings governance needed by the above.

### Phase 10 — Integrations & Developer Platform
Planned prefix: `IDP`.

Purpose: make external providers and developer extensions first-class without bypassing Re:Solve authority.

Primary scope:
- Connector platform and credentials/connections;
- provider adapters and webhook verification;
- Chatwoot/Google/Microsoft/payment/calendar/Cloudflare and other approved connectors as dependencies require;
- plugin capability registration and safe execution;
- authenticated API and webhooks;
- MCP platform;
- rate/security/audit controls;
- sync provenance and failure/retry visibility;
- portability boundaries so core business truth remains source-owned and provider-agnostic.

### Phase 11 — Setup, Product Completion & Production Readiness
Planned prefix: `SPR`.

Purpose: make Re:Solve installable, maintainable, supportable and production-ready as a self-hosted agency OS.

Primary scope:
- first-run Setup Mode/system checks/security bootstrap/Workspace/Operating Entity/commercial defaults/email/storage/integrations/import/readiness;
- one-way `Lock Setup` and post-install System Operations;
- PWA/installability/update/offline-safe policy with private/auth data network-only;
- System Health, workers/jobs, migrations, storage, email, backup and connector posture;
- backup/recovery and disaster-recovery acceptance;
- product documentation/help center/admin help/Portal help;
- security hardening, grants/RLS/tenant attacks/secrets/dependency review;
- accessibility, responsive/mobile, loading/empty/error and visual-consistency closure;
- performance/observability/logging/health;
- full Admin + Portal cross-domain E2E;
- exact-SHA OpenShip deployment/rollback/recovery evidence;
- final Product Bible/Oversight reconciliation and production-ready release.

## Explicit boundaries for this run
Do not add HR/payroll/recruitment/leave/attendance/performance management, Timesheets/Time Tracking/work timers, employee-utilization planning based on hours, full accounting/general ledger, inventory/warehouse/manufacturing/POS, a duplicate native live-chat engine, or CMS/public-content functionality.

CMS remains a distant-future extension only.

## Browser/experience gates
Each phase receives its own consolidated Admin/Portal browser acceptance at phase closure where UI is affected. Internal engineering slices do not falsely claim browser passes. Browser findings are fixed before final phase closure and the exact corrected SHA is re-qualified/deployed.

## Continuous product discovery
This roadmap is a baseline, not a ceiling. Real gaps discovered during implementation are captured in Product Oversight, assigned deliberately, and absorbed into the current phase only when they are required for correctness/security or materially complete the active workflow. Do not restart broad competitor-module hunting during every slice.
