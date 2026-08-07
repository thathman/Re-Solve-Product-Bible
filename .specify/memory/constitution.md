# Re:Solve Product Constitution

This repository is the canonical Product Bible for Re:Solve.

## I. Specification before implementation
Every substantial capability is specified before it is built. The Product Bible may be exhaustive; individual Lovable build tasks must remain intentionally small, testable, and reviewable.

## II. Product behavior over legacy implementation
The existing Re:Solve repository is a source of product behavior, useful business logic, edge cases, and prior work. Its current technical architecture is not automatically binding. When rebuilding, favor the development model that works best with Lovable while preserving portability and product requirements.

## III. Portable application
Lovable and Supabase may be used freely during development, but product specifications must not require a proprietary Lovable runtime. The resulting product must remain compatible with eventual independent self-hosting.

## IV. Loaded operating system, not generic dashboard
Re:Solve must feel like a deeply considered operational workspace. Information hierarchy, workflow speed, density, responsiveness, state design, accessibility, and real operational usefulness take precedence over generic SaaS templates and decorative card grids.

## V. Core, plugins, and connectors are separate
Core owns foundational business records and platform capabilities. Plugins extend business functionality. Connectors integrate external systems. Provider-specific behavior must not leak throughout core domain logic.

## VI. Support boundary
Chatwoot owns managed client support: helpdesk, web chat on client properties, support conversations, support knowledge, agents/teams, and Chatwoot's own AI engine. Re:Solve enriches and manages the business context around that support but does not rebuild Chatwoot.

## VII. Communication boundary
WhatsApp/Baileys is primarily for Re:Solve-to-client operational communication, ticket/status updates, reminders, direct messages, and notifications. Client end-customer support remains a Chatwoot concern.

## VIII. AI boundary
Re:Solve has its own built-in AI capabilities. Re:Solve AI remains architecturally separate from Chatwoot AI, even if both use the same underlying model provider.

## IX. Secure Vault
The Secure Vault exists for controlled sharing and access to confidential information including credentials, passwords, keys, sensitive files, proposals, contracts, certificates, and secure notes. Access, step-up authentication, sharing, expiry, revocation, and auditability are first-class requirements.

## X. Notifications are a platform primitive
Every meaningful feature must explicitly consider notification events, recipients, priorities, delivery channels, user preferences, grouping, deduplication, escalation, deep links, and mandatory security/operational notices.

## XI. API and MCP first-class
Meaningful business operations should normally have documented API equivalents. Re:Solve must expose a carefully scoped MCP surface suitable for integrations with Claude, ChatGPT, OpenClaw/Hermes, Codex, and future AI agents. Read/write scopes, confirmation, redaction, rate limiting, and audit are mandatory considerations.

## XII. PWA, responsive design, and accessibility from the start
Phone, tablet, desktop, and installed-PWA behavior are part of the definition of done. Responsive layouts, appropriate mobile interaction patterns, push notifications, safe offline behavior, keyboard access, and accessibility must be specified rather than added later.

## XIII. Design system discipline
Use a coherent component and interaction system. Implementation should prefer shadcn/ui and high-quality alternatives when they materially improve a workflow. Do not create arbitrary bespoke controls or visual patterns that fragment the product.

## XIV. Platform-wide concerns
Every important capability must consider as applicable: permissions, organisation/property isolation, audit, notifications, automation, API, MCP, plugin extension points, connector interactions, files, search, security, responsive/PWA behavior, accessibility, loading/empty/error/offline states, and analytics.

## XV. Small build slices
Never ask Lovable to build an entire major product area at once. Comprehensive specs are decomposed into bounded slices with clear objectives and acceptance criteria, reviewed before proceeding to the next slice.
