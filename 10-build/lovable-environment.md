# Re:Solve Lovable Development Environment

## Purpose

Re:Solve will be built in Lovable during active product development. Lovable is the development environment and product-building interface. It may use Lovable-native capabilities, Supabase, preview environments, and demo data freely during development.

The finished application must remain portable: Re:Solve must be capable of running independently of Lovable after export/self-host deployment. Lovable is not a required production runtime dependency.

This document defines only build compatibility and development discipline. It intentionally does not prescribe production domains or hosting details that Lovable does not need in order to build correctly.

## Governing rule

Build everything in Lovable, but do not create business functionality that fundamentally requires Lovable-hosted runtime services to continue functioning after code export.

## Development approach

The Product Bible may be exhaustive. Lovable receives only the current build slice plus the permanent architectural/design rules it needs.

Workflow:

```text
Product Bible
→ select one bounded slice
→ prepare Lovable prompt
→ build in Lovable
→ test/review
→ compare against acceptance criteria
→ refine
→ commit/sync to GitHub
→ next slice
```

Never ask Lovable to implement an entire loaded OS in one prompt.

## Source of truth

- Re-Solve-Product-Bible: canonical product behavior/specification
- Re-Solve: application source repository
- Lovable: active build environment
- GitHub: persistent source history and portability boundary

When generated implementation conflicts with the Product Bible, the Product Bible wins unless deliberately amended.

## Preferred implementation model

Favor Lovable's current preferred frontend/backend model over the legacy Re-Solve architecture unless a product requirement clearly requires otherwise.

During development, Supabase is an acceptable and preferred foundation for:
- PostgreSQL data
- authentication
- storage
- realtime where useful
- backend/server functions where appropriate
- demo data

Do not preserve NestJS, TypeORM, GraphQL/Apollo, Redis, or other legacy architecture merely because the current Re-Solve repository used them.

Preserve valuable business behavior and product logic, not obsolete implementation constraints.

## Portability boundaries

Even while using Supabase/Lovable during development:
- business rules should not be buried inside page components
- provider-specific integrations use connector boundaries
- plugins use declared extension contracts
- database migrations/schema changes are versioned
- environment variables/secrets are documented
- file storage is abstractable toward standard/self-hostable storage patterns
- authentication-dependent business code should use shared identity/permission services
- background work should use explicit jobs/events rather than hidden browser behavior
- APIs and MCP use server-side business services, not UI scraping

The target is the ability to replace hosted backing services or self-host compatible equivalents without rewriting the product surface.

## Demo data

Lovable development uses rich, realistic demo data.

Avoid generic filler such as "Acme Corp" where realistic domain structure tests the product better.

Demo data should include:
- multiple organisations
- multiple contacts per organisation
- contacts with multiple memberships
- hierarchical properties
- websites and journals
- active and completed projects
- opportunities/proposals/contracts
- invoices in multiple states
- payment examples
- approvals
- files
- Vault metadata/examples without real secrets
- notification history
- connector health states
- Chatwoot conversation references/summaries
- automation runs
- plugin examples

Demo records should intentionally cover empty, healthy, warning, overdue, blocked, degraded, permission-limited, and archived states.

## Framework and component policy

### Primary UI foundation

Use a coherent modern React design-system approach supported well by Lovable.

Default component foundation:
- shadcn/ui
- Radix primitives where appropriate
- Tailwind-compatible token system
- Lucide or the established Re:Solve icon system

Use shadcn as a foundation, not as a visual identity. Default component styling must be transformed into the Re:Solve design language.

### Alternatives

Lovable may use stronger alternatives when they materially improve a complex requirement, especially for:
- advanced data grids
- rich editors
- charts
- command palettes
- date/range selection
- drag/drop
- complex forms
- kanban/timeline/Gantt interactions
- file management

Alternative libraries must:
- integrate visually with the design system
- meet accessibility expectations
- support responsive behavior
- avoid locking core product logic into a proprietary runtime
- be justified by UX capability rather than novelty

