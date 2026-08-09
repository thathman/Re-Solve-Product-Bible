# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — SHELL-CTRL-001 IMPLEMENTED / CONDITIONAL CLOSURE — CLIENT HOME R2 STRUCTURE RETAINED BUT OWNER HAS REOPENED VISUAL DEPTH — NEXT: ADMIN SIDEBAR SEARCH + CLIENT DARK ANCHOR / MOTION PASS**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client-facing visual authority: `Airix360/AM-Client-Docs` Design System + `Airix360/airixmedia-web`
- Owner-supplied mockups/HTML are reference material only unless a later decision explicitly promotes an interaction/anatomy to canonical.
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval.

## Frozen security / architecture
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only. Private server functions/routes independently authorize at their server boundary.
- Normal user reads use caller-scoped Supabase + RLS; generated `supabaseAdmin` remains quarantined/unused by application authorization.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider/Zod/access errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- `requireActiveStaff()` / `getAdminAccess()` remain frozen for production Admin authorization.
- `requirePortalAccess()` / Portal parent access gate remain frozen for production Portal authorization.
- `requireActiveOrganisation(organisationId)` freshly revalidates exact active organisation access.
- `rs_portal_org` is an untrusted UUID-only context pointer, never authorization evidence.
- No service-role application path, broad RBAC, domain persistence, seed/test identities or public registration exists yet.

