# Re:Solve Architecture & Portability Checklist

## Purpose
Re:Solve is built in Lovable, but the application architecture must remain exportable, understandable, and independently deployable later. This checklist is a guardrail, not a mandate to build production infrastructure during product development.

## Principle
Prefer Lovable-native productivity now while avoiding unnecessary runtime lock-in.

## Data access
- [ ] Business UI does not directly embed complex Supabase queries everywhere.
- [ ] Shared data access is organized through domain services/repositories/hooks with clear ownership.
- [ ] Provider-specific response shapes are normalized before they reach unrelated feature code.
- [ ] Database assumptions are documented.
- [ ] Row-level security/policies do not replace application permission design without clear reasoning.
- [ ] Migrations/schema changes are reproducible.
- [ ] Demo seeding is reproducible and separable from system configuration.

## Authentication
- [ ] Auth usage is centralized enough that provider replacement would not require rewriting every page.
- [ ] Roles and permissions are Re:Solve concepts, not only provider metadata conventions.
- [ ] Session behavior and authorization checks are explicit.
- [ ] Client and Admin shell selection is based on canonical identity/membership data.

## Storage
- [ ] File metadata is a Re:Solve concept independent of storage provider.
- [ ] Storage object keys/URLs are not treated as permanent business identifiers.
- [ ] Signed/temporary URLs are generated through a service boundary.
- [ ] Secure Vault content uses stricter handling than ordinary files.

## Realtime
- [ ] Realtime subscriptions are an optimization/interaction layer rather than the only source of truth.
- [ ] Core flows still have deterministic fetch/reload behavior.
- [ ] Realtime provider details are not scattered across unrelated components.

## Server/runtime
- [ ] No product-critical feature depends solely on a Lovable-hosted proprietary runtime.
- [ ] Server-side actions can be represented as normal application/server functions after export.
- [ ] Environment configuration is explicit.
- [ ] Secrets are never committed into client bundles or repositories.
- [ ] Background work has a conceptual job/event contract even if the development implementation is simple initially.

## UI portability
- [ ] UI is built from source-controlled React/components rather than non-exportable visual configuration.
- [ ] Shared design tokens are represented in code.
- [ ] Components do not rely on undocumented Lovable-only behavior.
- [ ] shadcn/Radix and specialist libraries are normal package dependencies.

## API
- [ ] Core business operations can be exposed through a stable API boundary.
- [ ] UI-only mutations are not the sole way to perform meaningful business actions.
- [ ] API auth/scopes map to canonical Re:Solve permissions.

## MCP
- [ ] MCP tools call approved application services/API operations rather than direct arbitrary database access.
- [ ] Tool schemas are portable application definitions.
- [ ] Audit and scope rules are independent of a particular hosted MCP gateway.

## Plugins
- [ ] Plugin concepts are represented through manifests/contracts that can live in source control.
- [ ] Plugin UI uses declared extension slots.
- [ ] Plugin migrations/settings/permissions are explicit.
- [ ] Plugin lifecycle does not require a Lovable-only marketplace/runtime.

## Connectors
- [ ] External systems are accessed through connector contracts.
- [ ] Connector instances have explicit configuration and health state.
- [ ] Secrets are referenced, not casually copied into business tables.
- [ ] Webhook processing includes provider identity, verification, idempotency, retry, failure state, and audit concepts.

## PWA
- [ ] Manifest/service-worker behavior is represented in exportable source.
- [ ] Push implementation is replaceable if provider choice changes.
- [ ] Offline caching rules are explicit and security-aware.
- [ ] Vault values and sensitive tokens are never intentionally cached offline.

## Observability
- [ ] Errors have structured application context.
- [ ] Connector/webhook/job failures have identifiable records or logs.
- [ ] Correlation IDs/event IDs are used where asynchronous flows require them.
- [ ] Diagnostics do not expose secrets.

## Dependency review
For every unusual dependency ask:
1. What product problem does it solve?
2. Is it source-controlled and portable?
3. Is there a mature standard alternative?
4. Does it create a runtime dependency we actually need?
5. Can we replace it without rewriting domain logic?

## Cloud/provider-specific APIs
Provider-specific capabilities are allowed when useful during development, but must be wrapped if they are product-critical.

Examples to review carefully:
- Cloudflare-only runtime APIs
- Lovable-only server/runtime helpers
- provider-specific auth metadata assumptions
- storage URLs used as canonical IDs
- proprietary realtime semantics embedded in business logic

## What not to do yet
Do not spend early slices on:
- production reverse proxies
- Kubernetes
- elaborate Docker orchestration
- production backup infrastructure
- multi-region architecture
- premature queue clusters
- migration away from Supabase during active Lovable development

The requirement is architectural portability, not premature operations work.

## Slice completion check
Before closing a slice, ask:
- Did this slice introduce a new provider/runtime dependency?
- Is the dependency isolated?
- Is business truth still represented in Re:Solve concepts?
- Could exported source plausibly run outside Lovable without redesigning this feature?
- Did we accidentally encode a temporary development environment as permanent product architecture?
