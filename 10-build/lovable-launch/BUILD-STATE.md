# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN — FOUND-001F2A IDENTITY SCHEMA/RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS ACCEPTED/CANONICAL/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval

## Security memory
**ACCEPTED / CANONICAL**
- Authentication, roles, permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route guards are UX gates only. Every future server function/server route returning private data must authorize independently at its own server boundary.
- RLS + least privilege are mandatory for persistence; grants/policies/security configuration are version-controlled.
- Caller-scoped Supabase clients + explicit filters + RLS are the normal user-data path.
- Generated `supabaseAdmin`/service-role client is PRESENT / GENERATED / QUARANTINED / UNUSED by Re:Solve application code.
- `SECURITY INVOKER` default; `SECURITY DEFINER` requires narrow, explicit review.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- Vault secrets never appear in browser storage, search, notifications, logs, analytics or non-Vault surfaces.
- QR only signed/scoped/short-lived references, never raw secrets.
- Consequential mutations eventually use an Action Registry/equivalent audited mutation boundary.
- No security vulnerability exceptions accepted.

## Frozen foundation / Core / shells
**ACCEPTED / CANONICAL / FROZEN / CLOSED**
- Foundation + Core UI phases C1-C5E remain frozen.
- `/ui` remains the dev-only Core gallery.
- Admin shell lives under `/admin` and currently contains Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Client Portal shell covers `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Shells may only reopen for concrete regression or a separately supervised visual-system rollout.

## SECURITY-GATE-001
**ACCEPTED / CLOSED**
- `@tanstack/react-router ^1.170.18`
- `@tanstack/react-start ^1.168.32`
- `@tanstack/router-plugin ^1.168.23`
- `@tanstack/react-table 8.20.5`
- `@supabase/supabase-js ^2.112.2`
- `@supabase/ssr ^0.12.4`
- top-level `"overrides": { "js-yaml": "4.3.1" }`

## FOUND-001F0 — Identity / Auth Architecture
**ACCEPTED / CANONICAL**
Canonical identity facts are distinct:
- Auth User (`auth.users`)
- Profile
- Organisation
- Organisation Membership
- Staff Access

Surface direction:
- `/admin` requires authenticated **active staff** access.
- Portal requires authenticated **active organisation membership**.
- one active membership may become automatic org context;
- multiple active memberships require explicit selection before org-scoped Portal work;
- selected org is context only, never authorization evidence;
- a user may be staff, organisation member, both, or member of multiple organisations.

## FOUND-001F1A — Auth transport
**ACCEPTED / CANONICAL / FROZEN**
- Lovable Cloud/Supabase active.
- Canonical Re:Solve browser/server auth is shared cookie-backed `@supabase/ssr` session state.
- Initial SSR identity is validated with `getClaims()` through a request-scoped server client.
- Generated bearer serverFn transport remains available as a separate stateless path.
- PKCE/session cookie handling preserves Supabase-provided cookie options and refresh cache directives.
- `src/start.ts` preserves error middleware, generated auth attacher and explicit CSRF middleware.

## FOUND-001F1B — User-facing auth
**ACCEPTED / CANONICAL / FROZEN**
Routes:
- `/login`
- `/forgot-password`
- `/reset-password`
- `/auth/callback`

Canonical behavior:
- invite-oriented email/password; no public signup/social login/MFA yet;
- login uses canonical `supabaseAuthBrowser`;
- PKCE exchange is server-side through the cookie-backed request client;
- forgot-password messaging is account-enumeration-safe;
- reset errors are provider-neutral;
- safe internal redirects only;
- reusable server-side sign-out exists;
- F1 authenticates identity only; it does not authorize Admin/Portal access.

## FOUND-001F2A — Identity schema + baseline RLS
**ACCEPTED / CANONICAL / FROZEN**
Canonical migrations:
- `supabase/migrations/20260809051520_identity_foundation.sql`
- `supabase/migrations/20260809052255_identity_grants_closure.sql`

Tables:
- `profiles(id -> auth.users, display_name, avatar_url, created_at)`
- `organisations(id, name, created_at)`
- `organisation_memberships(id, organisation_id, user_id, status active|suspended, created_at)` with unique `(organisation_id,user_id)`
- `staff_members(user_id, status active|suspended, created_at)`

Canonical RLS/grants:
- profiles: own SELECT/INSERT/UPDATE; column-level browser mutation only for `id/display_name/avatar_url` on insert and `display_name/avatar_url` on update;
- memberships: own SELECT only;
- organisations: SELECT only through active membership;
- staff: own SELECT only;
- anon/PUBLIC: no privileges;
- service_role database role remains privileged, but application client is quarantined/unused;
- no recursive policy chain; no `SECURITY DEFINER`; no seed identities; no automatic profile trigger; no roles/capabilities/domain tables.

## FOUND-001F2B — Server-owned identity reads
**ACCEPTED / CANONICAL / FROZEN**
Verified files:
- `src/lib/identity/identity.server.ts`
- `src/lib/identity/identity.functions.ts`

Canonical implementation:
- internal `readCurrentIdentity()` starts from real `getAuthenticatedUser()`;
- all identity-table reads use the caller-scoped Supabase client and therefore RLS;
- public `getCurrentIdentity` is one read-only GET server function;
- no service-role use, writes, route guards, UI, migrations, RBAC or dependency changes.

Canonical snapshot distinguishes:
- unauthenticated;
- authenticated user `{ id, email }`;
- nullable profile;
- staff absent vs `active` vs `suspended`, with server-derived `isActive`;
- all own memberships with runtime-validated `active|suspended` status;
- active organisations `{ id, name, membershipId }[]` resolved only through caller-scoped RLS.

Fail-closed invariants:
- raw Supabase/PostgREST/Zod/provider error details are neither logged nor surfaced;
- query/status failures throw one stable `Internal identity read failure`;
- suspended memberships never resolve organisation details or grant active org access;
- every active membership must resolve to its organisation through RLS before the snapshot succeeds;
- missing/inconsistent active organisation resolution fails the entire snapshot closed;
- zero memberships/profile/staff remain valid absence states;
- no automatic active-organisation selection or persistence exists.

F2B is frozen. Do not reopen identity-read behavior without a concrete regression or new authorization requirement.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth transport, auth UX, identity persistence/RLS/grants and identity reads are now frozen.
- No Admin/Portal authorization is active yet.
- No active-organisation selector, invitation/onboarding flow, domain tables or broad RBAC exists yet.

## Next action
Begin **FOUND-001F3A — Server-Authoritative Admin Access** only. Protect the `/admin` route family so unauthenticated users go to `/login` with safe return-to context, authenticated users without an active `staff_members` record cannot enter Admin, and active staff can enter. Build the reusable server-owned active-staff authorization primitive that future private Admin server functions can invoke at their own server boundaries. Treat route `beforeLoad` as UX gating, not the private-data authorization boundary. Do not touch Portal authorization, organisation selection, database schema/RLS, invitations, RBAC, or the broader visual redesign in F3A.