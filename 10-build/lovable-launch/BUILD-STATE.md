# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / ADMIN AUTH / PORTAL AUTH / TENANCY FROZEN — VIS-001B1 ADMIN SHELL FROZEN — CLIENT VISUAL AUTHORITY SPLIT FROZEN — CLIENT PORTAL AIRIX SHELL ACCEPTED/FROZEN — DEV-PREVIEW-001 ACCEPTED/FROZEN — CLIENT PORTAL HOME NEXT**

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
- `requireActiveStaff()` / `getAdminAccess()` are frozen for production `/admin` authorization.
- `requirePortalAccess()` / Portal parent access gate are frozen for production Portal authorization.
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
**ACCEPTED / CANONICAL / FROZEN VISUALLY**
Verified current implementation:
- one existing `PortalShell`; no parallel shell.
- `.rs-client-theme` is scoped to Portal and applies Space Grotesk directly via `font-family`.
- Fontsource Space Grotesk and Instrument Serif are bundled locally; JetBrains Mono remains existing technical/data font.
- `--color-rs-surface-dark` is mapped to the semantic `--rs-surface-dark` variable, so active warm-charcoal nav utilities are real Tailwind theme utilities.
- client scope explicitly owns selected/disabled/destructive semantics required to avoid partial global-dark leakage.
- `PortalTopBar` brand and organisation controls are sibling links, not nested anchors, and both preserve the frozen focus-visible contract.
- active organisation comes only from the safe `/_portal` route context and remains UX context only.
- no new Supabase query or authorization shortcut was introduced.
- desktop navigation, mobile Sheet, command search, notifications, Àríyá and account behavior remain in the existing architecture.
- Admin visual files remain untouched by the client theme rollout.
- Lovable reported build/lint success; source review found no remaining shell blocker.

Do not reopen the client shell absent a concrete regression or explicit owner visual request.

## DEV-PREVIEW-001 — Temporary development visual preview mode
**ACCEPTED / CANONICAL FOR DEVELOPMENT / FROZEN UNTIL DEMO IDENTITY TRANSITION**
Verified app commit: `1e673b2c042283c88e55e777f32d5c52c1890bfd`.

Verified current files:
- `src/routes/admin.tsx` blob `56947b1d8e0c09092d97b44d2e02f1b26e0e8edd`.
- `src/routes/_portal.tsx` blob `ee239d8bb1068bb9800469871577dc8aca1fd8ff`.

Canonical behavior:
- only `import.meta.env.DEV` bypasses the parent route UX guards.
- development `/admin` returns before `getAdminAccess()` so static Admin visual surfaces render without a login.
- development Portal returns deterministic browser-only preview context: organisation id `00000000-0000-4000-8000-000000000001`, name `Adaeze Realty Group`.
- production branches remain byte-structurally present and continue calling the frozen `getAdminAccess()` and `getPortalOrganisationContext()` authorization flows.
- no localStorage/cookie/query-string/public production toggle exists.
- no identity/RLS/server function/CSRF/service-role boundary was changed.
- preview organisation context is presentation-only and is not authorization evidence.
- `/login` remains independently accessible.
- `/select-organisation` remains on its real authentication/context flow.
- no database changes, seed identities or test users were introduced.
- Lovable reported build/lint/typecheck success.

Development-visible visual routes include Portal `/`, `/properties`, `/projects`, `/support`, `/billing` and the full existing `/admin` route family.

This bypass must be removed or explicitly replaced when canonical demo/test identities become part of the supervised build. It must never become a production feature flag.

## Client Portal Home reference
The supplied Client Portal Home is a layout specification for the next visual slice:
- horizontal client navigation with Re:Solve + organisation context.
- warm editorial canvas and large Instrument Serif greeting.
- prominent warm-charcoal active-project panel with progress/approval state.
- simple recent-activity rows with mono time/date labels.
- compact property incident, overdue invoice, support and Àríyá modules in the right column.
- client-oriented calm density; do not copy Admin dashboard density.
- static believable demo data only until domain persistence is separately designed.

## Sequencing
1. CLIENT-VIS-HOME — implement supplied Client Portal Home reference using static demo data only.
2. inspect/freeze Portal Home.
3. propagate client grammar to Properties, Projects, Support and Billing in small slices.
4. later return to Auth visual redesign and Auth capability/onboarding work in separately supervised slices.
5. Admin Home VIS-001B2 can resume separately; Admin remains Lucid-style.
6. replace/remove DEV-PREVIEW-001 only when canonical demo/test identity support is intentionally introduced.

## Next action
Run **CLIENT-VIS-HOME — Client Portal Home Reference Implementation**. Modify only the Portal Home visual content using static believable demo data and the supplied Client Portal Home as the layout specification. Preserve the frozen Airix client shell, frozen development preview boundary, all production authorization/server security, and the separate Lucid Admin visual dialect.