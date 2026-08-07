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