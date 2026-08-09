# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN FUNCTIONALLY — FOUND-001F2A IDENTITY SCHEMA/RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS ACCEPTED/CANONICAL/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION ACCEPTED/CANONICAL/FROZEN — FOUND-001F3B PORTAL AUTHORIZATION ACCEPTED/CANONICAL/FROZEN — FOUND-001F3C ACTIVE ORGANISATION CONTEXT ACCEPTED/CANONICAL/FROZEN — VIS-001A TWO-COLUMN AUTH ACCEPTED/CANONICAL/FROZEN — VIS-001B1 ADMIN SHELL VISUALS CONDITIONAL / TWO-LINE CLOSURE NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval

## Security invariants
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only. Private server functions/routes must independently authorize at their own server boundary.
- Normal user reads use caller-scoped Supabase clients + explicit filters + RLS.
- RLS, grants and security configuration are version-controlled and least-privilege.
- Generated `supabaseAdmin`/service-role client is PRESENT / GENERATED / QUARANTINED / UNUSED by Re:Solve application code.
- `SECURITY INVOKER` is default; `SECURITY DEFINER` requires narrow explicit review.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider/Zod/access errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- Active-organisation selection is context only and is never authorization evidence; every organisation-specific server operation must freshly revalidate the exact requested organisation.
- Consequential mutations eventually pass through an Action Registry/equivalent audited boundary.
- Prompt/task/supervisor wording must never leak into runtime UI or source comments.
- No security vulnerability exceptions accepted.

