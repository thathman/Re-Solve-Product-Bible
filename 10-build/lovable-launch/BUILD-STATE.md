# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / ADMIN AUTH / PORTAL AUTH / TENANCY FROZEN — VIS-001B1 ADMIN SHELL FROZEN — CLIENT AIRIX SHELL ACCEPTED/FROZEN EXCEPT HELP-LAUNCHER REFINEMENT — DEV-PREVIEW-001 ACCEPTED/FROZEN — PORTAL HOME R1 VISUALLY REJECTED / R2 REDESIGN PENDING**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client-facing visual references: `Airix360/AM-Client-Docs` Design System + `Airix360/airixmedia-web`
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval.

## Frozen security / architecture
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only. Private server functions/routes independently authorize at their server boundary.
- Normal user reads use caller-scoped Supabase + RLS; generated `supabaseAdmin` remains quarantined/unused by application authorization.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider/Zod/access errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- `requireActiveStaff()` / `getAdminAccess()` are frozen for production Admin authorization.
- `requirePortalAccess()` / Portal parent access gate are frozen for production Portal authorization.
- `requireActiveOrganisation(organisationId)` freshly revalidates exact active organisation access.
- `rs_portal_org` is an untrusted UUID-only context pointer, never authorization evidence.
- No service-role application path, broad RBAC, domain data, seed/test users or public registration flow exists yet.

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
- Airix client styling must not leak into `/admin`.
- Account placeholder remains `Amara Okafor` / `Administrator`.

## Client-facing visual authority
**ACCEPTED / CANONICAL PRODUCT DECISION**
Applies to Auth/client entry surfaces and Client Portal only.

Canonical sources:
1. `Airix360/AM-Client-Docs` Re:Solve Design System.
2. `Airix360/airixmedia-web` as supporting systems/interaction reference.
3. Owner-supplied client mockups are reference material only unless a later slice explicitly promotes an interaction/anatomy to canonical.

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
- bundled/self-hosted fonts only; no runtime font CDN.

### Reference-use rule
**OWNER CORRECTION / CANONICAL**
- Never blindly clone an attached client sample page.
- Samples provide visual vocabulary, content clues and useful interaction ideas; they are not automatic layout specifications.
- Re:Solve client surfaces must be independently designed from product hierarchy and workflows while preserving Airix visual DNA.

## Auth visual / capability plan
**FUNCTIONAL AUTH FROZEN; VISUAL REFRESH + CAPABILITY EXPANSION TRACKED, NOT YET IMPLEMENTED**
- No public registration.
- Intended first-account flow: staff/admin creates account -> invite link -> onboarding -> set password -> optional passkey -> optional TOTP -> optionally link Google/GitHub -> finish onboarding -> authorized destination.
- Google/GitHub must not create public accounts.
- ALTCHA planned for abuse-prone Auth operations.
- Planned sign-in methods: password, magic link, Google, GitHub, passkey; TOTP is MFA/AAL2.
- WhatsApp authentication remains a future preflight; official WhatsApp OTP is preferred for authentication. Baileys is a messaging/connector concern.
- Current remote Unsplash Auth image is temporary and must be removed during Airix Auth redesign.
- Details: `10-build/lovable-launch/AUTH-EXPANSION.md`.

## Client Portal shell
**ACCEPTED / CANONICAL / FROZEN VISUALLY, EXCEPT OWNER-REQUESTED HELP-LAUNCHER REFINEMENT**
- One existing `PortalShell`; no parallel shell.
- `.rs-client-theme` applies Space Grotesk directly and remains scoped to Portal.
- Fontsource Space Grotesk + Instrument Serif are bundled locally; JetBrains Mono remains available.
- Active organisation comes only from safe `/_portal` route context and remains UX context only.
- Desktop navigation, mobile Sheet, command search, notifications and account behavior remain in existing architecture.
- Remove the dedicated client Àríyá topbar trigger in the upcoming help-launcher refinement.

## AI + support architecture
**OWNER-CORRECTED / CANONICAL**
Full authority: `10-build/lovable-launch/AI-SUPPORT-ARCHITECTURE.md`.

### Àríyá
- Àríyá is Re:Solve's own AI and exists only inside Re:Solve.
- Àríyá powers Re:Solve assistance/reasoning/context/tool use and future authorized Re:Solve workflows.
- Àríyá never becomes the AI embedded on a client's public website/property.
- Àríyá is not Captain and is not powered by Captain.

### Client property / website support
Example ownership model:
- Re:Solve owner/provider: Airix Media.
- Client: Adaeze Realty Group.
- Adaeze may have a website/property for which Airix Media is responsible for support.

