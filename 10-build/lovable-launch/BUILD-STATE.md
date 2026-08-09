# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / ADMIN AUTH / PORTAL AUTH / TENANCY FROZEN — VIS-001B1 ADMIN SHELL FROZEN — CLIENT VISUAL AUTHORITY SPLIT FROZEN — CLIENT PORTAL AIRIX SHELL ACCEPTED/FROZEN EXCEPT EXPLICIT HELP-LAUNCHER REFINEMENT — DEV-PREVIEW-001 ACCEPTED/FROZEN — CLIENT PORTAL HOME IMPLEMENTATION REVIEWED BUT REJECTED VISUALLY / REOPENED FOR ORIGINAL REDESIGN**

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
1. `Airix360/AM-Client-Docs` Re:Solve Design System.
2. `Airix360/airixmedia-web` as supporting systems/interaction reference.
3. Owner-supplied Client Portal pages are REFERENCE MATERIAL only unless a later slice explicitly promotes a specific interaction/anatomy to canonical.

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

### Reference-use rule
**OWNER CORRECTION / CANONICAL**
- Never blindly clone an attached client sample page.
- Samples provide visual vocabulary, content clues, and useful interaction ideas; they are not automatic layout specifications.
- Re:Solve client surfaces must be independently designed from the product's actual information hierarchy and workflows.
- Preserve the Airix visual DNA while producing a distinct Re:Solve product composition.
- Before freezing a client page, verify it is not merely a React transcription of an attached mockup.

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
**ACCEPTED / CANONICAL / FROZEN VISUALLY, WITH ONE OWNER-REQUESTED HELP-LAUNCHER REFINEMENT PENDING**
- one existing `PortalShell`; no parallel shell.
- `.rs-client-theme` is scoped to Portal and applies Space Grotesk directly via `font-family`.
- Fontsource Space Grotesk and Instrument Serif are bundled locally; JetBrains Mono remains existing technical/data font.
- `--color-rs-surface-dark` is mapped to the semantic `--rs-surface-dark` variable.
- client scope owns selected/disabled/destructive semantics required to avoid partial global-dark leakage.
- `PortalTopBar` brand and organisation controls are sibling links and both preserve the frozen focus-visible contract.
- active organisation comes only from the safe `/_portal` route context and remains UX context only.
- no new Supabase query or authorization shortcut was introduced.
- desktop navigation, mobile Sheet, command search, notifications and account behavior remain in the existing architecture.
- Admin visual files remain untouched by the client theme rollout.

### Client help / Àríyá interaction — OWNER OVERRIDE / CANONICAL DIRECTION
- Remove the dedicated Àríyá trigger from the Client Portal top navigation/topbar.
- Do not reserve a full Àríyá section or bottom command strip inside Portal Home.
- Client help should be persistently available through a floating launcher anchored to the lower-right of client Portal pages.
- The launcher belongs to the client Portal shell so it is available consistently across Home, Properties, Projects, Support and Billing.
- Preferred mental model is one help launcher with two clearly separated destinations/modes: **Ask Àríyá** and **Support**. Do not merge AI and human-support transcripts into one ambiguous conversation.
- Desktop may use a compact pill/launcher; mobile may collapse to a circular button while preserving accessible labels and touch targets.
- Àríyá should continue to use the existing shared `PortalAriyaPanel` rather than creating another AI implementation.
- Support may initially route/open a support surface and later connect to the canonical support-chat implementation (e.g. Chatwoot) when that integration is intentionally built.
- Floating launcher must respect safe-area insets, not cover critical content, and remain client-only. Do not add it to Admin or Auth unless separately requested.
- This explicit owner request is a permitted narrow reopening of the otherwise frozen Portal shell visuals.

## DEV-PREVIEW-001 — Temporary development visual preview mode
**ACCEPTED / CANONICAL FOR DEVELOPMENT / FROZEN UNTIL DEMO IDENTITY TRANSITION**
Verified app commit: `1e673b2c042283c88e55e777f32d5c52c1890bfd`.

Canonical behavior:
- only `import.meta.env.DEV` bypasses parent route UX guards.
- development `/admin` returns before `getAdminAccess()` so static Admin visual surfaces render without login.
- development Portal returns deterministic browser-only preview context: organisation id `00000000-0000-4000-8000-000000000001`, name `Adaeze Realty Group`.
- production branches remain present and continue calling the frozen `getAdminAccess()` and `getPortalOrganisationContext()` authorization flows.
- no localStorage/cookie/query-string/public production toggle exists.
- no identity/RLS/server function/CSRF/service-role boundary was changed.
- preview organisation context is presentation-only and is not authorization evidence.
- `/login` remains independently accessible.
- `/select-organisation` remains on its real authentication/context flow.
- no database changes, seed identities or test users were introduced.