Do not introduce multiple overlapping libraries for the same primitive without a clear need.

## Design skills

Lovable should actively use design/review skills and relevant framework knowledge rather than generate generic dashboards from scratch.

Required skill categories:
- product/interface design
- information architecture
- responsive design
- accessibility
- shadcn/component-system usage
- form design
- operational data tables
- dashboard design
- flow/prototype validation
- design review/redesign
- PWA/mobile review

Where Lovable provides built-in design/accessibility/redesign skills, use them at the appropriate build/review stages.

Project-specific skills should supplement, not conflict with, Re:Solve Product Bible rules.

## Installed planning skills

The Product Bible currently uses:
- `re-solve-spec`
- `flow-by-flow`
- `flow-prototype`

Equivalent build-side skills should be made available to Lovable where supported, especially for:
- feature slicing
- UI implementation
- forms
- data tables
- security review
- plugin work
- connector work
- migration review
- release review
- debugging
- self-host portability review

## Design-system rules

Lovable must not create random bespoke primitives in feature pages when an approved shared primitive exists.

Preferred layering:

```text
primitive/library
→ Re:Solve shared component
→ domain composite
→ feature/page
```

Examples of Re:Solve composites:
- RecordHeader
- RecordTabs
- StatusBadge
- HealthIndicator
- AttentionItem
- ActivityTimeline
- PropertyPicker
- OrganisationPicker
- PersonPicker
- ApprovalPanel
- FilePicker
- VaultAccessBadge
- ConnectorHealthCard
- EmptyState
- PermissionGate
- QuickCreate
- CommandMenu

## Non-generic design requirement

Re:Solve must not look like a stock SaaS template.

Avoid:
- walls of identical KPI cards
- arbitrary gradient hero panels
- decorative charts without decisions attached
- giant whitespace that reduces operational density
- every page being a card grid
- generic blue-purple startup styling
- inconsistent custom controls

Prefer:
- strong hierarchy
- calm density
- record relationships
- attention-driven layouts
- contextual side panels/drawers
- powerful tables and saved views
- compact action clusters
- command/search workflows
- meaningful status and health visualization
- contextual summaries rather than decorative metrics

The Admin OS may be denser than the Client Portal. The Client Portal should remain calmer and task-focused while sharing the same visual DNA.

## Responsive/PWA requirement

PWA and responsiveness are requirements from the first implementation slice.

Every build slice must consider:
- phone
- tablet
- laptop
- desktop
- wide desktop where relevant
- touch targets
- keyboard navigation
- safe areas
- installable PWA behavior
- standalone display mode
- service-worker/update behavior
- push notification compatibility
- offline/poor-network state

Do not design desktop-only screens and promise to "make responsive later."

### Mobile Admin

Mobile Admin prioritizes:
- attention queue
- My Work
- approvals
- notifications
- client/property/project lookup
- urgent status changes
- quick create
- incident response

Very complex editors may be read-only or simplified on phone with an explicit explanation.

### Mobile Client Portal

The Portal should be fully usable for common client tasks:
- view attention items
- approve/reject
- check project/property status
- view/pay invoice
- open support
- access files
- respond to requests
- manage notifications/account

Mobile navigation may differ from desktop when that improves usability.

## Accessibility

Target WCAG 2.2 AA for core product surfaces.

Each slice must check:
- semantic structure
- keyboard access
- visible focus
- dialog focus management
- labels/descriptions
- color contrast
- non-color status cues
- reduced motion
- screen-reader naming
- table alternatives on narrow screens
- error announcement

Run accessibility/design review before accepting UI-heavy slices.

## State completeness

A page is not complete because the happy path renders.

Every slice specifies and implements applicable:
- loading
- skeleton
- empty
- first-use
- populated
- success
- error
- partial data
- degraded connector
- permission denied
- read-only
- offline
- stale cached data
- destructive confirmation

