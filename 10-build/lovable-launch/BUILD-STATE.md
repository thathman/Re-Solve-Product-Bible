# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / ADMIN AUTH / PORTAL AUTH / TENANCY FROZEN — VIS-001B1 ADMIN SHELL FROZEN — CLIENT VISUAL AUTHORITY SPLIT FROZEN — CLIENT PORTAL AIRIX SHELL CONDITIONAL ON SMALL CLOSURE — PORTAL HOME NEXT AFTER CLOSURE**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client-facing visual references: `Airix360/AM-Client-Docs` Design system + `Airix360/airixmedia-web`
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval

## Frozen security / architecture
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only. Private server functions/routes independently authorize at their server boundary.
- Normal user reads use caller-scoped Supabase + RLS; generated `supabaseAdmin` remains quarantined/unused by application authorization.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider/Zod/access errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- `requireActiveStaff()` / `getAdminAccess()` are frozen for `/admin`.
- `requirePortalAccess()` / Portal parent access gate are frozen.
- `requireActiveOrganisation(organisationId)` freshly revalidates exact active organisation access.
- `rs_portal_org` is an untrusted UUID-only context pointer, never authorization evidence.
- zero active Portal organisations => forbidden; exactly one => automatic context; multiple + absent/malformed/stale pointer => explicit selection.
- no service-role application path, broad RBAC, domain data, seed/test users or public registration flow exists yet.

