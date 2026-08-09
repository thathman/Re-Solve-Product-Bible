# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A/F1B AUTH ACCEPTED/FROZEN FUNCTIONALLY — FOUND-001F2A/F2B IDENTITY ACCEPTED/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION ACCEPTED/FROZEN — FOUND-001F3B PORTAL AUTHORIZATION ACCEPTED/FROZEN — FOUND-001F3C TENANCY CONTEXT ACCEPTED/FROZEN — VIS-001B1 ADMIN SHELL VISUALS ACCEPTED/FROZEN — CLIENT VISUAL AUTHORITY SPLIT ACCEPTED — CLIENT AUTH/PORTAL AIRIX ROLLOUT NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client-facing visual references: `Airix360/AM-Client-Docs` Design system + `Airix360/airixmedia-web`
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval

## Security invariants
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only. Private server functions/routes independently authorize at their server boundary.
- Normal user reads use caller-scoped Supabase + RLS; generated `supabaseAdmin` remains server-only, quarantined and unused by Re:Solve application authorization.
- `SECURITY INVOKER` is default; `SECURITY DEFINER` requires narrow explicit review.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider/Zod/access errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- Active-organisation selection is context only, never authorization evidence. Organisation-specific server work freshly revalidates the exact requested organisation.
- Consequential mutations eventually pass through an Action Registry/equivalent audited boundary.
- Prompt/task/supervisor wording must never leak into runtime UI or source comments.
- No security vulnerability exceptions accepted.

