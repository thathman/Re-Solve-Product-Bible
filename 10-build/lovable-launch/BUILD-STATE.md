# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A/F1B AUTH ACCEPTED/FROZEN — FOUND-001F2A/F2B IDENTITY ACCEPTED/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION ACCEPTED/FROZEN — FOUND-001F3B PORTAL AUTHORIZATION ACCEPTED/FROZEN — FOUND-001F3C TENANCY CONTEXT ACCEPTED/FROZEN — VIS-001B1 ADMIN SHELL VISUALS ACCEPTED/FROZEN — VIS-001A AUTH IMAGE-LEFT REVISION CONDITIONAL ON EXACT LOCAL IMAGE ASSET**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
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
- `@supabase/react-table 8.20.5` is not canonical; actual frozen table dependency remains `@tanstack/react-table 8.20.5`.
- `@supabase/supabase-js ^2.112.2`
- `@supabase/ssr ^0.12.4`
- top-level `overrides.js-yaml = 4.3.1`.

## FOUND-001F1A/F1B — Authentication
**ACCEPTED / CANONICAL / FROZEN FUNCTIONALLY**
- Shared cookie-backed `@supabase/ssr` session is canonical for browser/SSR auth; validated identity uses `getClaims()`.
- Generated bearer serverFn transport remains separately accepted.
- server-side PKCE exchange, safe internal redirects and neutral auth errors are frozen.
- canonical redirect validator is `getSafeRedirect()` in `src/lib/auth.functions.ts`; do not duplicate it.
- no public signup/social login/MFA yet.

## FOUND-001F2A/F2B — Identity persistence + reads
**ACCEPTED / CANONICAL / FROZEN**
Canonical migrations:
- `supabase/migrations/20260809051520_identity_foundation.sql`
- `supabase/migrations/20260809052255_identity_grants_closure.sql`

Tables: `profiles`, `organisations`, `organisation_memberships`, `staff_members`.

Canonical behavior:
- least-privilege RLS/grants; no service-role application path, recursive policy, SECURITY DEFINER, seed identities, automatic profile trigger, RBAC or domain tables.
- `readCurrentIdentity()` starts from real `getAuthenticatedUser()` and uses caller-scoped Supabase + RLS.
- active memberships must resolve through organisation RLS before snapshot success; DB/status/integrity failure fails closed.

## FOUND-001F3A — Admin authorization
**ACCEPTED / CANONICAL / FROZEN**
- `requireActiveStaff()` / `checkAdminAccess()` derive from frozen identity reads.
- unauthenticated => 401; missing/suspended staff => 403; active staff => allowed; identity failure propagates fail-closed.
- `getAdminAccess()` returns only minimal status with `Cache-Control: private, no-store` and `Vary: Cookie, Authorization`.
- parent `/admin` gate covers the complete Admin family.

## FOUND-001F3B — Portal authorization
**ACCEPTED / CANONICAL / FROZEN**
- `requirePortalAccess()` / `checkPortalAccess()` derive from frozen identity reads.
- Portal eligibility requires authenticated identity plus at least one current active organisation.
- zero/suspended-only memberships => forbidden; staff-only does not grant Portal access.
- minimal route-facing status response is private/no-store and varies on Cookie/Authorization.

## FOUND-001F3C — Tenancy context + exact organisation revalidation
**ACCEPTED / CANONICAL / FROZEN**
- `requireActiveOrganisation(organisationId)` runtime-validates UUID input, obtains a fresh Portal identity and matches the exact requested organisation against newly resolved active organisations.
- `rs_portal_org` is an untrusted session pointer containing only an organisation UUID; `httpOnly`, `SameSite=Lax`, production-secure, path `/`, no persistent expiry/max-age.
- zero active organisations => forbidden; exactly one => automatic context; multiple with absent/malformed/stale pointer => explicit selection required.
- selection-required chooser starts unselected; selection authorizes exact organisation before writing cookie.
- selector lives outside `/_portal` and uses canonical `getSafeRedirect()`.
- no service role, DB changes, RBAC, domain data, test users or seed data.

## RUNTIME-DIAG-001 — `Error: aborted`
**CLOSED / TRANSIENT EDITOR-HMR EVENT / NO APP CHANGE REQUIRED**
- direct preview passed; no deterministic document/serverFn abort or redirect loop.
- do not add generic AbortError swallowing/retries or weaken authorization.