## Frozen functional surfaces
- Foundation + Core UI C1-C5E are frozen.
- `/ui` remains dev-only.
- Admin routes: Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Portal family: `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Auth routes: `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`.
- `/select-organisation` remains outside `/_portal` and uses canonical `getSafeRedirect()`.

## Admin visual authority
**VIS-001B1 ACCEPTED / CANONICAL / FROZEN VISUALLY**
- Admin stays on the established Lucid-style Re:Solve dialect.
- Inter UI typography; neutral/graphite palette; restrained Lucide; subtle borders; low shadow; denser operational composition.
- Existing Core Sidebar/AdminShell architecture remains canonical.
- sidebar/topbar/search/notifications/Àríyá/account/mobile behavior remain preserved.
- account placeholder is `Amara Okafor` / `Administrator`.
- complete frozen focus-visible contract is restored.
- Airix client styling must NOT leak into `/admin`.

## Client-facing visual authority
**ACCEPTED / CANONICAL PRODUCT DECISION**
Applies to Auth/client entry surfaces and Client Portal only.

Canonical sources:
1. `Airix360/AM-Client-Docs` Re:Solve Design System + supplied Client Portal Home.
2. `Airix360/airixmedia-web` as supporting systems/interaction reference.

Client grammar:
- warm paper canvas around `oklch(97% 0.012 60)`.
- warm surface around `oklch(94% 0.014 60)`.
- warm ink around `oklch(22% 0.02 55)`; muted around `oklch(45% 0.02 55)`.
- warm line around `oklch(88% 0.014 60)`.
- terracotta accent around `oklch(58% 0.14 35)`.
- warm charcoal featured surfaces around `oklch(17–22% 0.012–0.014 60)`.
- Space Grotesk = client UI/body.
- Instrument Serif italic = greetings/display/moments of address only.
- JetBrains Mono = currency, identifiers, dates/technical data selectively.
- tool-like 3–6px radii; borders over shadows; elevation only for floating layers.
- Lucide remains the icon family.
- implement as a scoped client theme, not a global token rewrite.
- bundled/self-hosted fonts only; no runtime Google Fonts/CDN dependency.
- no external stock-image dependency is canonical.

## Auth visual / capability plan
**FUNCTIONAL AUTH FROZEN; VISUAL REFRESH + CAPABILITY EXPANSION TRACKED, NOT YET IMPLEMENTED**
- Previous missing exact image asset is CLOSED/no-action; do not keep chasing it.
- Current remote Unsplash Auth image is temporary and must be removed during the Airix Auth redesign.
- No public registration.
- Intended first-account flow: staff/admin creates account -> invite email/link -> authenticated onboarding -> set password -> optional passkey -> optional TOTP -> optionally link Google/GitHub -> finish onboarding -> authorized destination.
- Google/GitHub sign-in must not create public accounts; identities are conveniences for existing invited users.
- ALTCHA is planned for abuse-prone Auth operations.
- planned sign-in methods: password, magic link, Google, GitHub, passkey; TOTP is MFA/AAL2.
- WhatsApp authentication is a separate future preflight; official WhatsApp OTP is preferred for authentication, while Baileys remains a messaging/connector concern rather than the root of identity trust.
- details tracked in `10-build/lovable-launch/AUTH-EXPANSION.md`.
- no Auth capability prompt yet unless explicitly requested.

## CLIENT-VIS portal shell rollout
**DIRECTION ACCEPTED / CONDITIONAL ON SMALL CLOSURE**

Verified current files:
- `src/components/shell/portal/PortalShell.tsx`
- `src/components/shell/portal/PortalTopBar.tsx`
- `src/components/shell/portal/PortalNavigation.tsx`
- `src/routes/_portal.tsx`
- `src/styles.css`
- `package.json` / `bun.lock`

Verified good:
- Portal uses one existing shell; no parallel shell was created.
- `.rs-client-theme` is scoped to `PortalShell`, so Admin structure remains separate.
- local Fontsource packages for Space Grotesk and Instrument Serif were added.
- topbar was restyled toward the supplied warm Airix/Re:Solve reference.
- active organisation comes only from the safe `/_portal` route context and is passed into the shell for UX.
- no new Supabase query or authorization shortcut was introduced.
- desktop navigation, mobile Sheet, command search, notifications, Àríyá and account behavior remain in the existing architecture.
- Lovable reported build/lint/typecheck success.

Blocking closure before the client Portal shell freezes:
1. `.rs-client-theme` currently overrides `--font-sans` but does not set `font-family`, so normal Portal text can continue inheriting Inter from `body`. Apply Space Grotesk directly on the scoped wrapper/theme.
2. `PortalTopBar` nests the organisation `<Link>` inside the Re:Solve brand `<Link>`. Split these into sibling links/elements; no nested anchors.
3. `bg-rs-surface-dark` is used for active navigation but no Tailwind semantic mapping `--color-rs-surface-dark` exists. Add the scoped/semantic mapping or use a valid mapped semantic token; the active warm-charcoal surface must render reliably.
4. Keep the client scope semantically complete enough that a global `.dark` class cannot leak mismatched Admin/global status/disabled/destructive colours into the warm client surface. Do not implement a broad client dark-mode redesign in this closure; just prevent partial mixed-theme inheritance where Portal Core components use these tokens.

## Client Portal Home reference
The supplied Client Portal Home is a layout specification for the next slice:
- horizontal client navigation with Re:Solve + organisation context.
- warm editorial canvas and large Instrument Serif greeting.
- prominent warm-charcoal active-project panel with progress/approval state.
- simple recent-activity rows with mono time/date labels.
- compact property incident, overdue invoice, support and Àríyá modules in the right column.
- client-oriented calm density; do not copy Admin dashboard density.
- static believable demo data only until domain persistence is separately designed.

## Sequencing
1. CLIENT-VIS-SHELL-FIX — close the four scoped-theme/topbar issues above only.
2. inspect and freeze Client Portal shell/theme primitives.
3. CLIENT-VIS-HOME — implement the supplied Client Portal Home reference using static demo data only.
4. inspect/freeze Portal Home.
5. propagate client grammar to Properties, Projects, Support and Billing in small slices.
6. later return to Auth visual redesign and Auth capability/onboarding work in separately supervised slices.
7. Admin Home VIS-001B2 can resume separately; Admin remains Lucid-style.

## Next action
Run one small **CLIENT-VIS-SHELL-FIX**. Do not begin Portal Home until the scoped client theme is actually applying Space Grotesk, active warm-charcoal navigation is backed by a real semantic utility/token, nested links are removed, and mixed global-dark token leakage is prevented. Preserve all security/auth/tenancy behavior and Admin visuals.