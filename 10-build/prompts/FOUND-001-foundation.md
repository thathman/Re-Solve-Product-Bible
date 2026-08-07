# FOUND-001 — Re:Solve Application Foundation

## Objective
Prepare Re:Solve as a Lovable-first, portable, responsive application foundation without implementing business modules.

After this slice, reviewers should be able to launch the app, authenticate into representative Admin and Client Portal shells, see the design system working across responsive breakpoints, and verify the project is ready for bounded feature slices.

## Product Bible sources
Read and follow:
- `00-foundation/product-thesis.md`
- `00-foundation/principles.md`
- `00-foundation/terminology.md`
- `00-foundation/actors-and-roles.md`
- `00-foundation/information-architecture.md`
- `09-design/design-direction.md`
- `09-design/design-system.md`
- `01-admin/shell.md`
- `02-portal/shell.md`
- `03-platform/pwa.md`
- `08-security/security-architecture.md`
- `10-build/lovable-knowledge.md`
- `10-build/architecture-portability-checklist.md`
- `10-build/demo-data-blueprint.md`

## Actor and goal
Internal staff and client users can enter a coherent Re:Solve application shell that correctly resolves their experience, feels intentionally designed across devices, and provides a stable foundation for future feature slices.

## In scope

### 1. Inspect current Re-Solve source
Treat the existing Re-Solve repository as behavior/reference material.
Do not preserve legacy architecture merely because it exists.
Identify reusable brand/design assets and useful behavior, but favor Lovable's preferred current application model.

### 2. Establish application architecture
Use Lovable's preferred React/full-stack approach and Supabase integration where appropriate.

Create clear conceptual boundaries for:
- app shells
- shared UI
- auth/identity
- permissions
- domain/data services
- connector/plugin extension points

Do not scaffold every future domain.

### 3. Establish shared design system
Use shadcn/ui and accessible Radix-style primitives as the default base.

Establish reusable tokens/primitives for:
- typography
- surfaces/backgrounds
- spacing
- borders
- radii
- elevation
- status colors
- focus states
- buttons
- inputs
- selects
- dialogs/drawers
- dropdowns
- tooltips
- badges/status indicators
- skeletons
- empty states
- alerts
- navigation
- page headers

The result must not resemble a generic dashboard template.

### 4. Establish Admin shell
Create the shell and navigation structure only.

Include:
- responsive sidebar/navigation
- top bar
- breadcrumb/context area where specified
- global command/search entry placeholder
- notifications entry placeholder
- profile/account menu
- clear active-route behavior
- collapsed navigation behavior where appropriate
- mobile/tablet navigation adaptation

Routes may point to deliberate "not built in this slice" placeholders where needed.
Do not create feature pages behind them.

### 5. Establish Client Portal shell
Create the client-facing shell only.

Include:
- calmer navigation than Admin
- responsive/mobile-first behavior
- account/profile entry
- notifications entry placeholder
- support/chat entry placeholder
- client-safe empty placeholder content

Do not build Portal Home feature content yet.

### 6. Identity/demo foundation
Using Supabase if appropriate, create only the minimum identity data needed to demonstrate:
- internal staff user
- client organisation user
- membership/role resolution
- staff routes versus client routes
- permission-denied path

Use demo identities from the demo-data blueprint.

Do not build complete Team & Access management yet.

### 7. Permission gate foundation
Create a reusable capability-aware guard/policy pattern.
Do not rely only on hiding navigation.

Demonstrate at least:
- authenticated staff allowed into Admin shell
- authenticated client allowed into Portal shell
- client denied from Admin shell
- unauthorized route produces a deliberate denial state

### 8. PWA base
Establish:
- manifest
- app icons/placeholders
- installable configuration
- service-worker/offline-shell strategy
- update lifecycle foundation
- safe offline fallback shell
- explicit prohibition on caching future Vault secrets/sensitive tokens

Do not implement complete push-notification delivery yet.

### 9. Shared application states
Create reusable patterns for:
- loading
- skeleton
- empty
- error
- permission denied
- offline
- unavailable/not-yet-built placeholder

### 10. Accessibility baseline
Verify:
- keyboard navigation
- focus visibility
- semantic landmarks
- dialog/menu focus handling
- touch targets
- contrast
- reduced-motion consideration

### 11. Quality baseline
Use the testing/tooling that best fits the generated Lovable stack.
At minimum establish a practical path for:
- TypeScript checks
- linting
- component/unit testing
- browser/flow testing

Add only dependencies required for this slice.

## Out of scope
Do not implement:
- Dashboard business widgets
- Organisations CRUD
- Contacts CRUD
- Properties
- Projects
- Billing
- Chatwoot integration
- WhatsApp
- Secure Vault
- Notifications delivery engine
- Automations
- Plugins marketplace/runtime beyond extension-friendly boundaries
- Connectors UI
- API product surface
- MCP
- Re:Solve AI
- Monitoring
- Reports
- full Settings

Do not create placeholder schemas for all these modules.

## Demo data
Seed only:
- Airix Media internal organisation
- Hendrix Nwaokolo — staff Owner/Administrator demo identity
- Ada Eze — Account Manager demo identity
- Kampala University — client organisation
- Dr. Sarah Kato — client Organisation Admin demo identity
- Grace Nambasa — property-restricted client user placeholder membership if property scope can be represented without creating the full Properties feature

Use obviously fictional development credentials/auth setup.

## Responsive expectations

### Phone
- Portal shell must be genuinely usable.
- Admin shell must remain usable for essential navigation even if dense workflows are optimized for larger screens.
- no desktop sidebar squeezed into phone width
- no horizontal page-level overflow

### Tablet
- adaptive navigation and content width

### Laptop/Desktop
- efficient Admin navigation
- strong information hierarchy
- no excessive empty space

## PWA/offline
- application shell may load offline where safe
- authenticated business data may remain online-only in this slice
- show a deliberate offline state rather than silent breakage
- never cache credentials/tokens beyond what the auth/runtime safely requires

## Security checks
- no secrets in client bundle/source
- client cannot access Admin route through URL manipulation
- permission checks are not visual-only
- development/demo configuration is clearly development-only
- auth/session handling uses provider best practices

## Portability checks
Run the `self-host-check` skill before completion.
Confirm:
- generated source is exportable
- no product-critical Lovable-only runtime dependency has been introduced unnecessarily
- Supabase/provider usage is reasonably centralized
- business identity/permission concepts are represented as Re:Solve concepts

## Acceptance criteria
1. App launches cleanly in Lovable.
2. Staff demo user enters Admin shell.
3. Client demo user enters Client Portal shell.
4. Client cannot access Admin shell.
5. Both shells share coherent design tokens but have visibly different density/IA.
6. Phone, tablet, and desktop layouts are intentional.
7. PWA manifest/service-worker foundation exists and does not cache sensitive future data.
8. Shared loading, error, empty, permission-denied, offline, and not-built states exist.
9. No major business module has been prematurely implemented.
10. shadcn/accessibility primitives are reused rather than reinvented.
11. Quality checks configured for the generated stack pass.
12. A portability review finds no unnecessary hard dependency on Lovable runtime services.

## Required Lovable completion report
Return:
- architecture chosen and why it fits Lovable
- meaningful files/components created or changed
- dependencies added
- identity/demo schema created
- routes created
- tests/checks run and results
- responsive/PWA checks performed
- portability concerns found
- any Product Bible contradiction found
- explicit list of adjacent features intentionally left unbuilt

## Stop condition
After satisfying FOUND-001, stop.
Do not proceed to Dashboard, Organisations, Properties, or other business functionality until a new build slice is provided.
