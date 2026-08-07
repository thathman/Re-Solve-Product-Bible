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

## Core Product Flows

### Admin
- [Admin Dashboard](01-admin/dashboard.md)
- [My Work](01-admin/my-work.md)
- [Organisations and Contacts](01-admin/organisations-and-contacts.md)
- [Properties](01-admin/properties.md)

### Client Portal
- [Client Portal Home](02-portal/home.md)

## Business Operations

### Admin
- [Projects](01-admin/projects.md)
- [Sales & Commercial](01-admin/sales-and-commercial.md)
- [Billing & Finance Operations](01-admin/billing.md)
- [Support Operations & Chatwoot](01-admin/support.md)
- [Secure Vault](01-admin/secure-vault.md)

### Platform
- [Files Platform](03-platform/files.md)
- [Re:Solve Knowledge Platform](03-platform/knowledge.md)
- [Automations Platform](03-platform/automations.md)

## Platform Core

### Extensions
- [Plugin Platform](05-extensions/plugins.md)
- [Connector Platform](05-extensions/connectors.md)

### API & AI Integration
- [API & Webhooks](07-api/api-and-webhooks.md)
- [MCP Platform](07-api/mcp.md)
- [Re:Solve AI](04-ai/re-solve-ai.md)

### Security
- [Security Architecture](08-security/security-architecture.md)

### Build
- [Lovable Development Environment](10-build/lovable-environment.md)

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

Specifications are added incrementally. Cross-cutting platform behavior is defined before feature pages that depend on it.