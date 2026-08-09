# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN FUNCTIONALLY — FOUND-001F2A IDENTITY SCHEMA/RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS ACCEPTED/CANONICAL/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION ACCEPTED/CANONICAL/FROZEN MODEL — VIS-001A TWO-COLUMN AUTH ACCEPTED/CANONICAL/FROZEN — FOUND-001F3B PORTAL AUTHORIZATION CONDITIONAL / RAW ACCESS-ERROR LOGGING FIX NEXT**

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
- `SECURITY INVOKER` is the default. `SECURITY DEFINER` requires narrow explicit review.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider/Zod/access errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- Active-organisation selection is context only and is never authorization evidence.
- Consequential mutations eventually pass through an Action Registry/equivalent audited boundary.
- No security vulnerability exceptions accepted.

## Frozen foundation / Core / shells
**ACCEPTED / CANONICAL / FROZEN FUNCTIONALLY**
- Foundation + Core UI C1-C5E remain frozen.
- `/ui` remains the dev-only Core gallery.
- Admin shell: `/admin` with Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Client Portal shell: pathless `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Shells may reopen only for concrete regression or a separately supervised visual rollout.

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
- exactly one active membership may become automatic organisation context.
- multiple active memberships require explicit selection before organisation-scoped Portal work.
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

## FOUND-001F2A — Identity schema + RLS
**ACCEPTED / CANONICAL / FROZEN**
Canonical migrations:
- `supabase/migrations/20260809051520_identity_foundation.sql`
- `supabase/migrations/20260809052255_identity_grants_closure.sql`

Tables:
- `profiles(id -> auth.users, display_name, avatar_url, created_at)`
- `organisations(id, name, created_at)`
- `organisation_memberships(id, organisation_id, user_id, status active|suspended, created_at)` unique `(organisation_id,user_id)`
- `staff_members(user_id, status active|suspended, created_at)`

RLS/grants:
- profiles own SELECT/INSERT/UPDATE with column-level mutation grants;
- memberships own SELECT only;
- organisations SELECT only through active membership;
- staff own SELECT only;
- anon/PUBLIC none;
- service_role database role privileged but app client quarantined;
- no recursive policies, SECURITY DEFINER, seed identities, automatic profile trigger, RBAC or domain tables.

## FOUND-001F2B — Server-owned identity reads
**ACCEPTED / CANONICAL / FROZEN**
- `readCurrentIdentity()` starts from real `getAuthenticatedUser()`.
- all DB reads use caller-scoped Supabase + RLS.
- snapshot distinguishes unauthenticated, nullable profile, staff absent/active/suspended, memberships active/suspended, and active organisations.
- every active membership must resolve through organisation RLS before snapshot success.
- DB/status/integrity failure fails closed using one stable error; raw provider details are not logged/surfaced.
- no service role, writes, UI, RBAC or active-org persistence.

## FOUND-001F3A — Server-authoritative Admin access
**ACCESS MODEL ACCEPTED / CANONICAL / FROZEN; SHARED WRAPPER CURRENTLY HAS A REGRESSION INTRODUCED DURING F3B**
Canonical model remains:
- `requireActiveStaff()` derives from frozen `readCurrentIdentity()`; unauthenticated => 401; missing/suspended staff => 403; active staff => allowed; identity failure propagates fail-closed.
- `checkAdminAccess()` returns only `allowed | unauthenticated | forbidden`.
- `getAdminAccess()` returns only the minimal status and sets `Cache-Control: private, no-store` plus `Vary: Cookie, Authorization`.
- parent `/admin` `beforeLoad` gates the entire Admin family; anonymous => `/login` with internal `returnTo`; authenticated forbidden => `/access-denied`.
- route gate is UX only; future private Admin server data must independently call `requireActiveStaff()` or an approved derivative.

F3B modified the shared `src/lib/identity/access.functions.ts` and introduced `console.error(..., error)` around `getAdminAccess()`. This raw caught-error logging violates the canonical security invariant. Remove the raw logging without changing the accepted F3A access model or cache headers.

## FOUND-001F3B — Server-authoritative Portal access
**CONDITIONAL — ACCESS MODEL ACCEPTED; RAW ERROR LOGGING MUST CLOSE**
Verified files:
- `src/lib/identity/access.server.ts`
- `src/lib/identity/access.functions.ts`
- `src/routes/_portal.tsx`

Verified-good architecture:
- shared access module now has `requirePortalAccess()` and `checkPortalAccess()` built on frozen `readCurrentIdentity()`.
- Portal eligibility requires authenticated identity plus `identity.activeOrganisations.length > 0`.
- zero memberships or suspended-only memberships => forbidden; staff-only does not grant Portal access.
- one or multiple active organisations => Portal allowed; no organisation is automatically selected or persisted.
- staff + active client membership may coexist; staff status neither grants nor blocks Portal access.
- `getPortalAccess()` returns only `allowed | unauthenticated | forbidden` and sets `Cache-Control: private, no-store` plus `Vary: Cookie, Authorization`.
- parent `/_portal` `beforeLoad` gates `/`, `/properties`, `/projects`, `/support`, `/billing`; anonymous => `/login` with router-derived `returnTo`; authenticated forbidden => `/access-denied`.
- identity-read failures are allowed to propagate rather than being normalized into access states.
- `supabaseAdmin` remains confined to generated `src/integrations/supabase/client.server.ts`.
- no active-organisation context/selector/persistence was introduced; no Portal visual, database, auth transport, RBAC or dependency changes were observed.

### Blocking closure
`src/lib/identity/access.functions.ts` currently catches errors in both `getAdminAccess()` and `getPortalAccess()` and logs the raw caught object:
- `console.error("[getAdminAccess] Access check failed:", error)`
- `console.error("[getPortalAccess] Access check failed:", error)`

This can expose internal identity/database/validation/provider detail in server logs and regresses the previously accepted error-hygiene contract.

Required closure:
- remove raw caught-error logging from both server functions;
- simplest accepted implementation is to remove the unnecessary try/catch entirely and let failures propagate naturally;
- alternatively, a fixed non-sensitive event label with no attached error object is acceptable, but no logging is preferred here;
- preserve cache headers and minimal response shapes exactly;
- do not change `access.server.ts`, Admin route, Portal route, auth, database, visuals or dependencies.

## VIS-001A — Two-column Auth + visual language proof
**ACCEPTED / CANONICAL / FROZEN VISUALLY**
- desktop auth is a full-height two-column composition; left side is a Re:Solve operational preview; right side is a restrained ~420px form column.
- Inter remains the UI typeface; subtle 1px borders, nested neutral surfaces, near-zero shadow, restrained radii, disciplined Lucide usage.
- mobile collapses to form-first single-column.
- login, forgot-password, reset-password and callback share the same environment.
- password visibility controls are keyboard reachable, state-labelled, non-submitting, 36px targets with 16px icons, and use the canonical focus-visible variables.
- login helper description `Use your account credentials to continue.` is accepted. Prompt/instruction text must never appear in runtime UI.

## Standing visual direction
**APPROVED / STANDING PRODUCT REQUIREMENT**
The clean reference-led visual grammar must later propagate through Admin, then Portal, then future domain screens. Auth is only the first proof.

Canonical grammar:
- restrained Inter sizing/weights;
- Lucide generally 16–18px;
- neutral light mode + charcoal/graphite dark mode;
- subtle borders, near-zero shadows, restrained 14–18px major radii;
- disciplined card anatomy, separators and nested regions instead of card soup;
- structured rows/tables/charts/metrics rather than generic dashboard grids;
- meaningful accent colour only; no generic AI gradients, glassmorphism, neon or oversized marketing typography.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth, identity persistence/RLS and identity reads are frozen.
- Admin authorization model is accepted; shared access serverFn wrapper has a narrow raw-error logging regression from F3B.
- Portal surface authorization is implemented directionally and awaits only the same raw-error logging closure.
- active-organisation selection/context, invitations/onboarding, domain tables and broad RBAC do not exist yet.
- Admin and Portal visual propagation remain explicitly queued.

## Sequencing
Continue in small supervised slices:
1. FOUND-001F3B-FIX — remove raw caught-error logging from the shared route-facing access server functions only.
2. If clean, freeze F3B and restore F3A wrapper compliance.
3. FOUND-001F3C — active-organisation context/selection + server revalidation.
4. Resume approved visual rollout into Admin, then Portal.
5. Continue identity onboarding/invitation and domain work in separately reviewed slices.

## Next action
Run one narrow **FOUND-001F3B-FIX — Shared Access Error-Hygiene Closure**. Modify only `src/lib/identity/access.functions.ts` to remove raw caught-error logging from both Admin and Portal route-facing access functions while preserving their cache headers, minimal status responses and natural fail-closed propagation. Do not modify access decisions, routes, auth, database, visuals, active-org context or dependencies.