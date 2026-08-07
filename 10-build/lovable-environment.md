# Re:Solve Lovable Development Environment

## Purpose
Re:Solve is built in Lovable during active product development. Lovable is the build environment; GitHub is the persistent source/portability boundary; Supabase may be used for development backend needs. The exported application must remain capable of independent self-hosting without a Lovable runtime dependency.

This document governs development compatibility and discipline, not production hosting/domain decisions.

## Governing rule
Build everything in Lovable, but do not make product-critical business behavior fundamentally depend on a proprietary Lovable runtime after export.

## Current Git sync constraint
As of 2026-08-07, Lovable Git sync can **export/create a new GitHub repository but cannot import an existing GitHub repository into a Lovable project**.

Therefore:
- current `thathman/Re-Solve` remains legacy behavior/reference during initial rebuild;
- create a fresh Lovable project;
- connect GitHub and let Lovable create a new private synced repository;
- build FOUND-001 there;
- do not overwrite/rename the legacy repository during setup;
- after FOUND-001 passes and with explicit owner approval, perform the one-time repository naming transition documented in `10-build/lovable-launch/GITHUB-TRANSITION.md`.

Renaming the connected repository itself is currently supported by Lovable sync; transferring/deleting/disconnecting it has stronger consequences and must not be done casually.

## Development flow
```text
Product Bible
→ choose one bounded slice
→ ensure Project Knowledge + relevant skills are current
→ send the slice prompt
→ build in Lovable
→ test/review
→ resolve acceptance blockers
→ Git sync/commit
→ Product Bible update if genuine product truth changed
→ next slice
```

Never ask Lovable to implement the complete loaded OS in one prompt.

## Context model
### Product Bible
Canonical full product truth. It is private and is not assumed to be directly browsable by Lovable.

### Project Knowledge
Compact durable Re:Solve rules that apply to every message. Use the paste-ready launch copy in `lovable-launch/PROJECT-KNOWLEDGE.md` and keep it within Lovable's current Project Knowledge limit.

### Skills
Task-specific playbooks loaded on demand. Install the canonical `resolve-*` skill catalogue from `10-build/lovable-skills/`.

### Build slice
The exact current feature/build requirement. Product Bible file paths in a slice are traceability references; the prompt itself must carry the requirements Lovable needs if the private Bible is not connected.

### Repository instructions
FOUND-001 creates a root `AGENTS.md` from the canonical launch template so critical architecture/build rules also live in exported source control and are readable outside Lovable.

## Preferred implementation model
Favor Lovable's current strongest React/full-stack patterns rather than preserving legacy NestJS, TypeORM, GraphQL/Apollo, Redis or other historical architecture merely for continuity.

Supabase is acceptable during development for:
- PostgreSQL/data;
- authentication;
- storage;
- realtime where useful;
- server/backend functions where appropriate;
- deterministic demo data.

Preserve valuable business behavior, not obsolete implementation constraints.

## Architecture boundaries
Even while using Lovable/Supabase:
- keep business rules outside presentation components;
- centralize data/provider access through domain/service/repository boundaries where practical;
- use canonical Principal/User/Membership/capability concepts rather than provider metadata as product truth;
- provider integrations use Connector boundaries;
- Plugins use declared extension contracts;
- version schema/data migrations;
- document environment variables/secrets;
- storage objects/URLs are not permanent business ids;
- background work uses explicit jobs/events rather than hidden browser behavior;
- API/MCP/Àríyá call controlled application services/Actions rather than scraping UI or querying arbitrary storage.

## Explicit exclusions
Do not introduce HR management, payroll, recruitment, leave/attendance, performance reviews, Timesheets/Time Tracking, or Client Service Consumption/remaining-hours/credits metering.

Projects may still use ownership, assignment, estimates, deadlines, milestones, recurring tasks and operational Expenses.

## Core UI Component Framework — mandatory
Re:Solve owns a source-controlled Core UI Component Framework.

Mandatory major sources/influences:
1. Re:Solve Product Design Language;
2. shadcn/ui;
3. Untitled UI React;
4. Tremor;
5. React Aria / Base UI / Radix where strongest;
6. TanStack Table / TanStack Query;
7. approved specialist libraries only for demonstrated needs.

Use these heavily, then normalize the result into Re:Solve tokens/components. Do not create library soup.

FOUND-001 must establish a Component Gallery/Storybook-equivalent and production-quality Sidebar, TopBar, ResolveAvatar/AccountMenu, Notifications chrome, Search/Command, Quick Create, Àríyá entry/panel foundation, mobile navigation and shared state components.

