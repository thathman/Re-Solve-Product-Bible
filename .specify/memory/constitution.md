# Re:Solve Product Constitution

This repository is the canonical Product Bible for Re:Solve. These rules override historical implementation assumptions and ordinary feature convenience unless explicitly amended in the Product Bible.

## I. Specify deeply, build in bounded slices
The Product Bible may design the complete operating system. Lovable receives only the current coherent build slice plus persistent Knowledge and relevant skills. Never build a whole major module because adjacent capability is already specified.

## II. Product behavior over legacy implementation
The existing Re:Solve application repository is reference evidence for behavior, edge cases and prior ideas. Its NestJS/GraphQL/TypeORM-era architecture is not binding. Favor Lovable's current strong application patterns while preserving portable product boundaries.

## III. Lovable-first, runtime-portable
All active product development is performed in Lovable. Supabase and Lovable-native development capabilities are acceptable. Exported Re:Solve must remain understandable and capable of independent self-hosting without a Lovable runtime dependency. Portability is a design boundary, not permission to build premature production infrastructure.

## IV. One application, two role-shaped shells
Admin OS and Client Portal share canonical data, identity, permissions, platform services, design tokens, plugins/connectors and audit. Admin is denser and keyboard-forward. Portal is calmer, guided and mobile-first. Portal is not Admin with controls hidden.

## V. Workspace, Operating Entity and Organisation are distinct
Each deployment has a Workspace. Operating Entity/Brand is the business doing the work. Organisation represents clients, prospects, vendors, partners and institutions. Airix Media is the first Operating Entity, not an ordinary client Organisation.

## VI. Principal-based authorization
`Principal` is the authorization actor; `User` means a human authenticated identity. Service Accounts, API Clients, MCP Clients, Plugins and Connectors are non-human Principal types. Roles are permission bundles. Authorization is capability + scope and is enforced server-side with negative cross-Organisation/Property tests.

Canonical permission grammar is `domain.action` or `domain.resource.action`.

## VII. Explicit product exclusions
Re:Solve core must not drift into HR management, payroll, recruitment, leave/attendance, employee performance management, Timesheets/Time Tracking, or Client Service Consumption/remaining-hours/credit metering.

Assignments, teams, deadlines, estimates, recurring tasks and operational expenses do not create an HR/Timesheet domain.

## VIII. Core, Plugin and Connector remain distinct
Core owns foundational identity/business/platform truth. Plugins add business capability. Connectors integrate external specialist systems/providers. A provider package may be distributed as a Plugin that registers a Connector implementation, but business domains remain provider-neutral.

## IX. Chatwoot support boundary
Chatwoot owns managed support conversations/messages, web chat, inboxes/channels, routing, agents/teams, support attachments, support Knowledge and Captain. Re:Solve owns client/property/service context, entitlement, incidents, safe references/summaries, business reporting and deep links. Do not rebuild the Chatwoot agent console or mirror every message.

## X. Operational communications boundary
WhatsApp/Baileys is primarily Re:Solve-to-client operational communication: status updates, reminders, approvals, billing/renewal notices, property alerts and direct operational messages. Client end-customer support remains a Chatwoot concern.

## XI. Àríyá is Re:Solve AI
The user-facing built-in AI is **Àríyá**. Àríyá remains separate from Chatwoot Captain, inherits caller permissions, uses controlled tools/registered Actions, shows evidence/freshness, distinguishes inference from system fact, and never receives arbitrary SQL or generic Vault secret access.

## XII. Attention, Notification, Activity and Audit are separate primitives
Attention = unresolved condition that matters now.
Notification = recipient-specific awareness/delivery.
Activity = durable business chronology.
Audit = append-only evidentiary security/operational history.
Dashboard, My Work, Portal Home and Àríyá should consume shared primitives rather than invent shadow status systems.