## Frozen functional surfaces
- Foundation + Core UI C1-C5E are frozen.
- `/ui` remains dev-only.
- Admin routes: Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Portal family: `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Auth routes: `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`.
- `/select-organisation` remains outside `/_portal` and uses canonical `getSafeRedirect()`.

## Visual dialects
### Admin
- Admin remains the Lucid-style Re:Solve operational dialect.
- Inter typography, neutral/graphite structure, restrained Lucide, subtle borders, low shadow, denser operational composition.
- Existing Sidebar/AdminShell architecture remains canonical.
- Account placeholder remains `Amara Okafor` / `Administrator`.
- Controlled semantic color accents are desired without turning Admin into a rainbow dashboard.

### Client-facing
- Auth + Client Portal use the Airix/Re:Solve client dialect.
- Space Grotesk = client UI/body; Instrument Serif italic = greetings/display; JetBrains Mono = currency/dates/identifiers/technical metadata selectively.
- Warm paper/surface/ink remains the light-mode base, with terracotta as brand/action accent.
- Client Portal has a scoped warm-charcoal dark mode and must keep all client semantic/surface tokens coherent in that mode.
- tool-like 3–6px radii; borders over shadows; elevation only for floating layers.
- bundled/self-hosted fonts only.

## Shared controlled-color direction
**OWNER REQUEST / CANONICAL**
Re:Solve should feel alive and recognizable, not monochrome/plain, while avoiding gimmicky rainbow SaaS styling.

Semantic family:
- brand / primary emphasis: terracotta.
- information / review / support: blue/cyan.
- healthy / success: green.
- warning / degraded / expiring: amber.
- danger / overdue / failing: red/coral.

Rules:
- neutral/warm canvases remain dominant; color is punctuation, not wallpaper.
- prefer tinted wells, section bands, status chips, dots, rails, progress segments, icon accents and selected indicators.
- distinct regions may use semantic or tonal background surfaces where they improve page rhythm and hierarchy.
- do not assign random colors to navigation items.
- no gradients, neon, rainbow card grids or glassmorphism.
- preserve accessible contrast and frozen focus-visible behavior.

### Client visual-depth rule
**OWNER CLARIFICATION / CANONICAL**
- Client pages should not be an uninterrupted field of paper/beige surfaces.
- It is valid and desirable for a major client page to contain **one strong dark anchor region** when it clarifies hierarchy, status or current work.
- The owner specifically likes the energy of the supplied Client Home HTML: dark featured surface, clear progress, layered contrast and motion. Those are design principles to reinterpret, not an instruction to copy its exact layout.
- Use restrained motion for state/progress: short, one-shot/reveal transitions rather than looping decoration. Respect `prefers-reduced-motion`.
- Dark anchors may use subtle technical line/grid texture, inverse typography and semantic accents, but must remain tool-like rather than promotional/hero marketing blocks.
- Do not reintroduce an embedded Àríyá Home section; Àríyá remains a floating shell control.

## Reference-use rule
**OWNER CORRECTION / CANONICAL**
- Never blindly clone an attached sample page.
- Samples provide visual vocabulary, content clues and useful interaction ideas; they are not automatic layout specifications.
- Re:Solve surfaces must be independently designed from product hierarchy and workflows.
- Before freezing a page, verify it is not merely a React transcription of a mockup.

## Auth capability plan
**FUNCTIONAL AUTH FROZEN; EXPANSION TRACKED, NOT YET IMPLEMENTED**
- No public registration.
- Intended first-account flow: staff/admin creates account -> invite link -> onboarding -> set password -> optional passkey -> optional TOTP -> optionally link Google/GitHub -> finish onboarding -> authorized destination.
- Google/GitHub must not create public accounts.
- ALTCHA planned for abuse-prone Auth operations.
- Planned sign-in methods: password, magic link, Google, GitHub, passkey; TOTP is MFA/AAL2.
- WhatsApp authentication remains a future preflight; official WhatsApp OTP preferred. Baileys is messaging/connector infrastructure.
- Current remote Unsplash Auth image is temporary and must be removed during later Airix Auth redesign.
- Details: `10-build/lovable-launch/AUTH-EXPANSION.md`.

## AI + support architecture
**OWNER-CORRECTED / CANONICAL**
Full authority: `10-build/lovable-launch/AI-SUPPORT-ARCHITECTURE.md`.

- Àríyá is Re:Solve's own AI and exists only inside Re:Solve.
- Àríyá is not Captain and is not powered by Captain.
- Re:Solve human escalation: `Re:Solve -> Àríyá -> dedicated owner/provider Re:Solve-support Chatwoot inbox -> human agent`.
- Captain MUST be disabled on that Re:Solve human-takeover inbox.
- Separately, an individual client website/property may embed its own Chatwoot inbox. Captain may be enabled on that specific property-support inbox/site when the provider owns that support responsibility.
- Do not cross these two domains.

## SHELL-CTRL-001 review
**IMPLEMENTED / FUNCTIONALLY SAFE / CONDITIONAL BEFORE FREEZE**
Verified app head: `bc72318e0a492f61b18faf156bd1c56289bb5833`.
Compared with `14624370102d615792f1ac309b3a84a0cb0d124f`, changed only shell/theme/Home visual files:
- `src/components/shell/admin/AdminShell.tsx`
- `src/components/shell/admin/AdminTopBar.tsx`
- `src/components/shell/portal/PortalShell.tsx`
- `src/components/shell/portal/PortalTopBar.tsx`
- removed `src/components/shell/portal/PortalHelpLauncher.tsx`
- added `src/components/shell/shared/MovableAriyaLauncher.tsx`
- added `src/components/shell/shared/ThemeModeMenu.tsx`
- `src/routes/_portal.index.tsx`
- `src/styles.css`

Accepted implementation facts:
- shared Light/Dark/System menu uses canonical `useTheme()`; no second theme store.
- Portal has scoped `.dark .rs-client-theme` foundation.
- Client and Admin topbar Àríyá triggers removed.
- both shells use one shared floating/movable Àríyá launcher and preserve their existing Àríyá panels.
- separate local UI-position keys are used for Admin and Portal.
- frozen focus-variable class contract is restored on the launcher.
- wide topbar searches were removed; Client icon search is accepted.
- Client Home embedded Àríyá remains removed.
- no auth/identity/server/Supabase/database/DEV-preview boundary changed.

Conditional closure items / owner refinements:
1. **Admin search placement changed again by owner:** remove search from AdminTopBar and restore the useful search *box* inside the expanded Admin Sidebar. It opens the existing `AdminCommandMenu`; collapsed Sidebar uses a discoverable icon-only form. Client keeps icon-only search in PortalTopBar.
2. Clean now-unused AdminTopBar `onAriyaClick` prop/callback wiring after floating-Àríyá migration.
3. Harden `MovableAriyaLauncher` persistence: current drag-end storage can capture stale React state. Persist the final/clamped pointer position reliably, clamp saved positions on initial mount as well as resize, and respect safe-area insets rather than only fixed pixel padding. Prefer unified Pointer Events if simplifying the implementation.
4. Client dark scope is directionally correct but incomplete: ensure `surface-raised`, muted/disabled/selected states, borders and any semantic tokens used by Core overlays/components cannot leak light client values into dark mode.
5. Client Home remains too pale/flat despite semantic tints. Add stronger depth using the client visual-depth rule below.

## Client Portal Home R2 -> R3 visual closure
**R2 INFORMATION ARCHITECTURE RETAINED / VISUAL DEPTH REOPENED**
Keep these R2 information regions:
1. briefing header.
2. segmented Needs Your Attention rail.
3. Work in Motion / current project.
4. Digital Estate.
5. Recent Movement.
6. shared Money + Support region.

R3 visual direction:
- reinterpret **Work in Motion** as the page's strong dark operational anchor rather than another pale box.
- do not copy the supplied HTML's exact dark-card anatomy, two-column hierarchy, buttons or right rail.
- keep the existing Briefing Board placement/composition while giving Work in Motion its own original systems-style internal layout.
- introduce a visible 68% progress treatment with a short one-shot animated reveal on load; no endless pulsing/loading animation.
- retain the systems-stage/node concept, but it may be redesigned inside the dark region for stronger legibility and rhythm.
- completed stages = restrained success green; current stage = terracotta; future stages = muted inverse-neutral.
- dark region may use subtle technical line/grid texture and warm charcoal depth.
- Attention segments should use perceptible but soft blue/amber/coral tints, not near-invisible white-on-paper differences.
- Money/Support may retain soft semantic tinted subdivisions.
- Recent Movement can remain relatively open/light so the dark anchor has contrast.
- Digital Estate remains row/system-oriented, not card soup.
- all treatments need deliberate client dark-mode equivalents.

## Shared shell-control direction
- ThemeModeMenu remains shared in both shells.
- Client search remains compact IconButton in PortalTopBar.
- Admin search belongs in the Sidebar, not AdminTopBar.
- Both shells retain movable floating Àríyá and existing panel ownership.
- No embedded/full-page Àríyá block in Home.

## DEV-PREVIEW-001
**ACCEPTED / FROZEN UNTIL DEMO IDENTITY TRANSITION**
Verified app commit: `1e673b2c042283c88e55e777f32d5c52c1890bfd`.
- only `import.meta.env.DEV` bypasses parent route UX guards.
- production authorization paths remain intact.
- development Portal uses presentation-only `Adaeze Realty Group` context.
- no server/RLS/CSRF/service-role boundary was weakened.
- must be removed/replaced when canonical demo/test identities are intentionally introduced.

## FOUND-001 remaining closure
Completed/frozen: A stack/repo, B tokens/UI stack, C Core C1-C5E, D/E shell architecture, F auth/identity/RLS/authorization/organisation context, DEV preview.

Still required before umbrella FOUND-001 closure:
1. current shell/search/launcher + Client Home R3 visual closure.
2. FOUND-001G PWA/accessibility/CI/testing/engineering hardening.
3. FOUND-001R integrated review + self-host check + final PASS/CONDITIONAL/FAIL record.

A rich Admin Home and client domain pages are not required to close the original FOUND-001 umbrella; they are post-foundation visual/domain slices.

## Sequencing
1. **SHELL-VIS-002** — Admin Sidebar search; clean topbar wiring; harden movable launcher; complete Client dark semantic scope; Client Home R3 dark Work-in-Motion anchor + one-shot animated progress and stronger surface depth.
2. inspect/freeze shell controls + Client Home visual closure.
3. **FOUND-001G** — PWA/offline/cache, CI/tests and engineering hardening.
4. **FOUND-001R** — integrated foundation review, self-host check, reconcile original demo-user acceptance criterion, final record.
5. after FOUND-001 closes: original Admin Home, Client Properties, Projects, Support, Billing, Auth onboarding/expansion, real Àríyá human takeover, then property-specific Chatwoot/Captain integrations in separately supervised slices.

## Next action
Run **SHELL-VIS-002 — Admin Sidebar Search + Client Home Depth Pass**. Preserve frozen security/auth/identity/DEV-preview behavior.