## Navigation
Navigation must stay shallow, labeled and understandable like a well-structured service CRM. Reject Odoo-style app grids/module launchers, Twenty-style object/module switching as the main mental model, icon-only root navigation, endless nested trees and uncontrolled plugin root items.

Major areas own their child tabs/views. The shell must remain simple as the product grows.

## Component/library policy
Prefer mature accessible primitives over custom reimplementations. Introduce specialist dependencies only when a current slice needs them.

Approved directions include:
- shadcn/ui + React Aria/Base UI/Radix for accessible application controls;
- Untitled UI React for high-quality application composition/pattern influence;
- Tremor/Recharts-style patterns for meaningful operational analytics;
- TanStack Table for default operational tables;
- TanStack Query or equivalent for coherent async server state;
- dnd-kit for accessible reordering/drag-drop;
- React Flow for automation/process canvas when complexity warrants it;
- an enterprise grid only when a true spreadsheet/grid workflow cannot be served cleanly by the default table stack.

## PWA/responsive/accessibility
PWA and responsive behavior begin in FOUND-001.

Every relevant slice considers phone, tablet, laptop, desktop, standalone PWA, touch, keyboard, poor network and safe offline states. Portal common flows must not require desktop. Admin essential operational flows remain usable on phone even when complex editors prefer larger screens.

Sensitive Vault values and equivalent protected content are never intentionally cached for offline access. Target WCAG 2.2 AA.

## State completeness
Implement applicable loading, skeleton, empty, first-use, success, error, partial/stale, degraded provider, permission denied, read-only, offline and destructive-confirmation states. Happy path alone is incomplete.

## Security
Use capability + scope authorization server-side. UI hiding is not authorization. Negative cross-Organisation/Property tests are required. Secrets do not belong in prompts, committed config, client bundles, generic logs or demo data.

High-risk reusable operations should use Action Registry contracts with explicit risk, confirmation, approval/step-up and audit.

## Demo data
Use one coherent fictional universe. Airix Media is the first Operating Entity. Client Organisations and demo people are fictional. Never use real client credentials, secrets or private personal data.

FOUND-001 seeds only identity/access examples required for shell behavior. Later domain slices expand deterministic seed/reset data.

## Testing and QA
Use the strongest stack-compatible quality setup, typically strict TypeScript, lint/format, component/unit tests and browser flows such as Playwright where appropriate.

A UI-heavy slice must also pass:
- responsive/PWA review;
- accessibility review;
- Core UI consistency/design review;
- security/permission review;
- portability review when architecture/provider coupling changes.

`resolve-release` is the final go/no-go review for every build slice.

## GitHub workflow
The active Lovable-created repository is the synced application source during build. Prefer changes aligned with bounded Product Bible slice ids and avoid giant unrelated commits.

Each completed slice should identify:
- slice id/Product Bible traceability;
- acceptance criteria;
- migrations/data changes;
- new permissions/Actions;
- new environment variables/dependencies;
- plugin/connector contracts;
- tests/reviews;
- deferred scope.

Do not disconnect/reconnect Git sync casually because current Lovable behavior creates a new repository on reconnect.

## Environment configuration
Use documented secret/environment handling. Provider-specific variables remain isolated behind Connectors rather than scattered through business code. Possible future prefixes include `CHATWOOT_*`, `BACHS_*`, `OPENROUTER_*`, `DOCUMENSO_*`, `CLOUDFLARE_*`, `OJS_*`, `WORDPRESS_*`, `WOOCOMMERCE_*` and optional compatibility providers such as `UPTIME_KUMA_*`.

Do not configure production provider secrets during early demo slices.

## Build prompt contract
Every Lovable implementation request states:
- exact slice id/objective;
- exact actor/goal;
- requirements that matter to this slice;
- in scope/out of scope;
- existing Core UI/service boundaries to reuse;
- data/permission/state/PWA/accessibility needs;
- acceptance criteria;
- required skills/reviews;
- stop condition.

Do not rely on Lovable having access to the private Product Bible merely because the prompt references a file path.

## Portability review
Periodically verify:
- exported source builds outside Lovable;
- no product-critical Lovable-only runtime dependency;
- migrations/schema are reproducible;
- auth/storage/provider boundaries are explicit;
- UI/design system is source-controlled;
- PWA assets/service worker are ordinary application assets;
- API/MCP/Actions use portable application services.

This is compatibility discipline, not a reason to build Kubernetes, reverse proxies, multi-region infrastructure or a production migration away from Supabase during product development.

## Official current Lovable references
- https://docs.lovable.dev/features/knowledge
- https://docs.lovable.dev/features/skills
- https://docs.lovable.dev/integrations/github
