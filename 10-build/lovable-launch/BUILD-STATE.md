# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN SHELL CONTROLS ACCEPTED — CLIENT HOME R3 / PWA-STYLE SHELL IMPLEMENTED BUT CONDITIONAL — CRITICAL ÀRÍYÁ INITIALIZATION BUG + TABLET BREAKPOINT/STATUS CLOSURE REQUIRED BEFORE FOUND-001G**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client-facing visual authority: `Airix360/AM-Client-Docs` Design System + `Airix360/airixmedia-web`
- Owner-supplied mockups/HTML are reference material only unless a later decision explicitly promotes an interaction/anatomy to canonical.
- `checklist.design` is a UX completeness / pre-freeze QA reference only, never a visual authority.
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
- Lucid-style Re:Solve operational dialect remains canonical.
- Inter typography, neutral/graphite structure, restrained Lucide, subtle borders, low shadow, denser operational composition.
- Existing Sidebar/AdminShell architecture remains canonical.
- Account placeholder remains `Amara Okafor` / `Administrator`.
- Controlled semantic color accents are desired without rainbow-dashboard styling.
- Admin search belongs in expanded Sidebar; collapsed Sidebar uses search IconButton. Admin TopBar has no search and no Àríyá trigger.
- Admin uses shared Light/Dark/System control and shared movable floating Àríyá launcher.

### Client-facing
- Auth + Client Portal use the Airix/Re:Solve client dialect.
- Space Grotesk = client UI/body; Instrument Serif italic = greetings/display; JetBrains Mono = currency/dates/identifiers/technical metadata selectively.
- Warm paper/surface/ink remains the light-mode base, terracotta brand/action accent.
- Client Portal has a scoped warm-charcoal dark mode and must keep all client semantic/surface tokens coherent in that mode.
- tool-like 3–6px radii; borders over shadows; elevation only for floating layers.
- bundled/self-hosted fonts only.

## Shared controlled-color direction
**OWNER REQUEST / CANONICAL**
Semantic family:
- brand / primary: terracotta.
- information / review / support: blue/cyan.
- healthy / success: green.
- warning / degraded / expiring: amber.
- danger / overdue / failing: red/coral.

Rules:
- neutral/warm canvases dominate; color is structural punctuation.
- prefer tinted wells, status chips, dots, rails, progress segments, icon accents and selected indicators.
- status meaning must not depend on color alone.
- no gradients, neon, rainbow card grids or glassmorphism.
- preserve accessible contrast and frozen focus-visible behavior.

### Client visual-depth rule
- Client pages should not be uninterrupted paper/beige surfaces.
- One strong dark anchor region is valid/desirable when it clarifies hierarchy or current work.
- Supplied Client Home HTML contributes principles only: dark featured surface, layered contrast, visible progress, restrained motion. Do not copy its composition.
- short one-shot/reveal motion only; respect `prefers-reduced-motion`.
- In light mode Work in Motion sits directly on page canvas: no pale/tinted wrapper, halo, or decorative background around the dark box.
- no embedded Àríyá Home section; Àríyá remains a floating shell control.

## Checklist.design QA rule
- Use relevant Checklist Design component/flow checklists before freezing meaningful surfaces: states, focus, responsiveness, dark mode, search behavior, loading/error feedback, copy clarity, forms, support, payments, auth/recovery, etc.
- Do not copy Checklist Design layouts or styling.
- Product Bible + Re:Solve Core/visual dialect remain authoritative.

## Auth capability plan
**FUNCTIONAL AUTH FROZEN; EXPANSION TRACKED, NOT YET IMPLEMENTED**
- no public registration.
- intended first-account flow: staff/admin creates account -> invite link -> onboarding -> set password -> optional passkey -> optional TOTP -> optionally link Google/GitHub -> finish onboarding -> authorized destination.
- Google/GitHub must not create public accounts.
- ALTCHA planned for abuse-prone Auth operations.
- planned sign-in methods: password, magic link, Google, GitHub, passkey; TOTP is MFA/AAL2.
- WhatsApp authentication remains future preflight; official WhatsApp OTP preferred. Baileys is messaging/connector infrastructure.
- current remote Unsplash Auth image is temporary and must be removed during later Airix Auth redesign.
- details: `10-build/lovable-launch/AUTH-EXPANSION.md`.

