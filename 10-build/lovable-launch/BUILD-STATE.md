# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN — FOUND-001F2A IDENTITY SCHEMA + BASELINE RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS CONDITIONAL / ERROR-HYGIENE + ACTIVE-ORG CONSISTENCY FIX NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`.
- Current app: `thathman/re-solve-c560d62c` on `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit owner approval.

## Security memory
**ACCEPTED / CANONICAL**
- Roles/permissions/capabilities are server-controlled; browser metadata is never authoritative.
- Auth/authz is enforced at server-function/server-route boundaries and by RLS, not only UI navigation.
- Never invent security helpers that do not exist; extend real server boundaries deliberately.
- RLS + least privilege are mandatory for persistence; grants/policies/security configuration are version-controlled and reviewable.
- Service-role credentials are server-only and never a shortcut around ordinary user RLS.
- `SECURITY INVOKER` is the default; `SECURITY DEFINER` only when narrow, justified and explicitly reviewed.
- Runtime validation is required at consequential server boundaries.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Vault secrets never appear in browser storage, logs, search, notifications, analytics or non-Vault surfaces.
- QR only signed/scoped/short-lived references; never raw secrets.
- Consequential mutations eventually use an Action Registry/equivalent audited boundary.
- Sensitive auth/database/provider values and raw privileged error objects are not logged or surfaced.
- No security vulnerability exceptions are accepted.

## SECURITY-GATE-001
**ACCEPTED / CLOSED**
Canonical security-sensitive package facts:
- `@tanstack/react-router ^1.170.18`
- `@tanstack/react-start ^1.168.32`
- `@tanstack/router-plugin ^1.168.23`
- `@tanstack/react-table 8.20.5`
- `@supabase/supabase-js ^2.112.2`
- `@supabase/ssr ^0.12.4`
- top-level override `"js-yaml": "4.3.1"`
- no accepted High/Critical finding.

## FOUND-001A/B/C/D/E
**ACCEPTED / CANONICAL / FROZEN / CLOSED**
Foundation, Core UI, Admin shell and Client Portal shell remain frozen. `/admin` is the staff shell. `/`, `/properties`, `/projects`, `/support`, `/billing` share the client Portal shell. Reopen only for a concrete regression.

## FOUND-001F0 — Identity / Auth Architecture
**ACCEPTED / CANONICAL**
Canonical identity primitives remain distinct: Auth User, Profile, Organisation, Organisation Membership, Staff Access.

Surface direction:
- `/admin` eventually requires authenticated active staff access.
- Portal eventually requires authenticated active organisation membership.
- exactly one active membership => automatic organisation context;
- multiple active memberships => explicit organisation selection before organisation-scoped Portal work;
- active-org selection is context only, never authorization evidence;
- invite-oriented email/password foundation, MFA-ready; enterprise SSO deferred;
- a user may be staff, organisation member, both, or a member of multiple organisations.

## FOUND-001F1A — Lovable Cloud + Auth Transport
**ACCEPTED / CANONICAL / FROZEN**
- Lovable Cloud/Supabase is activated and connected.
- generated `src/integrations/supabase/**` remains generated infrastructure.
- canonical Re:Solve auth uses cookie-backed `@supabase/ssr` browser/server session state for SSR initial requests.
- request-scoped server clients validate identity with `getClaims()`.
- generated bearer serverFn transport remains an accepted separate stateless path.
- generated `supabaseAdmin` is PRESENT / GENERATED / QUARANTINED / UNUSED by application code.
- `src/start.ts` preserves error middleware + explicit CSRF middleware + generated auth attacher.

## FOUND-001F1B — User-Facing Authentication Flows
**ACCEPTED / CANONICAL / FROZEN**
Canonical auth UX includes `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`; canonical browser sign-in/reset actions; request-scoped server sign-out; server-side PKCE exchange into cookie state; safe internal redirects; provider-neutral errors; no public signup; and no staff/org authorization assumptions.

F1B authenticates identity only. It does not determine what the authenticated user may access.

## FOUND-001F2A — Minimal Identity Schema + Baseline RLS
**ACCEPTED / CANONICAL / FROZEN**

Canonical migrations:
- `supabase/migrations/20260809051520_identity_foundation.sql`
- `supabase/migrations/20260809052255_identity_grants_closure.sql`

Canonical schema contains only:
- `public.profiles` — own human-facing profile, 1:1 to `auth.users`;
- `public.organisations` — minimal organisation identity;
- `public.organisation_memberships` — authoritative user↔organisation relationship, `active | suspended`, unique `(organisation_id,user_id)`;
- `public.staff_members` — independent internal staff-access fact, `active | suspended`.

RLS/grants:
- profiles: own SELECT/INSERT/UPDATE; authenticated INSERT limited to `id,display_name,avatar_url`, UPDATE limited to `display_name,avatar_url`;
- memberships: own SELECT only;
- organisations: SELECT only through active membership;
- staff: own SELECT only;
- anon/PUBLIC: no privileges;
- service_role: privileged database role retained, generated application service-role client remains quarantined/unused;
- no recursive policy path; no `SECURITY DEFINER`; no seed identities; no automatic profile trigger; no roles/capabilities; no domain tables.

F2A is frozen. Do not alter schema, grants or policies without a concrete supervised requirement.

## FOUND-001F2B — Server-Owned Identity Read Primitives
**CONDITIONAL — READ ARCHITECTURE ACCEPTED; RAW ERROR LOGGING + ACTIVE-ORGANISATION CONSISTENCY MUST CLOSE**

Verified files:
- `src/lib/identity/identity.server.ts`
- `src/lib/identity/identity.functions.ts`

Verified-good architecture:
- internal server-only `readCurrentIdentity()` starts from real `getAuthenticatedUser()`;
- all profile/staff/membership/organisation reads use the caller-scoped Supabase client, so RLS remains active;
- no service role or `supabaseAdmin` use;
- public `getCurrentIdentity` is one read-only GET server function;
- unauthenticated state is distinct from authenticated-with-no-access state;
- missing profile/staff/memberships are valid absence states;
- staff status preserves absent vs active vs suspended and exposes server-derived `isActive`;
- membership status is runtime-narrowed with Zod to `active | suspended`;
- suspended memberships remain in the snapshot but do not resolve organisation details;
- multiple active memberships are all returned with no active-org persistence or automatic selection;
- staff + organisation membership may coexist;
- no route guards, UI, writes, migrations, RBAC or dependency changes were introduced.

Canonical snapshot shape is directionally accepted:
- `authenticated` discriminator;
- authenticated user `{ id, email }`;
- nullable profile `{ id, displayName, avatarUrl }`;
- nullable staff `{ status, isActive }`;
- own membership list `{ id, organisationId, status }[]`;
- active organisation list `{ id, name, membershipId }[]` resolved through RLS.

### Blocking error-hygiene issue
`identity.server.ts` currently converts Supabase query errors into `Error` objects containing raw provider/PostgREST `.message` text and then logs the caught raw error object with `console.error(..., err)` before throwing the stable outward error `Internal identity read failure`.

This violates the intended boundary: provider/database error objects/messages must not be surfaced or logged raw at the identity/security layer. The outward failure is stable, but the server log still contains raw details.

Required closure:
- do not embed Supabase/PostgREST messages into thrown errors;
- do not log the caught raw error/Zod/provider object;
- expected implementation may log only a fixed non-sensitive event label, or omit logging entirely;
- continue throwing one stable internal identity-read failure for query/status/integrity failures.

### Blocking active-organisation consistency issue
For active memberships, organisation rows are resolved through the same RLS client. Current code safely avoids service-role bypass, but if one or more active memberships unexpectedly fail to resolve to organisation rows, it silently returns a smaller `activeOrganisations` array.

Because the FK and active-membership RLS policy should make those rows resolvable, a missing organisation here indicates data/policy inconsistency. Future F3 must not receive an apparently-normal partial snapshot.

Required closure:
- compare the expected active organisation IDs from active memberships with the organisation IDs actually returned;
- if any expected active organisation is missing, fail the entire identity read closed with the same stable internal error;
- never use service role to recover missing organisation data;
- do not expose raw IDs/error objects in logs.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- `/ui` remains dev-only gallery.
- Admin and Portal shells remain frozen.
- Lovable Cloud/Supabase is active.
- F1 auth transport + UX are frozen.
- F2A identity persistence/RLS/grants are frozen.
- F2B read infrastructure exists but is not frozen until error hygiene and active-org consistency close.
- No Admin/Portal route authorization, active-organisation selector, invitation/onboarding flow, domain tables or broad RBAC exists yet.

## Next action
Run one narrow **FOUND-001F2B-FIX — Identity Read Fail-Closed Closure**. Change only the identity read module as needed to remove raw provider/database error logging/messages and make unresolved active memberships fail the full identity snapshot closed. Do not modify auth, database, routes, UI, generated integrations or packages. If clean, freeze F2B and proceed to F3 server-authoritative surface authorization in small slices.