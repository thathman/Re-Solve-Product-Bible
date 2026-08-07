# Re:Solve Product Principles

These principles govern product decisions across Re:Solve. Detailed specifications may extend them but should not silently contradict them.

## 1. Business truth belongs in Re:Solve

Re:Solve should own durable business records, relationships, permissions, operational context, and audit history.

External systems may execute specialist functions, but Re:Solve should retain the context required to understand what happened and how it relates to clients, properties, projects, services, and finances.

## 2. Specialist systems remain replaceable

Do not rebuild mature specialist infrastructure without a clear product advantage.

Examples:
- Chatwoot for managed client support
- Documenso for document signing
- payment gateways for money movement
- external monitoring providers where useful

External providers are integrated through connectors and should not leak provider-specific assumptions across the product.

## 3. Core, plugin, and connector are different concepts

### Core
Capabilities required for Re:Solve to function as an operating system.

### Plugin
Adds or extends business capabilities inside Re:Solve.

### Connector
Integrates Re:Solve with an external system or provider.

A feature specification must identify which category it belongs to.

## 4. Properties are first-class

Digital and operational properties must not be treated as incidental custom fields on clients.

Properties can be nested and can carry their own:
- access
- health
- services
- projects
- files
- credentials
- support context
- monitoring
- renewals
- connector instances

## 5. Notifications are a platform primitive

Every meaningful event must deliberately consider notification behavior.

Notifications must support:
- recipient rules
- priority
- in-app delivery
- push
- email
- WhatsApp where appropriate
- digests
- deduplication
- deep links
- user preferences
- mandatory security/system notifications
- escalation
- audit where required

## 6. Every meaningful operation should consider API exposure

If an action is useful in the UI, there should normally be a documented API equivalent unless security, privacy, or implementation constraints justify exclusion.

APIs should support consistent:
- authentication
- scopes
- permissions
- filtering
- pagination
- sorting
- idempotency where needed
- audit
- errors
- versioning

## 7. MCP is a first-class product surface

Re:Solve should be usable by trusted AI and agent systems without brittle scraping or direct database access.

MCP tools must obey the same permission model as the UI and API.

Dangerous actions require stronger scopes, confirmation, approval, or deliberate exclusion.

## 8. AI is native but bounded

Built-in Re:Solve AI should assist with operational understanding, writing, search, analysis, and controlled actions.

AI must not bypass permissions or become the primary source of business truth.

Chatwoot AI remains architecturally separate.

## 9. PWA and responsive behavior are foundational

Mobile behavior is specified alongside desktop behavior.

Client portal flows must be excellent on mobile.

Admin workflows may optimize complex operations for larger screens but still require intentional responsive behavior.

Offline behavior, installability, update handling, push notifications, and safe caching must be planned deliberately.

## 10. Design for operations, not dashboard decoration

Avoid generic SaaS patterns by default.

Do not use rows of interchangeable KPI cards simply because they are easy to generate.

Each screen should express the hierarchy of the real work:
- attention
- state
- risk
- deadlines
- relationships
- next actions

## 11. Shared design primitives before bespoke components

Use a coherent design system.

Prefer shadcn/ui and proven accessible primitives where they fit. Use alternatives when they materially improve usability, data density, interaction quality, or accessibility.

Custom components should solve Re:Solve-specific problems, not reimplement common controls inconsistently.

## 12. Permissions are enforced server-side

Hidden UI is not authorization.

Every sensitive record and action must be protected by server-side permission checks.

Organisation isolation and property-level access must be explicitly testable.

## 13. Audit sensitive operations

Sensitive and consequential actions should produce durable audit events.

Examples include:
- permission changes
- vault reveals
- credential sharing
- invoice/payment changes
- connector configuration
- API token changes
- plugin installation
- security settings
- destructive actions
- AI actions with material side effects

## 14. Confidential information receives stronger controls

Vault items, credentials, sensitive files, and protected records must support stronger access controls than ordinary business records.

Specifications should consider:
- step-up authentication
- temporary access
- revocation
- expiry
- download controls
- redaction
- access logging
- secure deletion

## 15. External events are processed reliably

Connector webhooks and external events must be:
- authenticated or verified where supported
- idempotent
- auditable
- retryable
- observable
- recoverable

Failed external events should never disappear silently.

## 16. Automations use the same event model as the product

Automations should subscribe to well-defined domain events rather than feature-specific hacks.

Automation actions must respect permissions, rate limits, connector state, and audit requirements.

## 17. Client and admin experiences are intentionally different

The client portal is not the Admin OS with navigation hidden.

The Admin OS prioritizes operational speed and density.

The client portal prioritizes clarity, trust, collaboration, self-service, and mobile use.

They share business truth but not necessarily interaction design.

## 18. Realistic demo data is required

Specifications and prototypes should use realistic domain examples that expose complex relationships and edge cases.

Avoid placeholder ecosystems such as Acme Corp / John Doe when more representative data would produce a better product decision.

## 19. Build slowly, specify deeply

The Product Bible should anticipate the complete system.

Lovable build prompts should remain narrow.

A large specification is not permission to implement a large batch.

## 20. Existing Re-Solve behavior is evidence, not law

The current Re-Solve repository contains valuable product logic and ideas.

Keep what remains correct.
Adapt what is useful.
Replace what conflicts with the new architecture.
Remove what is duplicative or no longer strategically useful.

Do not preserve implementation technology solely for historical continuity.

## 21. Portability is a compatibility requirement

Development may use Lovable and Supabase fully.

Product architecture must avoid unnecessary assumptions that make the final application impossible to operate independently of Lovable.

Portability concerns belong in implementation planning, not in every user-facing feature description, but they remain a governing constraint.

## 22. Failure states are product states

Loading, empty, partial, error, offline, permission-denied, read-only, suspended, degraded-connector, and recovery states must be designed intentionally.

A feature is not complete if only its happy path is specified.

## 23. Extensions must have explicit boundaries

Plugins and connectors should extend supported interfaces rather than modifying unrelated core behavior.

Extension points must be documented, versioned, permissioned, and observable.

## 24. Settings is architecture made visible

Settings must reflect the product's real structure rather than becoming a miscellaneous configuration dump.

Each configurable capability should have a clear owner, scope, defaults, permissions, validation, audit policy, and reset/recovery behavior.

## 25. Security and usability should reinforce each other

Security should be visible where users need confidence and quiet where it does not require attention.

Strong controls should be understandable, recoverable, and integrated into the workflow rather than added as obscure administrative obstacles.