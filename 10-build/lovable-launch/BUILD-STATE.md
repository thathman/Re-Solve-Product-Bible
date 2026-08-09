# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN FUNCTIONALLY — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN FUNCTIONALLY — FOUND-001F2A IDENTITY SCHEMA/RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS ACCEPTED/CANONICAL/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION ACCEPTED/CANONICAL/FROZEN — FOUND-001F3B PORTAL AUTHORIZATION ACCEPTED/CANONICAL/FROZEN — VIS-001A TWO-COLUMN AUTH ACCEPTED/CANONICAL/FROZEN — FOUND-001F3C ACTIVE ORGANISATION CONTEXT CONDITIONAL / NARROW CLOSURE REQUIRED**

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
- Foundation + Core UI C1-C5E remain frozen.
- `/ui` remains the dev-only Core gallery.
- Admin shell: `/admin` with Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Client Portal shell: pathless `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Shells may reopen only for concrete regression or separately supervised visual rollout.

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
- exactly one active organisation may resolve automatically as context.
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
- canonical redirect validator is `getSafeRedirect()` in `src/lib/auth.functions.ts`; do not create duplicates.

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

RLS/grants remain least-privilege; no service-role application path, recursive policy, SECURITY DEFINER, seed identities, automatic profile trigger, RBAC or domain tables.

## FOUND-001F2B — Server-owned identity reads
**ACCEPTED / CANONICAL / FROZEN**
- `readCurrentIdentity()` starts from real `getAuthenticatedUser()`.
- all DB reads use caller-scoped Supabase + RLS.
- snapshot distinguishes unauthenticated, nullable profile, staff absent/active/suspended, memberships active/suspended, and active organisations.
- every active membership must resolve through organisation RLS before snapshot success.
- DB/status/integrity failure fails closed using one stable error; raw provider details are not logged/surfaced.
- no service role, writes, UI, RBAC or active-org persistence.

## FOUND-001F3A — Server-authoritative Admin access
**ACCEPTED / CANONICAL / FROZEN**
- reusable `requireActiveStaff()` and `checkAdminAccess()` derive from frozen identity reads.
- unauthenticated => 401; missing/suspended staff => 403; active staff => allowed; identity failure propagates fail-closed.
- `getAdminAccess()` returns only `allowed | unauthenticated | forbidden`, with `Cache-Control: private, no-store` and `Vary: Cookie, Authorization`.
- parent `/admin` gate covers the complete Admin family.
- future private Admin server data must independently call `requireActiveStaff()` or an approved derivative.

## FOUND-001F3B — Server-authoritative Portal access
**ACCEPTED / CANONICAL / FROZEN**
- reusable `requirePortalAccess()` and `checkPortalAccess()` derive from frozen identity reads.
- Portal eligibility requires authenticated identity plus at least one current active organisation.
- zero/suspended-only memberships => forbidden; staff-only does not grant Portal access.
- one or multiple active organisations => surface access allowed.
- `getPortalAccess()` returns only `allowed | unauthenticated | forbidden`, with private/no-store + Cookie/Authorization Vary.
- parent `/_portal` gate covers `/`, `/properties`, `/projects`, `/support`, `/billing`.
- identity failures propagate naturally; no raw caught-error logging.

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
- login, forgot-password, reset-password and callback share the same environment.
- password visibility controls are keyboard reachable, state-labelled, non-submitting and use the canonical focus-visible variables.
- login helper description `Use your account credentials to continue.` is accepted.

## Standing visual direction
**APPROVED / STANDING PRODUCT REQUIREMENT**
The clean reference-led grammar must later propagate through Admin, then Portal, then future domain screens. Auth is only the first proof.

Canonical grammar:
- restrained Inter sizing/weights;
- Lucide generally 16–18px;
- neutral light mode + charcoal/graphite dark mode;
- subtle 1px borders, near-zero shadows, restrained 14–18px major radii;
- disciplined card anatomy, separators and nested regions instead of card soup;
- structured rows/tables/charts/metrics rather than generic dashboard grids;
- meaningful accent colour only; no generic AI gradients, glassmorphism, neon or oversized marketing typography.

## FOUND-001F3C — Active organisation context + exact-organisation revalidation
**CONDITIONAL — CORE TENANCY BOUNDARY ACCEPTED; SELECTOR/REDIRECT/SOURCE-HYGIENE CLOSURE REQUIRED**

Verified implementation files:
- `src/lib/identity/access.server.ts`
- `src/lib/identity/organisation-context.server.ts`
- `src/lib/identity/organisation-context.functions.ts`
- `src/routes/_portal.tsx`
- `src/routes/select-organisation.tsx`
- generated `src/routeTree.gen.ts`
- `src/lib/utils.ts` was also modified and requires rollback of the duplicate redirect helper.

Verified-good architecture:
- `requireActiveOrganisation(organisationId)` validates UUID input and obtains a fresh authoritative Portal identity through `requirePortalAccess()` before matching the requested ID against current `activeOrganisations`.
- requested organisation not currently active => stable 403; invalid direct primitive UUID => stable 400; identity/RLS failures propagate fail-closed.
- `rs_portal_org` stores only an organisation UUID and is `httpOnly`, `SameSite=Lax`, production-secure, path `/`, with no persistent expiry/max-age.
- cookie is treated as an untrusted pointer: malformed/absent/stale values do not authorize access.
- zero active organisations => forbidden.
- exactly one active organisation resolves automatically and ignores any stale cookie.
- multiple active organisations resolve only when the cookie points to a currently active organisation; otherwise context is `selection_required`.
- browser-safe context exposes only organisation `{id,name}`; `membershipId` remains server-side.
- `getPortalOrganisationContext()` is private/no-store and varies on Cookie/Authorization.
- `selectPortalOrganisation` is POST + Zod UUID input; it calls `requireActiveOrganisation()` before writing the context cookie and returns only browser-safe selected organisation data.
- parent `/_portal` now distinguishes unauthenticated, forbidden, selection-required and resolved context states; resolved route context is explicitly marked UX context only, never authorization evidence.
- no domain reads, service role, RBAC, database migrations, seed/test users or Portal shell redesign were observed.

Blocking closure:
1. `src/lib/utils.ts` now contains a second `getSafeRedirect()`. Remove that new duplicate and import/reuse canonical `getSafeRedirect()` from `src/lib/auth.functions.ts` in the selector route.
2. `/select-organisation` currently renders a chooser even when context has exactly one active organisation. Exactly-one must redirect directly to canonical safe `returnTo` (or `/`) because selection is unnecessary.
3. when context is `selection_required`, the selector currently initializes the first organisation as selected. Do not preselect the first organisation; explicit multi-org selection must start unselected. A valid existing multi-org selection may remain preselected when the user explicitly visits the chooser to switch.
4. remove task-history/source-leak wording such as `F3B legacy` from runtime comments. Prefer normal product-purpose comments; do not add FOUND/task/prompt/supervisor language.
5. preserve all accepted cookie, exact-org authorization, context-resolution, cache, Admin/F3B and no-service-role behavior while closing the above.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth, identity persistence/RLS, identity reads, Admin authorization and Portal surface authorization are frozen.
- F3C tenancy/context architecture exists but is conditional on one narrow selector/redirect/source-hygiene cleanup.
- No invitation/onboarding flow, domain tables or broad RBAC exists yet.
- Admin and Portal visual propagation remain explicitly queued.

## Sequencing
Continue in small supervised slices:
1. close FOUND-001F3C selector/redirect/source-hygiene issues only.
2. if clean, freeze F3C tenancy boundary.
3. resume approved visual rollout into Admin, then Portal.
4. continue identity onboarding/invitation and domain work in separately reviewed slices.

## Next action
Run one narrow **FOUND-001F3C-FIX — Selector Explicitness + Canonical Redirect Closure**. Remove the duplicate redirect helper, make exactly-one organisation bypass the chooser, ensure multi-org selection-required state begins unselected, remove task-history comments, and preserve all accepted exact-organisation authorization/cookie/context behavior. Do not add domain data, database changes, service-role usage, RBAC, test users or broad visual changes.