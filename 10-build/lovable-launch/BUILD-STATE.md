# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN — FOUND-001F2A IDENTITY SCHEMA + BASELINE RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B NEXT**

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
- Sensitive values/tokens/secrets are not logged.
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

### Canonical migrations
`supabase/migrations/20260809051520_identity_foundation.sql`
- creates only `organisations`, `profiles`, `organisation_memberships`, `staff_members`;
- enables RLS on all four;
- creates the baseline policies.

`supabase/migrations/20260809052255_identity_grants_closure.sql`
- restores the already-applied Cloud grant closure to canonical source control;
- revokes all privileges on all four identity tables from `anon`, `authenticated`, and `PUBLIC` before re-granting;
- then applies the explicit least-privilege matrix;
- explicitly leaves `service_role` privileged for backend bypass, while application use remains quarantined.

The original foundation migration is preserved unchanged in migration history. The grant-closure migration is now present on canonical app `main`; no additional Cloud migration was applied during source reconciliation.

### Canonical identity schema
`public.profiles`
- `id uuid primary key -> auth.users(id) on delete cascade`
- `display_name text null`
- `avatar_url text null`
- `created_at timestamptz not null default now()`

`public.organisations`
- `id uuid primary key default gen_random_uuid()`
- `name text not null`
- `created_at timestamptz not null default now()`

`public.organisation_memberships`
- UUID primary key;
- organisation FK + user FK, both cascade on delete;
- status constrained to `active | suspended`;
- unique `(organisation_id, user_id)`;
- indexes on `user_id` and `organisation_id`.

`public.staff_members`
- `user_id` primary key -> `auth.users(id)`;
- status constrained to `active | suspended`;
- created timestamp.

No automatic auth-user profile trigger, invitation table, active-org column, role/capability catalogue, domain tables or seed users exist yet.

### Canonical RLS
- `profiles`: own-row SELECT, INSERT and UPDATE only; no DELETE policy.
- `organisation_memberships`: own-row SELECT only.
- `organisations`: SELECT only where `auth.uid()` has an `active` membership for that organisation.
- `staff_members`: own-row SELECT only.
- no anon policies.
- no recursive policy path.
- zero `SECURITY DEFINER` helpers.

### Canonical grants
`anon`
- NONE on all four identity tables.

`authenticated.profiles`
- SELECT all columns allowed by RLS;
- INSERT only `id`, `display_name`, `avatar_url`;
- UPDATE only `display_name`, `avatar_url`;
- no DELETE.

`authenticated.organisations`
- SELECT only.

`authenticated.organisation_memberships`
- SELECT only.

`authenticated.staff_members`
- SELECT only.

`PUBLIC`
- no table privileges on these identity tables.

`service_role`
- explicit privileged backend table access retained at the database role layer;
- generated service-role application client remains quarantined/unused.

### Generated types
`src/integrations/supabase/types.ts` contains all four public tables with expected nullability and public FK relationship metadata.

### Source-hygiene note
The already-applied foundation migration contains one historical build-slice comment. Do not rewrite migration history solely to remove it. Future migrations use database-purpose comments only.

F2A is frozen. Do not alter the identity schema, policies or grants without a concrete requirement and supervised migration review.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- `/ui` remains dev-only gallery.
- Admin and Portal shells remain frozen.
- Lovable Cloud/Supabase is active.
- F1 auth transport + UX are frozen.
- Minimal identity persistence + baseline RLS + deterministic grants are frozen.
- No Admin/Portal route authorization, active-organisation selector, invitation/onboarding flow, domain tables or broad RBAC exists yet.

## Next action
Begin **FOUND-001F2B — Server-Owned Identity Read Primitives**. Add a small server-only/read-only application boundary that starts from validated authenticated identity and reads the caller's own Profile, Staff Access and Organisation Memberships through the caller-scoped Supabase client/RLS. It should expose enough typed information for future F3 route authorization without adding route guards, UI wiring, writes, service-role usage, active-org persistence or new database objects.