## AI + support architecture
**OWNER-CORRECTED / CANONICAL**
Full authority: `10-build/lovable-launch/AI-SUPPORT-ARCHITECTURE.md`.
- Àríyá is Re:Solve's own AI and exists only inside Re:Solve.
- Àríyá is not Captain and is not powered by Captain.
- Re:Solve human escalation: `Re:Solve -> Àríyá -> dedicated owner/provider Re:Solve-support Chatwoot inbox -> human agent`.
- Captain MUST be disabled on that Re:Solve human-takeover inbox.
- Separately, an individual client website/property may embed its own Chatwoot inbox; Captain may be enabled on that specific property-support inbox/site when the provider owns that support responsibility.
- do not cross these two domains.

## Shared shell-control direction
- ThemeModeMenu remains shared in both shells.
- Client search remains compact IconButton in PortalTopBar/app bar.
- Admin search belongs in Sidebar.
- Both shells retain movable floating Àríyá and existing panel ownership.
- browser-local launcher position keys are allowed only for this non-sensitive UI preference.
- no embedded/full-page Àríyá Home block.

## Client Portal Home R3 retained structure
Keep unless explicit owner decision changes it:
1. briefing header.
2. Needs Your Attention.
3. Work in Motion/current project dark anchor.
4. Digital Estate.
5. Recent Movement.
6. Money + Support.

Rules:
- original Re:Solve composition, not a transcription of supplied HTML.
- dark Work-in-Motion is the primary contrast anchor with short one-shot progress reveal.
- semantic statuses should use visible soft surfaced treatment in both themes.
- Digital Estate remains monitoring/system oriented.
- Recent Movement stays timeline/editorial in spirit.
- Money + Support remains one conceptual operational area even when reflowed.

## Client mobile/PWA visual direction
**OWNER REQUEST / CANONICAL**
- Client Portal mobile/tablet is intentionally designed as an app/PWA surface, not compressed desktop.
- compact app bar, touch-friendly controls, safe-area handling, persistent primary route access and deliberate mobile information hierarchy are canonical.
- primary Portal navigation may use persistent bottom tabs on phone AND tablet; desktop horizontal navigation is a separate presentation.
- avoid redundant hamburger navigation when bottom tabs expose all five primary routes.
- installed-PWA infrastructure (manifest/icons/service worker/offline/update/cache policy) belongs to FOUND-001G; this governs visual/interaction anatomy only.

## CLIENT-PWA-VIS-001 review
**IMPLEMENTED / SECURITY-SAFE / NOT FROZEN — CLOSURE REQUIRED**
Verified app head: `843cec5cdfbc2499cc970d54fd23131c5fc4ebe7`.
Compared with prior verified app head `78b1be35afac07f68ee09b498d72d38bbdd9fc7c`, only client shell/Home/theme/shared-launcher files plus generated route tree changed:
- added `src/components/shell/portal/PortalBottomNav.tsx`
- `src/components/shell/portal/PortalShell.tsx`
- `src/components/shell/portal/PortalTopBar.tsx`
- `src/components/shell/shared/MovableAriyaLauncher.tsx`
- `src/routes/_portal.index.tsx`
- `src/styles.css`
- generated `src/routeTree.gen.ts`

Accepted implementation facts:
- dedicated on-dark tokens are mapped and scoped: `rs-text-on-dark`, `rs-text-on-dark-muted`, `rs-border-on-dark`.
- Work in Motion now uses on-dark vocabulary and no extra light-mode wrapper/shadow.
- Estate, Billing and Support use Core `StatusBadge` treatments.
- Portal hamburger/Sheet navigation was removed from visible mobile anatomy.
- PortalBottomNav exists with the five primary routes and safe-area-bottom padding.
- Home spacing/reflow improved and main composition is less desktop-compressed.
- no Auth/identity/server/Supabase/database/authorization/DEV-preview boundary changed.

