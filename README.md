# Re:Solve Product Bible

The Product Bible is the canonical source of truth for Re:Solve product behavior, flows, roles, states, permissions, information architecture, integrations, extension points, design system, build discipline and acceptance criteria.

The product may be specified comprehensively here, but implementation is delivered in small, reviewable build slices inside owner-visible phases with complete atomic ledgers.

## Canonical Foundation
- [Product Thesis](00-foundation/product-thesis.md)
- [Product Principles](00-foundation/principles.md)
- [Canonical Expansion Decisions](00-foundation/canonical-expansion-decisions.md)
- [Product Model Closure Decisions](00-foundation/product-model-closure.md)
- [Terminology](00-foundation/terminology.md)
- [Actors, Principals, Roles and Access](00-foundation/actors-and-roles.md)
- [Domain Model](00-foundation/domain-model.md)
- [Information Architecture](00-foundation/information-architecture.md)
- [Operating Entities & Brands](00-foundation/operating-entities-and-brands.md)

### Current canonical product decisions
- **Tasks** is the staff execution surface; `My Work` is deprecated.
- **Proposal** unifies Proposal/Quote/Estimate into one offer domain with presentation styles.
- Service pricing supports flat, quantity and **duration** bases.
- Payment remains transaction evidence; late fees/penalties/credits/write-offs use explicit Adjustments/Credit/Refund records.
- Forms is a shared platform primitive for discovery, Project questionnaires, onboarding, surveys, feedback/reviews and intake.
- Communications includes Connected Mailboxes, inbound/outbound email, Shared Inbox/Triage, staff HTML signatures, templates and review requests.
- **Ariya (Àríyá)** is baked into the OS as the intelligence fabric across authorised domains with Ask/Draft/Act/Watch/Investigate/Recommend modes.
- Portal live chat uses `Portal -> Ariya -> Chatwoot -> Ariya -> Client`.
- Native Property Health/Monitoring is first-class and Ariya can Watch/investigate it through controlled capabilities.
- **Every issued/final generated PDF is issuer-signed**, including Invoices and Receipts, with immutable signature snapshot/hash/verification evidence.
- Default Portal invitation occurs at commercial commitment, normally Proposal acceptance; pre-commitment flows can use Secure External Access.
- First-run setup/installation is built into the product and locks after bootstrap.
- **Template Center** governs reusable domain-owned templates with versioning, preview/test and dependency visibility.
- **Client Journeys** orchestrate onboarding, activation, handover, renewal and offboarding using real underlying records.
- Projects have an agency-focused **Financial Plan** using commercial/Billing/Expense truth without staff time tracking.
- Approval is policy-driven with single, any-one, all, sequential, parallel and conditional routing.
- Record lifecycle uses deliberate Archive/Trash/Restore/Purge semantics with Dependency/Impact inspection.
- High-impact configuration/workflows support **Preview/Test/Dry Run** before execution.
- Bulk Actions are explicit, permission-aware and impact-previewed rather than automatically available for selectable rows.
- Portal Service Requests for new paid scope route `Request -> Opportunity -> Proposal` rather than Support or instant Invoice/Project.
- Admin and Client Portal require a deliberate experience redesign before product completion.
- Public/headless CMS is distant-future only and explicitly outside the current development run.
- No HR, payroll, attendance/leave/recruitment/performance, Timesheets/Time Tracking/work timers or Client Service Consumption metering.

The 2026-08 broad feature-discovery pass is now **closed**. New product gaps discovered during implementation use Product Oversight and do not restart horizontal competitor-feature hunting unless explicitly approved.

## Design & Core UI
- [Design Direction](09-design/design-direction.md)
- [Design System](09-design/design-system.md)
- [Core UI Component Framework](09-design/core-ui-framework.md)
- [Navigation & Application Chrome](09-design/navigation-and-application-chrome.md)
- [Admin and Client Portal Experience Reset](09-design/admin-and-portal-experience-reset.md)
- [Performance, Device & Design QA](09-design/performance-device-and-design-qa.md)

### Non-negotiable UI direction
Re:Solve's Core UI Framework is source-owned and heavily influenced/implemented from shadcn/ui, Untitled UI React, Tremor, React Aria/Base UI/Radix, TanStack Table/Query and approved specialist libraries where justified.

Navigation remains simple and business-readable, closer to straightforward service-CRM clarity than app-launcher/module-grid systems. The experience-reset document overrides any assumption that the current Admin/Portal shells are final visual authority.

## Admin OS
### Shell and Home
- [Admin OS Shell](01-admin/shell.md)
- [Admin Dashboard](01-admin/dashboard.md)
- [Tasks](01-admin/tasks.md)
- [`My Work` — deprecated compatibility note](01-admin/my-work.md)

### Clients / CRM / Delivery
- [Organisations and Contacts](01-admin/organisations-and-contacts.md)
- [Client Success & Account Operations](01-admin/client-success.md)
- [Properties](01-admin/properties.md)
- [Projects](01-admin/projects.md)
- [Project Financial Plan & Commercial Health](01-admin/project-financials.md)
- [Sales & Commercial](01-admin/sales-and-commercial.md)
- [Service Catalogue & Client Services](01-admin/services-and-recurring.md)

