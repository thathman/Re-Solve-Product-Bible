# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN SIDEBAR SEARCH CLEANUP ACCEPTED — CLIENT HOME R3 STRUCTURE/DARK ANCHOR IMPLEMENTED BUT VISUAL/RESPONSIVE CLOSURE OPEN — NEXT: CLIENT PWA-STYLE RESPONSIVE SHELL + STATUS/CONTRAST + ÀRÍYÁ INITIALIZATION FIX**

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
- In light mode the dark Work-in-Motion anchor should sit directly on the page: no extra pale/tinted wrapper, halo, or decorative background around the box. The dark region itself supplies the contrast.
- Do not reintroduce an embedded Àríyá Home section; Àríyá remains a floating shell control.

## Reference-use rule
**OWNER CORRECTION / CANONICAL**
- Never blindly clone an attached sample page.
- Samples provide visual vocabulary, content clues and useful interaction ideas; they are not automatic layout specifications.
- Re:Solve surfaces must be independently designed from product hierarchy and workflows.
- Before freezing a page, verify it is not merely a React transcription of a mockup.

## Checklist.design QA rule
**OWNER-REQUESTED / CANONICAL QA REFERENCE**
- `checklist.design` is a UX completeness / pre-freeze QA reference, not a Re:Solve visual authority.
- Use the relevant component/flow checklist before freezing meaningful surfaces: states, focus, responsiveness, dark mode, search behavior, loading/error feedback, copy clarity, forms, support, payments, auth/recovery, and other applicable flow checks.
- Do not copy Checklist Design layouts or styling.
- Product Bible + Re:Solve Core/visual dialect remain authoritative when a checklist recommendation conflicts with a product/security decision.

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
**IMPLEMENTED / FUNCTIONALLY SAFE / SUPERSEDED BY LATER VISUAL CLOSURE PASSES**
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
- Client search is compact icon-only.
- Client Home embedded Àríyá remains removed.
- no auth/identity/server/Supabase/database/DEV-preview boundary changed.

## SHELL-VIS-002 + closure-fix review
**ADMIN CLEANUP ACCEPTED / CLIENT VISUAL + RESPONSIVE CLOSURE OPEN**
Latest verified app head: `78b1be35afac07f68ee09b498d72d38bbdd9fc7c`.
The closure-fix after `5bd8f62a3593271257ec40b84da9975e60086ea0` changed only:
- `src/components/shell/admin/AdminSidebar.tsx`
- `src/components/shell/admin/AdminTopBar.tsx`
- `src/components/shell/shared/MovableAriyaLauncher.tsx`
- generated `src/routeTree.gen.ts`

Accepted:
- Admin search is now in the expanded Sidebar and opens the existing Command menu; collapsed Sidebar keeps the icon form.
- AdminTopBar no longer carries the empty props interface/suppression.
- shared launcher uses Pointer Events and retains frozen focus classes, separate non-sensitive position keys, and safe-area/resize clamping intent.
- Client Home R3 keeps the Briefing Board information architecture and has the requested dark Work-in-Motion anchor with visible progress/stage treatment.
- no auth/identity/server/Supabase/database/DEV-preview boundary changed.

Open blockers found from code + owner screenshots:
1. **Àríyá initial-position flash/jump:** `MovableAriyaLauncher` still renders visibly at `{x:0,y:0}` and only computes the default lower-right coordinate in an effect. On load it can visibly appear top-left and then jump across the viewport. Position must be resolved before the launcher becomes visible; do not animate `left/top` during initialization.
2. **Àríyá final-position persistence remains fragile:** pointer-up still writes React `position` state directly. Use an explicit latest-position ref/final-clamped coordinate so storage cannot lag the final pointer frame.
3. **On-dark semantic clash:** Work-in-Motion and the launcher use ordinary `text-primary`/`text-inverse` semantics against `surface-dark`. Client dark mode deliberately makes `text-inverse` dark, so launcher text can disappear; in client light mode `text-primary` is dark, so Work-in-Motion content can become dark-on-dark. Add a dedicated always-light on-dark text/border vocabulary and use it for dark anchors/launchers/active dark navigation surfaces.
4. **Statuses need surfaced treatment:** owner wants operational states such as `HEALTHY`, `DEGRADED`, `OVERDUE`, `BUILD`, approval/support state, etc. presented with soft semantic background chips/wells similar to the existing `Awaiting reply from Re:Solve` treatment. Prefer the existing Core `StatusBadge` where appropriate; do not rely on color-only text.
5. **Client mobile/tablet is still compressed desktop:** current mobile PortalTopBar relies on hamburger + Sheet and the Home layout simply stacks desktop regions. Redesign client-only mobile/tablet composition to feel like a PWA/app while preserving desktop anatomy. Actual manifest/offline installability remains FOUND-001G.
6. **Work-in-Motion light-mode framing:** keep the dark anchor itself, but remove any additional light/tinted wrapper/halo/shadow-like background around it in light mode. The surrounding grid cell/page stays transparent/canvas.
7. **Responsive/color QA:** screenshots show cramped tiny metadata, weak dark-mode contrast, and status/action text that can disappear. Validate 390px phone, common tablet widths, desktop, Light/Dark/System, safe areas, and no accidental horizontal overflow.