## Forms

Default form pattern:
- schema validation
- accessible labels/descriptions
- inline validation
- server validation
- save progress/state
- clear submit feedback
- unsaved-change protection where consequential
- responsive field layout
- permission-aware fields

Use a shared validation approach such as Zod where compatible with the chosen Lovable stack.

## Data tables and operational lists

Operational lists should consider:
- search
- filters
- sort
- saved views
- column visibility
- pagination/infinite loading
- row selection
- bulk actions
- quick actions
- export permissions
- keyboard navigation
- mobile list alternative

Do not put every dataset into a basic HTML table with no workflow support.

## Testing expectations

The chosen Lovable-compatible testing stack should cover:
- unit/domain logic
- integration/server behavior
- component behavior
- end-to-end critical flows
- permission denial
- cross-organisation/property denial
- responsive/PWA smoke behavior
- accessibility checks where practical

Vitest/React Testing Library/Playwright are acceptable when compatible with the generated stack, but exact tools may follow Lovable's current preferred ecosystem.

## GitHub workflow

Lovable-generated source should remain synchronized with the Re-Solve repository.

Prefer small commits/changes aligned to Product Bible slices.

Each completed slice should identify:
- Product Bible spec
- acceptance criteria satisfied
- migrations
- new permissions
- new environment variables
- new dependencies
- new plugin/connector contracts
- known deferred items

## Environment configuration

Use documented environment variables and secret management.

Group external providers consistently, e.g.:
- CHATWOOT_*
- BACHS_*
- OPENROUTER_*
- OPENBAO_*
- DOCUMENSO_*
- UPTIME_KUMA_*
- OJS_*
- WOOCOMMERCE_*

Do not put production secrets into prompts, demo data, client code, or committed configuration.

## Development connector policy

During Lovable development use:
- mock/demo connectors where useful
- sandbox/test provider accounts
- non-production API keys
- dedicated demo instances

UI should support realistic connected, degraded, disconnected, authentication-required, rate-limited, and failed states even before every real connector is implemented.

## Build-slice prompt contract

Every Lovable implementation prompt should include only:
- the current objective
- relevant Product Bible excerpt/requirements
- relevant permanent architecture/design rules
- exact in-scope routes/components/records
- acceptance criteria
- demo data needed
- explicit out-of-scope items

It should explicitly say not to pre-build later slices.

## Slice acceptance review

Before moving on, review:
- behavior against spec
- flow completeness
- visual quality
- responsiveness
- PWA implications
- accessibility
- permissions
- loading/empty/error states
- API implications
- audit/notifications where applicable
- regression against existing slices

## Self-host portability review

Periodically verify:
- source can build outside Lovable
- application does not import a Lovable-only runtime requirement for core business behavior
- database schema/migrations are exportable/versioned
- auth/storage/provider boundaries remain explicit
- environment requirements are documented
- API/MCP are deployment-independent
- PWA assets/service worker are ordinary application assets

This is a compatibility check, not a reason to slow down normal Lovable development.

## Initial foundation sequence in Lovable

When implementation begins, do not start by building all modules.

Recommended progression:
1. project/import and architecture inspection
2. shared design tokens/components
3. PWA/responsive shell foundation
4. Admin shell
5. Client Portal shell
6. identity/permissions foundation
7. realistic demo-data foundation
8. Dashboard first slice
9. review
10. next bounded Product Bible slice

## Acceptance criteria

- all active product development can occur in Lovable
- Supabase/demo data can be used freely during development
- implementation favors Lovable-compatible architecture over legacy Re-Solve technology
- exported source remains normal maintainable application code
- product does not require Lovable runtime for core operation after export
- PWA/responsive behavior exists from foundation
- shared design primitives prevent generic/inconsistent page generation
- Product Bible slices, not giant prompts, drive implementation
- GitHub remains a usable source/portability boundary