## Frozen foundation / Core / shells
**ACCEPTED / CANONICAL / FROZEN FUNCTIONALLY**
- Foundation + Core UI C1-C5E remain frozen functionally.
- `/ui` remains the dev-only Core gallery.
- Admin shell: `/admin` with Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Client Portal shell: pathless `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Functional shells may reopen only for concrete regression or separately supervised visual rollout.

## SECURITY-GATE-001
**ACCEPTED / CLOSED**
- `@tanstack/react-router ^1.170.18`
- `@tanstack/react-start ^1.168.32`
- `@tanstack/router-plugin ^1.168.23`
- `@tanstack/react-table 8.20.5`
- `@supabase/supabase-js ^2.112.2`
- `@supabase/ssr ^0.12.4`
- top-level `"overrides": { "js-yaml": "4.3.1" }`

## FOUND-001F0 — Identity/Auth architecture
**ACCEPTED / CANONICAL**
Canonical identity facts are distinct: Auth User, Profile, Organisation, Organisation Membership, Staff Access.

Surface rules:
- `/admin` requires authenticated active staff access.
- Portal requires authenticated active organisation membership.
- exactly one active organisation resolves automatically as Portal context.
- multiple active organisations require explicit selection before organisation-scoped Portal work.
- selected organisation is context only; server/RLS revalidate authorization independently.
- a user may be staff, organisation member, both, or member of multiple organisations.

## FOUND-001F1A/F1B — Authentication
**ACCEPTED / CANONICAL / FROZEN FUNCTIONALLY**
- Lovable Cloud/Supabase active.
- Shared cookie-backed `@supabase/ssr` session is canonical for browser/SSR auth; validated identity uses `getClaims()`.
- Generated bearer serverFn transport remains a separate accepted path.
- `/login`, `/forgot-password`, `/reset-password`, `/auth/callback` are canonical.
- server-side PKCE exchange; safe internal redirects; neutral auth errors; no public signup/social login/MFA yet.
- `src/start.ts` keeps error middleware + generated auth attacher + explicit CSRF middleware.
- canonical redirect validator is `getSafeRedirect()` in `src/lib/auth.functions.ts`; do not duplicate it.

## FOUND-001F2A/F2B — Identity persistence + server reads
**ACCEPTED / CANONICAL / FROZEN**
Canonical migrations:
- `supabase/migrations/20260809051520_identity_foundation.sql`
- `supabase/migrations/20260809052255_identity_grants_closure.sql`

Tables: `profiles`, `organisations`, `organisation_memberships`, `staff_members`.

Canonical behavior:
- least-privilege RLS/grants; no service-role application path, recursive policy, SECURITY DEFINER, seed identities, automatic profile trigger, RBAC or domain tables.
- `readCurrentIdentity()` starts from real `getAuthenticatedUser()` and uses caller-scoped Supabase + RLS only.
- active memberships must resolve through organisation RLS before snapshot success; DB/status/integrity failure fails closed.

## FOUND-001F3A — Server-authoritative Admin access
**ACCEPTED / CANONICAL / FROZEN**
- `requireActiveStaff()` / `checkAdminAccess()` derive from frozen identity reads.
- unauthenticated => 401; missing/suspended staff => 403; active staff => allowed; identity failure propagates fail-closed.
- `getAdminAccess()` returns only `allowed | unauthenticated | forbidden` with `Cache-Control: private, no-store` and `Vary: Cookie, Authorization`.
- parent `/admin` gate covers the complete Admin family.
- future private Admin server data must independently call `requireActiveStaff()` or an approved derivative.

## FOUND-001F3B — Server-authoritative Portal access
**ACCEPTED / CANONICAL / FROZEN**
- `requirePortalAccess()` / `checkPortalAccess()` derive from frozen identity reads.
- Portal eligibility requires authenticated identity plus at least one current active organisation.
- zero/suspended-only memberships => forbidden; staff-only does not grant Portal access.
- `getPortalAccess()` returns only minimal access status with private/no-store + Cookie/Authorization Vary.
- identity failures propagate naturally; no raw caught-error logging.

## FOUND-001F3C — Active organisation context + exact-organisation revalidation
**ACCEPTED / CANONICAL / FROZEN**
- `requireActiveOrganisation(organisationId)` runtime-validates UUID input, obtains a fresh `requirePortalAccess()` identity, and matches the exact requested organisation against newly resolved `activeOrganisations`.
- `rs_portal_org` is an untrusted session pointer containing only organisation UUID; `httpOnly`, `SameSite=Lax`, production-secure, path `/`, no persistent expiry/max-age.
- zero active organisations => forbidden; exactly one => automatic context; multiple with absent/malformed/stale pointer => explicit selection required.
- selection-required chooser starts unselected; `selectPortalOrganisation` authorizes the exact organisation before writing the cookie.
- selector lives outside `/_portal`, uses canonical `getSafeRedirect()` from `auth.functions.ts`, and cannot form a redirect loop.
- no service role, DB changes, RBAC, domain data, test users or seed data.

## RUNTIME-DIAG-001 — `Error: aborted`
**CLOSED / TRANSIENT EDITOR-HMR TRANSPORT EVENT / NO APP CHANGE REQUIRED**
- direct preview and anonymous redirect matrix passed.
- no deterministic document/serverFn abort, redirect loop, `src/start.ts` involvement or root-boundary involvement.
- do not add generic AbortError swallowing/retries or weaken authorization for this closed event.

## VIS-001A — Two-column Auth + visual language proof
**ACCEPTED / CANONICAL / FROZEN VISUALLY**
- desktop auth is a full-height two-column composition; left is a Re:Solve operational preview and right is a restrained form column.
- Inter remains the UI typeface; subtle borders, nested neutral surfaces, near-zero shadow, restrained radii, disciplined Lucide usage.
- mobile is form-first single-column.
- password visibility controls are keyboard reachable, state-labelled, non-submitting and use the canonical focus-visible variables.
- login helper description `Use your account credentials to continue.` is accepted.

## Standing visual direction
**APPROVED / STANDING PRODUCT REQUIREMENT**
The clean reference-led grammar propagates through Admin, then Portal, then future domain screens.

Canonical grammar:
- restrained Inter sizing/weights;
- Lucide generally 16–18px with thin technical treatment;
- neutral light mode + charcoal/graphite dark mode;
- subtle 1px borders, near-zero shadows, restrained major radii;
- disciplined card anatomy, separators/inset regions and nested surfaces instead of card soup;
- structured rows/tables/charts/metrics rather than generic dashboard grids;
- meaningful accent colour concentrated in icon/status/data surfaces;
- no generic AI gradients, glassmorphism, neon, giant marketing headings or decorative SaaS clutter.
- Admin is denser and operational; Portal later uses the same family with more breathing room.

## VIS-001B1 — Admin Shell visual redesign
**CONDITIONAL — VISUAL ARCHITECTURE ACCEPTED; TWO SMALL TOPBAR CLOSURES REQUIRED**

Verified current runtime files:
- `src/components/shell/admin/AdminShell.tsx`
- `src/components/shell/admin/AdminSidebar.tsx`
- `src/components/shell/admin/AdminTopBar.tsx`
- `src/components/shell/admin/AdminPageHeader.tsx`
- `src/components/shell/admin/AdminBreadcrumbs.tsx`

Verified-good visual/functional architecture:
- existing Core Sidebar architecture remains in place; no parallel shell was created.
- expanded sidebar continues to use the canonical 16rem/256px sidebar contract, within the approved 240–260px visual target.
- sidebar now uses quiet primary surface, subtle border, 28px brand mark, 36px nav rows, ~13.5px labels and 18px Lucide icons.
- selected nav remains route-aware and uses a restrained selected surface rather than a large brand-colour pill.
- topbar remains the existing shared component and retains sidebar trigger, route context, Cmd/Ctrl+K search, notifications, Àríyá and account dropdown.
- command menu remains unchanged and still binds Meta/Ctrl+K.
- page header now uses restrained 28px/600 title treatment and 14px supporting copy.
- shell content frame uses the available workspace with a max 1600px content frame and canonical responsive gutters.
- `src/routes/admin.tsx` is unchanged; authoritative Admin access remains frozen.
- Core implementations, styles.css, Portal/Auth, DB, identity and dependencies were not part of the visual change set.
- Lovable reported build/lint/typecheck success.

Blocking closure before B1 freezes:
1. Account-menu trigger in `AdminTopBar.tsx` dropped the canonical focus offset classes. Restore the full frozen focus-visible contract, including `--rs-focus-offset-width` and `--rs-focus-offset-color`.
2. Preserve the canonical fictional account placeholder exactly as `Amara Okafor` / `Administrator`; B1 shortened the role to `Admin`.

No other B1 redesign is requested in the closure.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth, identity persistence/RLS, identity reads, Admin authorization, Portal authorization and tenancy context are frozen.
- Admin shell visual direction is implemented and awaits one tiny topbar closure.
- Admin Home is still the placeholder StatePanel and is the next visible proof after B1 freezes.
- No invitation/onboarding flow, domain tables or broad RBAC exists yet.
- Portal visual propagation remains explicitly queued after Admin approval.

## Sequencing
1. close VIS-001B1 account focus-contract + placeholder-role regressions only.
2. freeze VIS-001B1.
3. VIS-001B2 — replace only Admin Home placeholder with the approved operational dashboard proof.
4. inspect/freeze Admin Home visual grammar.
5. propagate the approved family into Portal in a separate VIS slice.
6. continue identity onboarding/invitation and domain work separately.

## Next action
Run one tiny **VIS-001B1-FIX — Account Trigger Closure**. Modify only `src/components/shell/admin/AdminTopBar.tsx`: restore the complete canonical focus-visible offset contract on the account trigger and restore the fictional role label to `Administrator`. Preserve all other B1 visuals and behavior. Then run the full build/lint/typecheck gate and stop.