### Finance / Support / Operations
- [Billing & Finance Operations](01-admin/billing.md)
- [Operational Spend & Expenses](01-admin/spend-and-expenses.md)
- [Support Operations & Chatwoot](01-admin/support.md)
- [Monitoring & Property Posture](01-admin/monitoring.md)
- [Reports & Analytics](01-admin/reports-and-analytics.md)
- [Secure Vault](01-admin/secure-vault.md)

### Administration
- [People, Principals & Access](01-admin/team-and-access.md)
- [System Operations](01-admin/system-operations.md)
- [Settings](01-admin/settings.md)

## Client Portal
- [Client Portal Shell](02-portal/shell.md)
- [Home](02-portal/home.md)
- [Properties](02-portal/properties.md)
- [Projects](02-portal/projects.md)
- [Billing](02-portal/billing.md)
- [Support](02-portal/support.md)
- [Files, Vault & Knowledge](02-portal/files-vault-knowledge.md)
- [Organisation & Account / Portal Activation](02-portal/organisation-and-account.md)

## Platform Primitives
### Attention, Actions and Workflows
- [Attention Engine](03-platform/attention-engine.md)
- [Command & Action Registry](03-platform/action-registry.md)
- [Approvals & Approval Policies](03-platform/approvals.md)
- [Automations](03-platform/automations.md)
- [Test, Preview & Dry-Run Framework](03-platform/testing-and-simulation.md)
- [Reminders, Cadences & Recurring Work](03-platform/reminders-cadences-and-recurring-work.md)
- [Calendar, Agenda & Time-Based Commitments](03-platform/calendar-and-reminders.md)

### Client / Intake / Collaboration
- [Client Lifecycle](03-platform/client-lifecycle.md)
- [Client Journeys & Onboarding Packs](03-platform/client-journeys.md)
- [Request Management](03-platform/requests.md)
- [Forms](03-platform/forms.md)
- [Collaboration & Following](03-platform/collaboration-and-following.md)
- [Booking & Public Scheduling](03-platform/booking-and-public-scheduling.md)
- [Feedback, Surveys & Business Goals](03-platform/feedback-surveys-and-business-goals.md)
- [Communications & Announcements](03-platform/operational-communications-and-announcements.md)

### Templates, Documents, Files and Knowledge
- [Template Center](03-platform/template-center.md)
- [Document Studio / Signed PDFs](03-platform/document-studio.md)
- [Files Platform](03-platform/files.md)
- [Re:Solve Knowledge Platform](03-platform/knowledge.md)
- [Secure External Access](03-platform/secure-external-access.md)

### Properties / Monitoring
- [Native Monitoring Engine](03-platform/monitoring-engine.md)

### Installation / System foundation
- [First-Run Setup and Installation](03-platform/first-run-setup-and-installation.md)

### Notifications / Navigation / Data
- [Notifications Platform](03-platform/notifications.md)
- [Global Search, Command & Activity](03-platform/search-and-activity.md)
- [Saved Views, Favorites & Recents](03-platform/saved-views-favorites-and-recents.md)
- [Custom Fields, Taxonomy & Record Extensibility](03-platform/custom-fields-taxonomy-and-record-extensibility.md)
- [Data Provenance, Authority & Sync](03-platform/data-provenance-and-sync.md)
- [Import, Export, Migration & Data Quality](03-platform/import-export-and-data-quality.md)
- [Human References & Record Lifecycle](03-platform/reference-numbering-and-record-lifecycle.md)
- [Privacy, Consent & Data Rights](03-platform/privacy-consent-and-data-rights.md)
- [PWA & Responsive Experience](03-platform/pwa.md)

## Ariya / AI
- [Ariya — Re:Solve Intelligence Fabric](04-ai/re-solve-ai.md)
- [Ariya Product Identity & Experience](04-ai/ariya-experience.md)

Ariya is separate from Chatwoot Captain. Portal human-support chat uses Ariya/Chatwoot integration rather than a duplicate Re:Solve live-chat console.

## Extensions
- [Plugin Platform](05-extensions/plugins.md)
- [Connector Platform](05-extensions/connectors.md)
- [Planned Domain Extensions](05-extensions/planned-domain-extensions.md)

The headless CMS is recorded only as a distant-future expansion in Planned Domain Extensions.

## Connector Contracts
- [Core Connector Contracts](06-connectors/core-connectors.md)
- [Cloudflare Connector](06-connectors/cloudflare.md)

Uptime Kuma is optional compatibility connector territory; Re:Solve has a native Monitoring Engine.

## API & Agent Integration
- [API & Webhooks](07-api/api-and-webhooks.md)
- [MCP Platform](07-api/mcp.md)

## Security
- [Security Architecture](08-security/security-architecture.md)