## Client Portal Home R3 retained structure
Keep these information regions unless an explicit later owner decision changes them:
1. briefing header.
2. Needs Your Attention.
3. Work in Motion/current project dark anchor.
4. Digital Estate.
5. Recent Movement.
6. Money + Support.

Visual rules:
- original Re:Solve composition, not a copy of the supplied HTML.
- dark Work-in-Motion is the main contrast anchor; short one-shot progress animation, no looping decoration.
- semantic status chips/backgrounds should be visible and readable in both themes.
- Digital Estate remains row/system-oriented on desktop, but may be recomposed into touch-friendly app rows on mobile/tablet.
- Recent Movement stays timeline/editorial in spirit but may be reflowed for app ergonomics.
- Money + Support remains conceptually one operational area but may reflow on small screens.
- no embedded Àríyá Home section.

## Shared shell-control direction
- ThemeModeMenu remains shared in both shells.
- Client search remains compact IconButton in PortalTopBar/app bar.
- Admin search belongs in the Sidebar, not AdminTopBar.
- Both shells retain movable floating Àríyá and existing panel ownership.
- No embedded/full-page Àríyá block in Home.

## Client mobile/PWA visual direction
**OWNER REQUEST / CANONICAL**
- Client Portal mobile/tablet should be intentionally designed as an app/PWA surface, not merely stacked desktop content.
- Compact app bar, touch-friendly controls, clear safe-area handling, persistent route access, and deliberate mobile information hierarchy are desired.
- A mobile bottom-tab navigation pattern is allowed/preferred for the five primary Portal destinations if it improves app ergonomics; desktop horizontal navigation remains a separate presentation.
- Avoid redundant hamburger navigation when primary destinations are already persistently reachable in an app-style bottom bar.
- Installed-PWA infrastructure (manifest, icons, service worker/offline/update lifecycle/cache policy) is still implemented and reviewed under FOUND-001G; this section governs visual/interaction anatomy only.

## DEV-PREVIEW-001
**ACCEPTED / FROZEN UNTIL DEMO IDENTITY TRANSITION**
Verified app commit: `1e673b2c042283c88e55e777f32d5c52c1890bfd`.
- only `import.meta.env.DEV` bypasses parent route UX guards.
- production authorization paths remain intact.
- development Portal uses presentation-only `Adaeze Realty Group` context.
- no server/RLS/CSRF/service-role boundary was weakened.
- must be removed/replaced when canonical demo/test identities are intentionally introduced.

## FOUND-001 remaining closure
Completed/frozen: A stack/repo, B tokens/UI stack, C Core C1-C5E, D/E functional shell architecture, F auth/identity/RLS/authorization/organisation context, DEV preview.

Still required before umbrella FOUND-001 closure:
1. client shell/Home visual-responsive closure described above.
2. FOUND-001G PWA/accessibility/CI/testing/engineering hardening.
3. FOUND-001R integrated review + self-host check + final PASS/CONDITIONAL/FAIL record.

A rich Admin Home and client domain pages are not required to close the original FOUND-001 umbrella; they are post-foundation visual/domain slices.

## Sequencing
1. **CLIENT-PWA-VIS-001** — fix status surfaces/on-dark contrast; eliminate Àríyá initialization/persistence jump; PWA-style Client mobile/tablet shell and Home reflow; remove extra Work-in-Motion light-mode framing.
2. inspect/freeze Client shell controls + Home responsive/visual closure.
3. **FOUND-001G** — real PWA manifest/offline/cache, CI/tests and engineering hardening, using Checklist.design as a QA reference where applicable.
4. **FOUND-001R** — integrated foundation review, self-host check, reconcile original demo-user acceptance criterion, final record.
5. after FOUND-001 closes: original Admin Home, Client Properties, Projects, Support, Billing, Auth onboarding/expansion, real Àríyá human takeover, then property-specific Chatwoot/Captain integrations in separately supervised slices.

## Next action
Run **CLIENT-PWA-VIS-001 — Client Mobile/PWA Visual Closure**. Preserve frozen security/auth/identity/DEV-preview behavior.