## VIS-001B1 — Admin Shell visual redesign
**ACCEPTED / CANONICAL / FROZEN VISUALLY**
Verified current architecture:
- existing Core Sidebar/AdminShell architecture was refined rather than replaced.
- sidebar uses quiet neutral surface, subtle border, 28px brand mark, 36px nav rows, ~13.5px labels, 18px Lucide icons and subdued selected state.
- topbar preserves sidebar trigger, route context, Cmd/Ctrl+K search, notifications, Àríyá and account dropdown.
- page header uses 28px/600 title treatment and restrained supporting copy.
- content frame uses a max 1600px workspace with canonical responsive gutters.
- account placeholder remains exactly `Amara Okafor` / `Administrator`.
- account trigger now has the complete frozen focus-visible contract including ring offsets.
- `src/routes/admin.tsx` remains unchanged; Admin authorization is frozen.
- Lovable reported full build/lint/typecheck success.

Do not reopen B1 absent a concrete regression or owner-requested visual change.

## VIS-001A — Authentication visual direction, revised
**FUNCTIONAL AUTH FROZEN; CURRENT IMAGE-LEFT COMPOSITION ACCEPTED; IMAGE ASSET CONDITIONAL**

Owner's current visual requirement supersedes the earlier left-side operational-preview treatment:
- desktop must be a strict image-left / auth-form-right composition, approximately 50/50 and full viewport height.
- the image is an edge-to-edge editorial/photo surface using `object-cover`.
- auth form remains on the right at approximately 400–440px max width and vertically centered.
- below the desktop breakpoint the image may hide and the form becomes the primary single-column surface.
- `AuthProductPreview` has been intentionally removed/deleted from the current visual direction.
- authentication behavior, validation, password controls, safe redirect and session flow remain functionally frozen.

### Current conditional issue
`src/components/auth/AuthLayout.tsx` currently hard-codes a remote Unsplash URL:
`https://images.unsplash.com/photo-1497366754035-f200968a6e72?...`

This is NOT accepted as canonical because:
1. the owner asked for the exact supplied reference image, not a substituted stock office image;
2. remote image hosting creates an unnecessary production/runtime dependency and weakens final self-host portability.

Required closure:
- use the exact owner-supplied reference image as a local app asset;
- do not substitute another stock image;
- if Lovable cannot access the supplied image bytes/file, STOP and report that instead of guessing;
- remove the remote Unsplash runtime URL;
- preserve the accepted 50/50 composition and all auth behavior.

## Standing visual direction
**APPROVED / STANDING PRODUCT REQUIREMENT**
- restrained Inter sizing/weights;
- Lucide generally 16–18px;
- neutral light mode + charcoal/graphite dark mode;
- subtle 1px borders, near-zero shadows and restrained radii;
- structured/nested surfaces instead of card soup;
- meaningful accent colour concentrated in icons/status/data;
- no generic AI gradients, glassmorphism, neon, giant marketing headings or decorative SaaS clutter.
- Admin is denser and operational; Portal later uses the same family with more breathing room.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth functionality, identity/RLS, Admin authorization, Portal authorization and tenancy context are frozen.
- Admin shell visual grammar is now frozen.
- Admin Home still needs the VIS-001B2 operational dashboard proof.
- Auth image-left composition needs one asset-source closure before its revised visual state freezes.
- Portal visual propagation remains queued after Admin Home approval.
- no invitation/onboarding flow, domain tables or broad RBAC exists yet.

## Sequencing
1. VIS-001A-IMAGE-FIX — replace remote Unsplash substitution with the exact supplied reference image stored locally; no other Auth change.
2. if clean, freeze revised Auth image-left visual state.
3. VIS-001B2 — replace only Admin Home placeholder with the approved static operational dashboard proof.
4. inspect/freeze Admin Home visual grammar.
5. propagate the approved visual family into Portal in a separate VIS slice.
6. continue onboarding/invitations and domain work separately.

## Next action
Run one tiny **VIS-001A-IMAGE-FIX — Exact Local Reference Asset**. Modify only the Auth image asset/source as necessary. Preserve the 50/50 image-left/form-right layout, mobile behavior and all frozen auth functionality. Do not substitute stock imagery. If the exact supplied reference image is unavailable to Lovable, stop and report the blocker.