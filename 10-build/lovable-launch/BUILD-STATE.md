# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — VIS-COLOR-HELP-001 FUNCTIONALLY SAFE / VISUALLY CONDITIONAL — OWNER HAS REOPENED BOTH SHELLS FOR MODE CONTROL, ICON SEARCH, MOVABLE FLOATING ÀRÍYÁ, AND STRONGER CLIENT SURFACE RHYTHM**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client-facing visual authority: `Airix360/AM-Client-Docs` Design System + `Airix360/airixmedia-web`
- Owner-supplied mockups are reference material only unless an interaction/anatomy is explicitly promoted to canonical.
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
- Controlled semantic color accents are allowed and desired without turning Admin into a rainbow dashboard.

### Client-facing
- Auth + Client Portal use the Airix/Re:Solve client dialect.
- Space Grotesk = client UI/body; Instrument Serif italic = greetings/display; JetBrains Mono = currency/dates/identifiers/technical metadata selectively.
- Warm paper/surface/ink remains the light-mode base, with terracotta as brand/action accent.
- Client Portal now requires a deliberate scoped dark theme rather than remaining warm-light only.
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
- distinct regions may use subtle semantic or tonal background surfaces where they improve page rhythm and hierarchy.
- do not assign random colors to navigation items.
- no gradients, neon, rainbow card grids, glassmorphism or decorative color for its own sake.
- preserve accessible contrast and frozen focus-visible behavior.

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

## Shared shell-controls direction
**OWNER DIRECTION / CANONICAL**
Applies to Admin and Client Portal shells.

### Theme / appearance
- Both shells must expose an accessible Light / Dark / System mode control using the existing canonical `ThemeProvider` / `useTheme` state.
- Do not create a second theme persistence mechanism.
- Admin already inherits the global light/dark semantic tokens.
- Client Portal must add a coherent scoped `.dark .rs-client-theme` token set so dark mode is genuinely designed in the Airix/Re:Solve client dialect; do not let the light client override mask global dark mode.
- Theme controls must remain compact and available on desktop and mobile.

### Search
- Replace wide topbar search fields in both Admin and Client Portal with compact search IconButtons.
- The icon continues to open the existing shell-owned Command/Search experience.
- Cmd/Ctrl+K behavior remains.
- Do not remove or rebuild Command menus.

### Àríyá launchers
- Neither Admin nor Client Portal should keep a dedicated Àríyá topbar trigger.
- Both shells use a floating Àríyá launcher that opens their EXISTING shell-owned Àríyá panel.
- Floating launchers may be dragged freely within the visible viewport, constrained so they cannot be lost off-screen or under unsafe areas.
- Drag must not accidentally open the panel; click/tap still opens it.
- Preserve keyboard accessibility and the canonical focus-visible variable contract.
- A browser-local position preference is acceptable because launcher position is non-sensitive UI preference only; do not store auth/domain/security context with it.
- Use separate position keys per shell so Admin and Client placement do not overwrite each other.
- Reset to a sensible lower-right default if a stored position is invalid after viewport resize/device change.
- Floating movement should not become a springy/gimmicky animation. Reduced-motion rules remain respected.

## VIS-COLOR-HELP-001 review
**FUNCTIONALLY SAFE / VISUALLY CONDITIONAL — SUPERSEDED BY OWNER SHELL-CONTROL REFINEMENT**
Verified app head: `14624370102d615792f1ac309b3a84a0cb0d124f`.
Compared with prior Home R2 head `7e63646412b2b7c18d2faa8f5735cdad0ff68e7b`, only these files changed:
- `src/styles.css`
- `src/components/shell/portal/PortalShell.tsx`
- `src/components/shell/portal/PortalTopBar.tsx`
- `src/components/shell/portal/PortalAriyaPanel.tsx`
- `src/components/shell/portal/PortalHelpLauncher.tsx` (new)
- `src/routes/_portal.index.tsx`
- `src/components/shell/admin/AdminSidebar.tsx`
- `src/components/shell/admin/AdminTopBar.tsx`

Accepted implementation facts:
- Client topbar Àríyá trigger removed.
- Existing `PortalAriyaPanel` retained and receives future-ready human-support placeholder only; no Chatwoot integration was faked.
- Persistent Client floating launcher added and opens the existing panel.
- Home embedded Àríyá command strip removed.
- Client Home semantic markers now distinguish info/warning/danger/success.
- Admin received restrained terracotta/danger accents without layout redesign.
- No auth/identity/server/Supabase/database/DEV-preview boundary changed.

Open visual/interaction issues:
1. Client Portal still has no functional dark appearance because `.rs-client-theme` currently defines a warm-light token set after the global `.dark` tokens. Add a deliberate `.dark .rs-client-theme` palette.
2. Neither Admin nor Client shell exposes a Light/Dark/System mode control.
3. Both topbars still use more search chrome than the owner wants; reduce to search icon only while preserving Command behavior.
4. Admin still has a topbar Àríyá trigger; move Admin Àríyá to floating launcher too.
5. Floating Àríyá launcher must be draggable/movable on both shells.
6. Current Client launcher hard-codes `ring-2` / `ring-offset-2` instead of the frozen focus variable contract; correct this before freeze.
7. Client Home still feels too same-tone. Preserve the Briefing Board structure but introduce a small reusable vocabulary of distinct section backgrounds/bands/tinted wells so regions have stronger visual rhythm without card soup or gimmicky color.

## Client Portal Home R2
**STRUCTURAL DIRECTION ACCEPTED / FUNCTIONALLY SAFE / VISUAL CLOSURE OPEN**
Accepted structure:
1. briefing header.
2. segmented Needs Your Attention rail.
3. Work in Motion workflow/system map.
4. row-based Digital Estate.
5. Recent Movement editorial timeline.
6. shared Money + Support region.

Do not redesign this structure again merely to add visual rhythm. Improve surface hierarchy/background treatments within the accepted composition.

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
1. shell-controls + visual closure described above.
2. FOUND-001G PWA/accessibility/CI/testing/engineering hardening.
3. FOUND-001R integrated review + self-host check + final PASS/CONDITIONAL/FAIL record.

A rich Admin Home and client domain pages are not required to close the original FOUND-001 umbrella; they are post-foundation visual/domain slices.

## Sequencing
1. **SHELL-CTRL-001** — Light/Dark/System controls + search icon only + movable floating Àríyá on Admin and Client + client scoped dark theme + Client Home surface-rhythm refinement.
2. inspect/freeze both shell control systems and Client Home visual closure.
3. **FOUND-001G** — PWA/offline/cache, CI/tests and engineering hardening.
4. **FOUND-001R** — integrated foundation review, self-host check, reconcile original demo-user acceptance criterion, final record.
5. after FOUND-001 closes: original Admin Home, Client Properties, Projects, Support, Billing, Auth onboarding/expansion, real Àríyá human takeover, then property-specific Chatwoot/Captain integrations in separately supervised slices.

## Next action
Run **SHELL-CTRL-001 — Shared Shell Controls + Client Surface Rhythm**. Preserve frozen security/auth/identity/DEV-preview behavior.