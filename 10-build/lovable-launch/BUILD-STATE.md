# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — VIS-001B1 ADMIN SHELL FUNCTIONALLY/VISUALLY STABLE BUT OWNER HAS REOPENED COLOR ACCENTS — CLIENT AIRIX SHELL STABLE EXCEPT FLOATING ÀRÍYÁ LAUNCHER REFINEMENT — DEV-PREVIEW-001 FROZEN — PORTAL HOME R2 STRUCTURE ACCEPTED DIRECTIONALLY / NOT YET FROZEN DUE EMBEDDED ÀRÍYÁ STRIP + COLOR CALIBRATION**

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
- Owner has explicitly reopened ONLY the visual color treatment: Admin should gain restrained, purposeful color accents without losing operational clarity or becoming a colorful dashboard clone.

### Client-facing
- Auth + Client Portal use the Airix/Re:Solve client dialect.
- warm paper canvas `oklch(97% 0.012 60)`.
- warm surface `oklch(94% 0.014 60)`.
- warm ink `oklch(22% 0.02 55)`; muted `oklch(45% 0.02 55)`.
- warm line `oklch(88% 0.014 60)`.
- terracotta brand/action accent around `oklch(58% 0.14 35)`.
- warm charcoal featured/floating surfaces around `oklch(17–22% 0.012–0.014 60)`.
- Space Grotesk = client UI/body.
- Instrument Serif italic = greetings/display/moments of address only.
- JetBrains Mono = currency, dates, identifiers and technical metadata selectively.
- tool-like 3–6px radii; borders over shadows; elevation only for floating layers.
- bundled/self-hosted fonts only.

## Shared controlled-color direction
**OWNER REQUEST / CANONICAL**
Re:Solve should feel alive and recognizable, not monochrome/plain, while avoiding gimmicky rainbow SaaS styling.

Use a restrained shared semantic accent family across both dialects:
- **Brand / primary emphasis:** terracotta.
- **Information / review / support context:** blue/cyan family.
- **Healthy / success:** green.
- **Warning / degraded / expiring:** amber.
- **Danger / overdue / failing:** red/coral.

Rules:
- neutral/warm canvases remain dominant; color is punctuation, not wallpaper.
- prefer small tinted wells, status chips, dots, rails, progress segments, icon accents, active indicators and subtle 6–14% tint surfaces.
- use semantic meaning consistently; do not randomly assign colors to navigation items.
- generally use one primary accent plus the necessary semantic status color within a region.
- no gradients, neon, rainbow card grids, glassmorphism or decorative color for its own sake.
- preserve accessible contrast and frozen focus-visible behavior.
- do not globally rewrite Core components solely to make them colorful; apply color through scoped shell/page composition and semantic tokens.

Reference lesson from owner attachments:
- useful: restrained terracotta brand, blue info, green success, amber warning and red danger accents; colored progress/status markers; soft tint wells.
- non-canonical: exact layout, dark Admin composition, card arrangements, icon placements or component anatomy from the supplied files.

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
- Current remote Unsplash Auth image is temporary and must be removed during the later Airix Auth redesign.
- Details: `10-build/lovable-launch/AUTH-EXPANSION.md`.

## AI + support architecture
**OWNER-CORRECTED / CANONICAL**
Full authority: `10-build/lovable-launch/AI-SUPPORT-ARCHITECTURE.md`.

- Àríyá is Re:Solve's own AI and exists only inside Re:Solve.
- Àríyá is not Captain and is not powered by Captain.
- When a Re:Solve user requests/escalates to a human: `Re:Solve -> Àríyá -> dedicated owner/provider Re:Solve-support Chatwoot inbox -> human agent`.
- Captain MUST be disabled on that Re:Solve human-takeover inbox to avoid AI clash.
- Separately, an individual client website/property may embed its own Chatwoot inbox. If the service provider is responsible for that property's public support, Captain may be enabled on that specific property-support inbox/site.
- Do not cross the Re:Solve Àríyá/human-takeover domain with a client's public website/property Captain domain.