This bypass must be removed or explicitly replaced when canonical demo/test identities become part of the supervised build. It must never become a production feature flag.

## CLIENT-VIS-HOME — Current implementation review
**FUNCTIONALLY SAFE / VISUALLY REJECTED / NOT FROZEN**
Current app head reviewed: `29074337bf93808ac020863d74ccd0258a8207bc`.
Current Home blob: `src/routes/_portal.index.tsx` SHA `36b9f1f52b6803f9a09bec6839a6f99a0a2fde52`.

Verified scope:
- compared with DEV-PREVIEW head `1e673b2c042283c88e55e777f32d5c52c1890bfd`, the visual slice changed only `src/routes/_portal.index.tsx` plus generated `src/routeTree.gen.ts`.
- static demo content only; no database/server/security change.
- frozen Portal shell/Admin/Auth/identity boundaries were preserved.

Reason for visual rejection:
- implementation follows the attached Client Portal Home sample too literally: greeting-first anatomy, approximately 1.3/1 two-column split, dark active-project block at upper left, recent activity below, and a stacked property/billing/support/Àríyá rail at right.
- this is effectively a React translation of the supplied mockup rather than an original Re:Solve Home designed from product hierarchy.
- owner explicitly requires a complete redesign rather than blind use of the attached sample.

### New Home design thesis — Client Briefing Board
The redesigned Home should feel like a concise morning/working brief from Re:Solve, not a generic dashboard and not the supplied sample.

Required information hierarchy:
1. **Briefing header** — restrained Instrument Serif greeting + date/context + one-sentence operational summary.
2. **Needs your attention** — one full-width segmented priority rail containing the few things that actually require the client's decision/action (approval, degraded property, overdue invoice). This is the first operational object after the greeting.
3. **Work in motion** — one large bordered workspace region, not a dark hero card. Show the active project as a horizontal stage/route system (Discovery -> Design -> Build -> QA -> Launch), current stage, 68% overall progress, next handoff, and approval count. Use thin Airix systems-line/node language rather than a diagonal texture.
4. **Your digital estate** — compact property health rows/table-like region with domains, state, and latest signal. Avoid individual property cards.
5. **Recent movement** — editorial event stream/timeline with mono dates and restrained status markers.
6. **Money + support** — one shared bordered region subdivided internally into billing and support, not separate floating cards.

Home must NOT include an Àríyá section/strip. Persistent Àríyá/support access belongs to the floating client help launcher owned by the Portal shell.

Composition guidance:
- use a primarily single broad content column with large subdivided regions; selective two-column subdivision only inside lower sections.
- avoid a permanent right sidebar of stacked cards.
- use strong horizontal rules, internal dividers, system lines/nodes and whitespace for hierarchy.
- terracotta appears selectively for attention/action/current-stage emphasis.
- warm charcoal may be used selectively for deliberate inset/floating help surfaces, not automatically as a project hero.
- use believable static demo content but do not invent domain persistence.
- mobile becomes a linear briefing sequence preserving the same information priority.

## Sequencing
1. CLIENT-HELP-001 — move client Àríyá access from the topbar to a persistent floating Àríyá/Support launcher while preserving the existing `PortalAriyaPanel`; no Home content redesign in this slice.
2. inspect/freeze the help-launcher refinement.
3. CLIENT-VIS-HOME-R2 — fully redesign only `src/routes/_portal.index.tsx` using the Client Briefing Board thesis above and no embedded Àríyá module.
4. inspect/freeze the original Portal Home composition.
5. propagate the accepted client grammar to Properties, Projects, Support and Billing in small slices; those pages must also be independently designed rather than cloned from attached samples.
6. later return to Auth visual redesign and Auth capability/onboarding work in separately supervised slices.
7. Admin Home VIS-001B2 can resume separately; Admin remains Lucid-style.
8. replace/remove DEV-PREVIEW-001 only when canonical demo/test identity support is intentionally introduced.

## Next action
When prompting resumes, run **CLIENT-HELP-001 — Floating Àríyá/Support Launcher** first. Remove the client topbar Àríyá trigger, add one persistent lower-right client help launcher using the existing `PortalAriyaPanel` for Àríyá and a clearly separated Support destination/mode, and preserve all shell/security contracts. Then run **CLIENT-VIS-HOME-R2** without any embedded Àríyá section.