## Frozen foundation / Core / functional shells
**ACCEPTED / CANONICAL / FROZEN FUNCTIONALLY**
- Foundation + Core UI C1-C5E remain frozen.
- `/ui` remains the dev-only Core gallery.
- Admin routes: Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Portal family: `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Auth routes: `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`.

## Security gate
**ACCEPTED / CLOSED**
- `@tanstack/react-router ^1.170.18`
- `@tanstack/react-start ^1.168.32`
- `@tanstack/router-plugin ^1.168.23`
- `@tanstack/react-table 8.20.5`
- `@supabase/supabase-js ^2.112.2`
- `@supabase/ssr ^0.12.4`
- top-level `overrides.js-yaml = 4.3.1`.

## Authentication / identity / authorization
**ACCEPTED / CANONICAL / FROZEN FUNCTIONALLY**
- Shared cookie-backed `@supabase/ssr` session is canonical for browser/SSR auth; validated identity uses `getClaims()`.
- server-side PKCE exchange, safe internal redirects and neutral auth errors are frozen.
- canonical redirect validator is `getSafeRedirect()` in `src/lib/auth.functions.ts`; do not duplicate it.
- canonical identity tables: `profiles`, `organisations`, `organisation_memberships`, `staff_members` with least-privilege RLS/grants.
- `readCurrentIdentity()` uses caller-scoped Supabase + RLS and fails closed on DB/status/integrity failure.
- Admin: `requireActiveStaff()` / `checkAdminAccess()` / `getAdminAccess()` are frozen; parent `/admin` gates the full Admin family.
- Portal: `requirePortalAccess()` / `checkPortalAccess()` are frozen; active organisation membership is required.
- Exact tenancy: `requireActiveOrganisation(organisationId)` freshly revalidates exact active organisation access; `rs_portal_org` is an untrusted UUID-only context pointer.
- zero active Portal organisations => forbidden; exactly one => automatic context; multiple + absent/malformed/stale pointer => explicit selection required.
- no service-role application path, RBAC, domain data, seed/test users or invitation flow exists yet.

## RUNTIME-DIAG-001 — `Error: aborted`
**CLOSED / TRANSIENT EDITOR-HMR EVENT / NO APP CHANGE REQUIRED**
- direct preview passed; no deterministic document/serverFn abort or redirect loop.
- do not add generic AbortError swallowing/retries or weaken authorization.

## VIS-001B1 — Admin Shell visual redesign
**ACCEPTED / CANONICAL / FROZEN VISUALLY**
- Existing Core Sidebar/AdminShell architecture was refined rather than replaced.
- Admin remains the previously approved Lucid-style Re:Solve dialect: quiet neutral surfaces, restrained Inter typography, 16–18px Lucide icons, subtle borders, low shadow, denser operational composition.
- sidebar, topbar, command search, notifications, Àríyá, account dropdown, responsive behavior and Admin authorization are preserved.
- account placeholder remains `Amara Okafor` / `Administrator`; account trigger has the full frozen focus-visible contract.
- Do not apply the Airix client visual system to Admin.
- Do not reopen B1 absent concrete regression or explicit owner request.

## Surface-specific visual authority
**ACCEPTED / CANONICAL PRODUCT DECISION**

Re:Solve now has TWO deliberate visual dialects sharing one functional/Core grammar.

### A. Admin visual authority
- Admin remains on the accepted/frozen Lucid-style Re:Solve system from VIS-001B1.
- Inter remains Admin UI typography.
- neutral/graphite palette, restrained 8–16px radii as already implemented, quiet selected nav, near-zero shadow, operational density.
- Airix client-facing styling must NOT leak into `/admin`.

### B. Client-facing visual authority
Applies to:
- `/login`
- `/forgot-password`
- `/reset-password`
- `/auth/callback`
- `/select-organisation`
- `/access-denied` when reached as a client-facing surface
- Portal shell and `/`, `/properties`, `/projects`, `/support`, `/billing`

Canonical sources:
1. `Airix360/AM-Client-Docs` — Re:Solve Design System / Client Portal references supplied by owner.
2. `Airix360/airixmedia-web` — supporting systems-first visual language and interaction reference.

Client-facing grammar from the supplied design system:
- warm paper canvas around `oklch(97% 0.012 60)`.
- warm surface around `oklch(94% 0.014 60)`.
- warm ink around `oklch(22% 0.02 55)` and muted text around `oklch(45% 0.02 55)`.
- line/border around `oklch(88% 0.014 60)`.
- primary accent is terracotta around `oklch(58% 0.14 35)`.
- client dark/featured surfaces use warm charcoal around `oklch(17–22% 0.012–0.014 60)` with warm inverse ink.
- status colour logic retains info/success/warning/danger semantics.
- Space Grotesk is client UI/body type.
- Instrument Serif italic is reserved for greetings, section-display moments and moments of address; never body copy, controls or data.
- JetBrains Mono is used selectively for currency, dates, identifiers and technical data.
- client control/card radius is deliberately tool-like, generally 3–6px; avoid the Admin's larger rounded SaaS treatment.
- borders over shadows; elevation only for floating overlays/drawers/command/Àríyá.
- spacing rhythm follows 4/8/12/16/24/32/48/64.
- Lucide remains the icon family; client UI should remain restrained and editorial rather than icon-heavy.

### Client Portal Home reference anatomy
The supplied Client Portal Home is the target direction, not merely inspiration:
- horizontal top navigation rather than Admin-style sidebar.
- Re:Solve display wordmark at left, active organisation context adjacent, then Home/Properties/Projects/Support/Billing.
- compact workspace search, notifications and avatar at right.
- warm editorial canvas with large Instrument Serif greeting.
- prominent dark active-project panel with restrained technical pattern, progress, approval status and real-route actions.
- recent activity rendered as simple editorial rows with mono date/time labels.
- right column contains compact property incident, overdue invoice, support and Àríyá modules.
- information is calm, sparse and client-oriented; do not clone Admin density.

## Client theme implementation boundary
- Do NOT rewrite global Re:Solve semantic tokens in a way that changes Admin.
- Implement the Airix client language as a scoped client theme/dialect applied inside Auth/Portal/client-facing wrappers.
- Reuse Core behavior and accessibility contracts, but use client-specific composition and scoped visual variables/classes.
- Fonts must be self-hosted/bundled. Remote Google Fonts/CDN/font runtime dependencies are not canonical.
- Approved self-host route is Fontsource packages for Space Grotesk and Instrument Serif; existing JetBrains Mono remains available.
- External runtime stock-image dependencies are not canonical.

## Auth visual state
**FUNCTIONAL AUTH FROZEN; CURRENT REMOTE-IMAGE VERSION IS TEMPORARY / SUPERSEDED BY CLIENT VISUAL ROLLOUT**
- Current `AuthLayout.tsx` has a 50/50 image-left/form-right composition and a remote Unsplash image.
- The exact prior image asset was unavailable in Lovable; this is CLOSED as a missing-asset/no-action event, not an ongoing blocker.
- Do not keep chasing the missing image.
- The next Auth visual implementation should be redesigned under the Airix client-facing authority and remove the remote Unsplash runtime dependency.
- Preserve all frozen authentication behavior, password accessibility, validation, sessions and safe redirects.

## Current Portal state
- Functional Portal shell is frozen and currently owns horizontal NavigationMenu, mobile Sheet nav, command search, notifications, shared Àríyá panel and account placeholder.
- F3C now provides safe browser-facing active organisation context from `/_portal` but current shell still displays fictional `Chinedu Okeke / Acme Properties Ltd.` placeholders.
- Portal Home remains a placeholder `StatePanel` and is ready for the supplied Airix/Re:Solve client-home visual proof.
- Do not add real domain database data during the visual rollout; use believable static demonstration content only.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth functionality, identity/RLS, Admin authorization, Portal authorization and tenancy context are frozen.
- Admin shell visual grammar is frozen separately from the new client visual authority.
- no invitation/onboarding flow, domain tables or broad RBAC exists yet.

## Sequencing
Continue in small supervised slices:
1. CLIENT-VIS-001A — establish scoped Airix client theme + self-hosted client fonts and restyle Auth only; remove remote Unsplash dependency. Do not modify Admin or Portal yet.
2. inspect/freeze client theme primitives and Auth application.
3. CLIENT-VIS-001B — restyle Portal shell/top navigation under the same client theme while preserving F3B/F3C behavior.
4. CLIENT-VIS-001C — implement supplied Client Portal Home reference using static demo data only.
5. propagate the approved client grammar to Properties, Projects, Support, Billing in small slices.
6. separately resume VIS-001B2 Admin Home when owner chooses; Admin remains Lucid-style.
7. continue onboarding/invitations and domain work separately.

## Next action
Run **CLIENT-VIS-001A — Scoped Airix Client Theme + Auth**. Create the client-only visual dialect without changing global Admin styling. Self-host Space Grotesk + Instrument Serif, retain JetBrains Mono, remove the remote Unsplash image dependency, and restyle only Auth/client entry surfaces under the warm Airix/Re:Solve grammar. Preserve all auth/security behavior and stop before Portal shell changes.