Closure blockers found by canonical code review:
1. **CRITICAL — Àríyá launcher cannot initialize:** `MovableAriyaLauncher` starts `position = null` and returns `null` when unresolved, but its mount effect requires `buttonRef.current` to measure/resolve the position. The button never mounts, so the ref never exists and initialization can deadlock with the launcher permanently absent. Fix with a mounted-but-hidden measurement state or another initialization method that does not depend on an unmounted ref. Do not reintroduce visible position jumping.
2. **Tablet PWA breakpoint does not match owner direction:** `PortalBottomNav` is `md:hidden` and desktop PortalNavigation becomes visible at `md`, so 768px+ tablets are treated as desktop. Keep app-style bottom navigation/app bar through common tablet widths; use a desktop breakpoint around `xl` unless a better verified breakpoint is justified. 768x1024, 834x1194 and 1024x768 must remain app/tablet anatomy.
3. **PortalShell bottom clearance follows the same incorrect breakpoint:** `pb-16 md:pb-0` stops reserving bottom-nav space at 768px. Align it with the tablet bottom-nav breakpoint and include safe-area-bottom.
4. **Àríyá must avoid bottom navigation:** clamp/default position must reserve bottom-tab height + safe-area on client phone/tablet, not merely safe-area inset, so the draggable launcher cannot be parked under the nav.
5. **Status migration is incomplete:** Attention labels (`Approval required`, `Property degraded`, `Invoice overdue`) remain plain text while tiny dots/left rails use soft status-surface tokens directly. Use compact surfaced status treatment and use semantic foreground/strong marker values for tiny dots/rails where needed. `BUILD` should also get a small brand/current-stage surfaced treatment. Do not make the rail loud.
6. **PortalTopBar cleanup:** drawer imports/state/location/nav helpers remain after drawer removal. Remove dead `Menu`, `Sheet*`, `PORTAL_NAV_ITEMS`, `cn`, `useLocation`, `mobileMenuOpen` etc. with no behavior change.
7. **Single navigation source:** PortalBottomNav currently duplicates the five nav-item definitions instead of consuming canonical `PORTAL_NAV_ITEMS`. Extend canonical nav metadata with icons if needed so desktop/mobile cannot drift.
8. **Bottom-nav accessibility:** add `aria-current="page"` and frozen focus-visible treatment/touch-safe semantics to bottom-tab links; active state must not rely on color alone (subtle indicator/surface allowed).
9. **Desktop transition:** Home main two-column composition currently begins at `lg`; tablet app anatomy should remain deliberate through the accepted tablet breakpoint. Prefer moving the broad desktop composition to `xl` while preserving sensible tablet sub-layouts.
10. Remove residual dead Home helper/import code introduced by older prototypes when confirmed unused; do not alter information architecture.

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
1. tiny CLIENT-PWA-VIS-001 closure above.
2. FOUND-001G PWA/accessibility/CI/testing/engineering hardening.
3. FOUND-001R integrated review + self-host check + final PASS/CONDITIONAL/FAIL record.

A rich Admin Home and client domain pages are not required to close original FOUND-001; they remain post-foundation visual/domain slices.

## Sequencing
1. **CLIENT-PWA-VIS-001-FIX** — repair launcher initialization; align phone/tablet app breakpoints; reserve nav clearance; complete status treatment/nav accessibility; clean dead shell code.
2. inspect/freeze Client shell controls + Home visual-responsive closure.
3. **FOUND-001G1** — real PWA installability baseline: manifest/icons/theme/display/start-url and service-worker/cache architecture preflight/first bounded implementation.
4. later FOUND-001G slices — offline/update behavior, accessibility/device QA, automated tests/CI and engineering hardening.
5. **FOUND-001R** — integrated foundation review, self-host check, reconcile original demo-user acceptance criterion, final record.
6. after FOUND-001 closes: original Admin Home, Client Properties, Projects, Support, Billing, Auth onboarding/expansion, real Àríyá human takeover, then property-specific Chatwoot/Captain integrations.

## Next action
Run **CLIENT-PWA-VIS-001-FIX** only. Do not start PWA infrastructure until the critical launcher/tablet closure passes.