## Client Portal shell
**STABLE EXCEPT OWNER-REQUESTED FLOATING HELP REFINEMENT**
Current facts:
- one `PortalShell`.
- `.rs-client-theme` remains scoped and applies Space Grotesk.
- active organisation comes only from safe `/_portal` route context and remains UX context only.
- desktop nav, mobile Sheet, command search, notifications and account behavior remain.

Upcoming refinement:
- remove the dedicated Àríyá trigger from `PortalTopBar`.
- add one persistent lower-right client launcher owned by `PortalShell`.
- launcher opens the existing `PortalAriyaPanel`; do not create another AI client.
- desktop may use a compact pill; mobile may use a circular control.
- expose a future-ready `Talk to a person` / `Request human support` affordance inside the Àríyá experience, but do not fake live Chatwoot connectivity.
- human takeover will later route to the Captain-disabled owner/provider Re:Solve-support Chatwoot inbox.
- launcher must respect safe-area insets and not obscure critical content.
- no floating launcher in Admin or Auth unless separately requested.

## DEV-PREVIEW-001
**ACCEPTED / FROZEN UNTIL DEMO IDENTITY TRANSITION**
Verified app commit: `1e673b2c042283c88e55e777f32d5c52c1890bfd`.
- only `import.meta.env.DEV` bypasses parent route UX guards.
- production authorization paths remain intact.
- development Portal uses presentation-only `Adaeze Realty Group` context.
- no server/RLS/CSRF/service-role boundary was weakened.
- must be removed/replaced when canonical demo/test identities are intentionally introduced.

## CLIENT-VIS-HOME R2 review
**STRUCTURAL DIRECTION ACCEPTED / FUNCTIONALLY SAFE / NOT YET FROZEN**
Current app head reviewed: `7e63646412b2b7c18d2faa8f5735cdad0ff68e7b`.
Current Home blob: `80fb701570e92825a406f4b7dbd2e29602f200de`.

Verified scope:
- compared with prior Home R1 head `29074337bf93808ac020863d74ccd0258a8207bc`, R2 changed only `src/routes/_portal.index.tsx`.
- no database/server/security/shell/Admin/Auth change.

Accepted directional improvements:
- original Client Briefing Board composition rather than the supplied sample anatomy.
- full-width segmented `Needs your attention` rail.
- systems-style project stage route for `Work in motion`.
- row-based digital estate.
- editorial recent-movement timeline.
- one internally divided money/support region.

Remaining closure issues:
1. Home still includes an embedded full-width Àríyá command strip. Remove it; persistent Àríyá access now belongs only to the shell-owned floating launcher.
2. Color is still too terracotta-heavy/neutral. Calibrate the Home with the controlled semantic accent family: approval/info blue, degraded/warning amber, overdue/danger red, healthy green, current project stage/brand terracotta.
3. Preserve the structural R2 composition; do not redesign it again merely to add color.

## Sequencing
1. **VIS-COLOR-HELP-001** — one controlled visual calibration slice:
   - remove client topbar Àríyá trigger;
   - add floating client Àríyá launcher using existing panel;
   - remove Home embedded Àríyá strip;
   - apply restrained semantic color accents to current Client Home;
   - add a restrained color accent pass to the existing Admin shell without redesigning Admin structure.
2. inspect/freeze Client help launcher + Home R2 closure + Admin color calibration.
3. design **Admin Home** as its own original operational page using the accepted Lucid structure plus controlled semantic accents.
4. continue client Properties, Projects, Support and Billing as original design slices.
5. later implement actual Àríyá -> Captain-disabled Chatwoot human-takeover bridge.
6. separately implement property/site Chatwoot + Captain support where provider support is enabled.
7. later return to Auth visual/onboarding work.

## Next action
Run **VIS-COLOR-HELP-001 — Controlled Color + Floating Àríyá**. This is a visual calibration/refinement slice only. Preserve all frozen security, development-preview and shell behavior not explicitly reopened above.