# Re:Solve Product Bible

The Product Bible is the canonical source of truth for Re:Solve product behavior, flows, roles, states, permissions, information architecture, integrations, extension points, design system, build discipline and acceptance criteria.

The product may be specified comprehensively here, but implementation must be delivered in small, reviewable Lovable build slices.

## Canonical Foundation
- [Product Thesis](00-foundation/product-thesis.md)
- [Product Principles](00-foundation/principles.md)
- [Canonical Expansion Decisions](00-foundation/canonical-expansion-decisions.md)
- [Terminology](00-foundation/terminology.md)
- [Actors, Principals, Roles and Access](00-foundation/actors-and-roles.md)
- [Domain Model](00-foundation/domain-model.md)
- [Information Architecture](00-foundation/information-architecture.md)
- [Operating Entities & Brands](00-foundation/operating-entities-and-brands.md)

## Design & Core UI
- [Design Direction](09-design/design-direction.md)
- [Design System](09-design/design-system.md)
- [Core UI Component Framework](09-design/core-ui-framework.md)
- [Navigation & Application Chrome](09-design/navigation-and-application-chrome.md)
- [Performance, Device & Design QA](09-design/performance-device-and-design-qa.md)

### Non-negotiable UI direction
Re:Solve's Core UI Framework is source-owned and heavily influenced/implemented from:
- shadcn/ui
- Untitled UI React
- Tremor
- React Aria / Base UI / Radix
- TanStack Table / TanStack Query
- approved specialist libraries where justified

Navigation must remain simple and business-readable, closer to straightforward Perfex/Brevo-style clarity than Odoo app launchers or Twenty-style object/module navigation.

## Admin OS
### Shell and Home
- [Admin OS Shell](01-admin/shell.md)
- [Admin Dashboard](01-admin/dashboard.md)
- [My Work](01-admin/my-work.md)

### Clients / CRM / Delivery
- [Organisations and Contacts](01-admin/organisations-and-contacts.md)
- [Client Success & Account Operations](01-admin/client-success.md)
- [Properties](01-admin/properties.md)
- [Projects](01-admin/projects.md)
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
- [Organisation & Account](02-portal/organisation-and-account.md)

## Platform Primitives
### Attention, Actions and Workflows
- [Attention Engine](03-platform/attention-engine.md)
- [Command & Action Registry](03-platform/action-registry.md)
- [Approvals](03-platform/approvals.md)
- [Automations](03-platform/automations.md)
- [Reminders, Cadences & Recurring Work](03-platform/reminders-cadences-and-recurring-work.md)
- [Calendar, Agenda & Time-Based Commitments](03-platform/calendar-and-reminders.md)

### Client / Intake / Collaboration
- [Client Lifecycle](03-platform/client-lifecycle.md)
- [Request Management](03-platform/requests.md)
- [Forms](03-platform/forms.md)
- [Collaboration & Following](03-platform/collaboration-and-following.md)
- [Booking & Public Scheduling](03-platform/booking-and-public-scheduling.md)
- [Feedback, Surveys & Business Goals](03-platform/feedback-surveys-and-business-goals.md)
- [Operational Communications & Announcements](03-platform/operational-communications-and-announcements.md)

### Documents, Files and Knowledge
- [Document Studio](03-platform/document-studio.md)
- [Files Platform](03-platform/files.md)
- [Re:Solve Knowledge Platform](03-platform/knowledge.md)
- [Secure External Access](03-platform/secure-external-access.md)

### Properties / Monitoring
- [Native Monitoring Engine](03-platform/monitoring-engine.md)

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

## Àríyá / AI
- [Àríyá — Re:Solve AI](04-ai/re-solve-ai.md)
- [Àríyá Product Identity & Experience](04-ai/ariya-experience.md)

Chatwoot Captain remains a separate support AI owned by Chatwoot.

## Extensions
- [Plugin Platform](05-extensions/plugins.md)
- [Connector Platform](05-extensions/connectors.md)

## Connector Contracts
- [Core Connector Contracts](06-connectors/core-connectors.md)
- [Cloudflare Connector](06-connectors/cloudflare.md)

Uptime Kuma is optional compatibility connector territory; Re:Solve has a native Monitoring Engine.

## API & Agent Integration
- [API & Webhooks](07-api/api-and-webhooks.md)
- [MCP Platform](07-api/mcp.md)

## Security
- [Security Architecture](08-security/security-architecture.md)

## Lovable Build System
- [Lovable Development Environment](10-build/lovable-environment.md)
- [Lovable Persistent Knowledge](10-build/lovable-knowledge.md)
- [Lovable Skills Catalogue](10-build/lovable-skills.md)
- [Lovable Setup Sequence](10-build/lovable-setup-sequence.md)
- [Build Slice Protocol](10-build/build-slice-protocol.md)
- [Architecture & Portability Checklist](10-build/architecture-portability-checklist.md)
- [Demo Data Blueprint](10-build/demo-data-blueprint.md)
- [FOUND-001 — Application + Core UI Foundation](10-build/prompts/FOUND-001-foundation.md)

### Initial Lovable skill templates
- `10-build/lovable-skills/resolve-feature/`
- `10-build/lovable-skills/resolve-ui/`
- `10-build/lovable-skills/resolve-shell/`
- `10-build/lovable-skills/resolve-form/`
- `10-build/lovable-skills/resolve-data-table/`
- `10-build/lovable-skills/resolve-security-review/`
- `10-build/lovable-skills/resolve-pwa/`
- `10-build/lovable-skills/resolve-release/`
- `10-build/lovable-skills/self-host-check/`

Deprecated `airix-*` skill names are removed; Re:Solve is the reusable product and Airix Media is the first Operating Entity/deployment.

## Governing Workflow
Product specification should follow the installed Re:Solve planning skills:
- `.github/skills/re-solve-spec/`
- `.github/skills/flow-by-flow/`
- `.github/skills/flow-prototype/`

Planning/build sequence:
1. establish governing product truth;
2. define actors/Principals, goal, scope, states, permissions and flows;
3. specify the complete product experience;
4. validate flow completeness and cross-domain ownership;
5. prototype major/high-risk interactions where needed;
6. define acceptance criteria;
7. break implementation into small Lovable build slices;
8. run functional/security/responsive/accessibility/Core UI/visual/portability review;
9. update Product Bible first if implementation reveals a real contradiction.

## Explicit Product Exclusions
Re:Solve core does **not** include:
- HR management;
- payroll;
- recruitment;
- leave/attendance;
- employee performance reviews;
- Timesheets / Time Tracking;
- Client Service Consumption / remaining-hours/credits usage metering.

Teams, assignments, Account Teams, Project deadlines, Reminders, Booking and operational Expenses are allowed business capabilities but must not drift into HR/Timesheet systems.

## Planned Spec Areas
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

The Product Bible can remain expansive. Lovable implementation remains intentionally gradual and slice-bound.