For such a client website/property:
- Chatwoot may be embedded on that website as its customer-support channel.
- Captain may be enabled on that specific property-support inbox/site.
- In that context Captain is the AI serving visitors/users of the Adaeze website/property.
- Captain belongs to that site's support experience only; it has nothing to do with powering Re:Solve or Àríyá.

### Re:Solve human takeover
When a Re:Solve user asks Àríyá for a human, or Àríyá escalates later according to policy:

`Re:Solve user -> Àríyá inside Re:Solve -> escalation -> dedicated owner/provider Chatwoot Re:Solve-support inbox -> human agent`

Canonical rules:
- Àríyá never leaves Re:Solve as another website-support AI.
- The Chatwoot destination for Re:Solve human takeover is a dedicated owner/provider support inbox/property (for example Airix Media Re:Solve Support).
- **Captain must be disabled on that Re:Solve human-takeover inbox.**
- Human support is the destination; this prevents Àríyá escalating into another AI and avoids AI clash.
- Chatwoot provides conversation persistence, queue/assignment, human participation and history for the takeover path.

This is separate from:

`Visitor on client website/property -> that property's Chatwoot inbox -> Captain if enabled -> human agent if needed`

Do not silently cross these two domains.

## Floating client help launcher
**OWNER DIRECTION / NEXT SHELL REFINEMENT**
- Remove Àríyá from the client topbar.
- Do not embed a full Àríyá section/command strip in Portal Home.
- Add one persistent lower-right client launcher owned by the Portal shell.
- Launcher opens Àríyá inside Re:Solve using the existing `PortalAriyaPanel` as the current UI implementation to evolve.
- Include a visible future-ready `Request human support` / `Talk to a person` affordance.
- Human takeover eventually routes to the dedicated owner/provider Re:Solve Chatwoot inbox with Captain disabled.
- Before Chatwoot integration exists, takeover UI may be visual/demo-only and must not fake a connected human.
- Launcher is client-only, respects safe-area insets and must not cover critical content.

## DEV-PREVIEW-001
**ACCEPTED / CANONICAL FOR DEVELOPMENT / FROZEN UNTIL DEMO IDENTITY TRANSITION**
Verified app commit: `1e673b2c042283c88e55e777f32d5c52c1890bfd`.

- Only `import.meta.env.DEV` bypasses parent route UX guards.
- Development Admin renders without `getAdminAccess()`.
- Development Portal returns presentation-only preview organisation `Adaeze Realty Group`.
- Production branches continue calling the frozen real authorization flows.
- No localStorage/cookie/query-string/public-production bypass exists.
- No identity/RLS/server/CSRF/service-role boundary was changed.
- Must be removed/replaced when canonical demo/test identities are intentionally introduced.

## CLIENT-VIS-HOME R1 review
**FUNCTIONALLY SAFE / VISUALLY REJECTED / NOT FROZEN**
Current Home reviewed at app head `29074337bf93808ac020863d74ccd0258a8207bc`, blob `36b9f1f52b6803f9a09bec6839a6f99a0a2fde52`.

Reason for rejection:
- R1 follows the supplied client sample too literally: greeting-first anatomy, ~1.3/1 two-column split, dark project block, activity below and stacked right rail.
- Owner requires an original Re:Solve composition rather than a React transcription of a sample.

### Home R2 thesis — Client Briefing Board
Required hierarchy:
1. Briefing header — restrained Instrument Serif greeting + date/context + concise operational summary.
2. Needs your attention — one full-width segmented priority rail for approval, degraded property and overdue invoice.
3. Work in motion — one large bordered workspace using systems-style project stages/nodes, not a dark hero.
4. Your digital estate — compact property health rows/table-like region.
5. Recent movement — editorial event stream/timeline with mono dates.
6. Money + support — one shared internally divided region.

Home must not contain an embedded Àríyá section. Persistent Àríyá/human-escalation access belongs to the floating shell launcher.

## Sequencing
1. **CLIENT-HELP-001** — remove client topbar Àríyá and add persistent floating Àríyá launcher using existing panel; visual/future-ready human takeover only, no fake Chatwoot connectivity.
2. Inspect/freeze help launcher.
3. **CLIENT-VIS-HOME-R2** — completely redesign Home using Client Briefing Board thesis, no embedded Àríyá region.
4. Inspect/freeze Home.
5. Properties, Projects, Support and Billing in separate original client-design slices.
6. Later implement actual Àríyá -> dedicated Captain-disabled Chatwoot human-takeover bridge.
7. Separately design client property/site Chatwoot + Captain support integration where provider support is enabled.
8. Later return to Auth visual/onboarding capability work.
9. Resume Admin Home separately when desired; Admin remains Lucid-style.

## Next action
When prompting resumes, run **CLIENT-HELP-001 — Floating Àríyá Launcher** first. Preserve all frozen shell/security behavior. Then run **CLIENT-VIS-HOME-R2**.