# Build System
- [Lovable Development Environment](10-build/lovable-environment.md)
- [Lovable Persistent Knowledge — detailed source](10-build/lovable-knowledge.md)
- [Lovable Skills Catalogue](10-build/lovable-skills.md)
- [Lovable Setup Sequence](10-build/lovable-setup-sequence.md)
- [Build Slice Protocol](10-build/build-slice-protocol.md)
- [Phase Execution & Checkpoint Protocol](10-build/phase-execution-protocol.md)
- [Architecture & Portability Checklist](10-build/architecture-portability-checklist.md)
- [Demo Data Blueprint](10-build/demo-data-blueprint.md)
- [FOUND-001 — Application + Core UI Foundation](10-build/prompts/FOUND-001-foundation.md)

## Phase governance — non-negotiable
Before **every** implementation phase begins:
1. expand it into a complete stable numbered atomic ledger;
2. show the entire expansion to the owner;
3. absorb/assign relevant Product Oversight items;
4. only then execute build slices.

Every meaningful checkpoint/completion summary must show the **full current-phase task ledger** with all complete, active, pending and deliberately deferred tasks. Broad roadmap Steps do not replace the phase ledger.

See [Phase Execution & Checkpoint Protocol](10-build/phase-execution-protocol.md).

## Lovable Launch Pack
Start here when the Product Bible is merged and the first Lovable build is ready:
- [START HERE](10-build/lovable-launch/START-HERE.md)
- [Pre-build Readiness Checklist](10-build/lovable-launch/READINESS-CHECKLIST.md)
- [Paste-ready Project Knowledge](10-build/lovable-launch/PROJECT-KNOWLEDGE.md)
- [Application `AGENTS.md` template](10-build/lovable-launch/AGENTS.md.template)
- [GitHub transition plan](10-build/lovable-launch/GITHUB-TRANSITION.md)
- [FOUND-001 review gate](10-build/lovable-launch/FOUND-001-REVIEW.md)
- [Build State tracker](10-build/lovable-launch/BUILD-STATE.md)

Current Lovable Git sync creates a new repository and does not import the existing legacy `thathman/Re-Solve` repository. The launch pack therefore preserves the legacy repository as reference during FOUND-001 and defines a controlled post-foundation repository naming transition.

## Lovable Skills
Installation/governance:
- [Skill installation guide](10-build/lovable-skills/INSTALL.md)
- [Skill manifest](10-build/lovable-skills/manifest.md)

### Build/UI
- `resolve-feature`
- `resolve-ui`
- `resolve-shell`
- `resolve-navigation`
- `resolve-responsive`
- `resolve-form`
- `resolve-data-table`
- `resolve-record-workspace`
- `resolve-dashboard`
- `resolve-portal`

### Design/quality
- `resolve-accessibility`
- `resolve-design-review`
- `resolve-security-review`
- `resolve-pwa`
- `resolve-debug`
- `resolve-release`
- `self-host-check`

### Platform
- `resolve-notifications`
- `resolve-attention`
- `resolve-action-registry`
- `resolve-settings`
- `resolve-data-migration`

### Extensions/machine interfaces
- `resolve-plugin`
- `resolve-connector`
- `resolve-automation`
- `resolve-api`
- `resolve-mcp`

### Specialist domains
- `resolve-monitoring`
- `resolve-document`
- `resolve-ai`
- `resolve-vault`

Every skill has a canonical `10-build/lovable-skills/<skill>/SKILL.md` file. Deprecated `airix-*` skill names are removed.

## Governing Workflow
Product specification follows the installed Re:Solve planning skills:
- `.github/skills/re-solve-spec/`
- `.github/skills/flow-by-flow/`
- `.github/skills/flow-prototype/`

Planning/build sequence:
1. establish governing product truth;
2. define actors/Principals, goal, scope, states, permissions and flows;
3. specify the complete product experience;
4. validate flow completeness/cross-domain ownership;
5. expand the implementation phase into its full numbered ledger and show the owner;
6. prototype high-impact interactions where needed;
7. define acceptance criteria;
8. break implementation into small build slices;
9. configure Project Knowledge and relevant canonical skills;
10. build one slice;
11. run functional/security/responsive/PWA/accessibility/Core UI/design/portability review;
12. update Product Bible first if implementation reveals genuine new product truth;
13. update the full owner-visible phase checklist/checkpoint;
14. only then proceed to the next slice/phase.

## Explicit Product Exclusions
Re:Solve core/current run does **not** include:
- HR management;
- payroll;
- recruitment;
- leave/attendance;
- employee performance reviews;
- Timesheets / Time Tracking / work timers;
- Client Service Consumption / remaining-hours/credits usage metering;
- the distant-future CMS/public content platform.

Teams, assignments, Account Teams, Project deadlines, Reminders, Booking and operational Expenses are allowed business capabilities but must not drift into HR/Timesheet systems.

## Spec Areas
```text
00-foundation/
01-admin/
02-portal/
03-platform/
04-ai/
05-extensions/
06-connectors/
07-api/
08-security/
09-design/
10-build/
```

The Product Bible can remain expansive. Implementation remains intentionally phase-led, slice-bound and evidence-driven.
