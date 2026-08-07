# Re:Solve Product Bible

The Product Bible is the canonical source of truth for Re:Solve product behavior, flows, roles, states, permissions, information architecture, integrations, extension points, and acceptance criteria.

The product may be specified comprehensively here, but implementation must be delivered in small, reviewable Lovable build slices.

## Foundation

- [Product Thesis](00-foundation/product-thesis.md)
- [Product Principles](00-foundation/principles.md)
- [Terminology](00-foundation/terminology.md)
- [Actors and Roles](00-foundation/actors-and-roles.md)
- [Domain Model](00-foundation/domain-model.md)
- [Information Architecture](00-foundation/information-architecture.md)

## Experience Foundation

### Design
- [Design Direction](09-design/design-direction.md)
- [Design System](09-design/design-system.md)

### Admin
- [Admin OS Shell](01-admin/shell.md)
- [Settings](01-admin/settings.md)

### Client Portal
- [Client Portal Shell](02-portal/shell.md)

### Platform
- [Notifications Platform](03-platform/notifications.md)
- [PWA & Responsive Experience](03-platform/pwa.md)

## Core Product Flows

### Admin
- [Admin Dashboard](01-admin/dashboard.md)
- [My Work](01-admin/my-work.md)
- [Organisations and Contacts](01-admin/organisations-and-contacts.md)
- [Properties](01-admin/properties.md)

### Client Portal
- [Client Portal Home](02-portal/home.md)
- [Properties](02-portal/properties.md)
- [Projects](02-portal/projects.md)
- [Billing](02-portal/billing.md)
- [Support](02-portal/support.md)
- [Files, Vault & Knowledge](02-portal/files-vault-knowledge.md)
- [Organisation & Account](02-portal/organisation-and-account.md)

## Business Operations

### Admin
- [Projects](01-admin/projects.md)
- [Sales & Commercial](01-admin/sales-and-commercial.md)
- [Billing & Finance Operations](01-admin/billing.md)
- [Support Operations & Chatwoot](01-admin/support.md)
- [Secure Vault](01-admin/secure-vault.md)
- [Monitoring](01-admin/monitoring.md)
- [Reports & Analytics](01-admin/reports-and-analytics.md)
- [Service Catalogue & Recurring Services](01-admin/services-and-recurring.md)
- [Team & Access Administration](01-admin/team-and-access.md)
- [System Operations](01-admin/system-operations.md)

### Platform
- [Files Platform](03-platform/files.md)
- [Re:Solve Knowledge Platform](03-platform/knowledge.md)
- [Automations Platform](03-platform/automations.md)
- [Forms](03-platform/forms.md)
- [Global Search & Activity](03-platform/search-and-activity.md)
- [Calendar & Reminders](03-platform/calendar-and-reminders.md)
- [Approvals](03-platform/approvals.md)

## Platform Core

### Extensions
- [Plugin Platform](05-extensions/plugins.md)
- [Connector Platform](05-extensions/connectors.md)
- [Core Connector Contracts](06-connectors/core-connectors.md)

### API & AI Integration
- [API & Webhooks](07-api/api-and-webhooks.md)
- [MCP Platform](07-api/mcp.md)
- [Re:Solve AI](04-ai/re-solve-ai.md)

### Security
- [Security Architecture](08-security/security-architecture.md)

## Lovable Execution

- [Lovable Development Environment](10-build/lovable-environment.md)
- [Persistent Lovable Knowledge](10-build/lovable-knowledge.md)
- [Lovable Skill Set](10-build/lovable-skills.md)
- [Build Slice Protocol](10-build/build-slice-protocol.md)
- [Demo Data Blueprint](10-build/demo-data-blueprint.md)
- [Architecture & Portability Checklist](10-build/architecture-portability-checklist.md)
- [Lovable Setup Sequence](10-build/lovable-setup-sequence.md)
- [FOUND-001 — Re:Solve Application Foundation](10-build/prompts/FOUND-001-foundation.md)

### Initial Lovable Skill Templates

- `10-build/lovable-skills/airix-feature/SKILL.md`
- `10-build/lovable-skills/airix-ui/SKILL.md`
- `10-build/lovable-skills/airix-form/SKILL.md`
- `10-build/lovable-skills/airix-data-table/SKILL.md`
- `10-build/lovable-skills/airix-security-review/SKILL.md`
- `10-build/lovable-skills/airix-pwa/SKILL.md`
- `10-build/lovable-skills/airix-release/SKILL.md`
- `10-build/lovable-skills/self-host-check/SKILL.md`

## Governing Workflow

Product specifications should follow the installed Re:Solve spec and flow skills:

- `.github/skills/re-solve-spec/`
- `.github/skills/flow-by-flow/`
- `.github/skills/flow-prototype/`

The planning sequence is:

1. establish governing product truth
2. define actors, goals, scope, states, permissions, and flows
3. specify the complete product experience
4. validate flow completeness
5. prototype major interaction flows where needed
6. define acceptance criteria
7. break implementation into small Lovable build slices
8. install persistent Lovable Knowledge and only the skills needed for the current build phase
9. build one bounded slice
10. review against Product Bible, security, accessibility, PWA, and portability rules before moving on

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

Specifications are added incrementally. Cross-cutting platform behavior is defined before feature pages that depend on it.