## XIII. Action Registry unifies consequential operations
Reusable business mutations should be registered Actions shared where practical by UI, Command Palette, Àríyá, API, MCP, Automations and plugins. Every Action declares permissions, scope, risk, confirmation/approval/step-up policy, side effects and audit. Discoverability is never authorization.

## XIV. Properties, Monitoring and Renewals are first-class
Property is a central native object with hierarchy, services, projects, support, files, Vault, connectors, access, monitoring and renewals. Re:Solve includes a native Monitoring Engine and independently deployable Worker/Probe architecture. External monitors such as Cloudflare Health Checks or Uptime Kuma are optional signal sources. Property Posture is explainable and source/freshness-aware.

Domain, hosting, certificate, service, contract and similar expiries use first-class Renewal/Expiry Obligations and a Renewal Desk rather than isolated date badges.

## XV. Files and Secure Vault have separate access domains
Files handles ordinary documents. Secure Vault handles protected confidential information/files. A protected confidential document must not retain a second ordinary File access path. Vault values are excluded from generic search, logs, Notifications, unsafe PWA caches and ordinary Àríyá/MCP retrieval.

## XVI. Document Studio preserves immutable commercial evidence
Proposal, Estimate/Quote, Contract, Invoice, Receipt, Statement and other generated documents use the shared Document Studio. Accepted/executed material receives an immutable Final Snapshot. Signature providers such as Documenso own signature transaction execution; Re:Solve owns the business document and lifecycle.

## XVII. Provenance and sync authority are visible
Synced, imported, derived and AI-produced information must preserve source/authority/freshness where material. Every Connector declares sync direction and conflict policy. External IDs are mappings, not canonical identity.

## XVIII. API and MCP are first-class
Meaningful business operations should normally have a documented programmatic equivalent. API/MCP use the same canonical permissions/business services where practical. MCP exposes curated tools, not arbitrary SQL/database/filesystem/provider access. High-risk operations require narrow scopes and stronger controls.

## XIX. PWA, responsive design and accessibility start at foundation
Phone, tablet, laptop, desktop and installed-PWA behavior are part of definition of done. Portal common flows must not require desktop. Admin essential operations remain usable on phone. Sensitive data receives strict cache policy. Target WCAG 2.2 AA.

## XX. Core UI Component Framework is mandatory infrastructure
Re:Solve owns a reusable Core UI Component Framework. Mandatory primary sources/influences are shadcn/ui, Untitled UI React and Tremor, supported by React Aria/Base UI/Radix, TanStack and approved specialist libraries where warranted. Use them heavily, then normalize final behavior into Re:Solve-owned tokens/components.

Sidebar, TopBar, ResolveAvatar/AccountMenu, Notifications, Search/Command, Quick Create, Àríyá, record headers, tables, forms and global states require production-quality design. The foundation must include a Component Gallery/Storybook-equivalent.

## XXI. Navigation must stay simple as the OS grows
Admin uses a clear labeled left sidebar, shallow human-readable major areas and area-level tabs/views. Portal is even simpler. Reject Odoo-style app launchers/module grids, Twenty-style object/module switching as the primary mental model, icon-only root navigation, uncontrolled plugin root entries and endless nested trees. Favor the clarity of a well-structured service CRM such as Perfex/Brevo.

## XXII. Failure states and design QA are product states
Loading, empty, first-use, partial, stale, error, permission-denied, read-only, offline, degraded-provider and recovery states must be deliberately designed. A slice is not complete after the happy path. Completion includes functional, security, responsive/PWA, accessibility, visual/Core UI consistency and portability review.

## XXIII. Extensions use declared platform contracts
Plugins/connectors extend through named UI slots, events, jobs, Actions, Notifications, API/MCP and namespaced data contracts. They must not silently mutate unrelated core navigation, schemas, permissions or secrets.

## XXIV. Product Bible before new product truth
If implementation reveals a real ambiguity or contradiction, stop, record it and update the Product Bible before allowing code to establish a new canonical rule.
