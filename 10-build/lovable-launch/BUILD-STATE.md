# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN — FOUND-001F2A IDENTITY SCHEMA + BASELINE RLS CONDITIONAL / GRANT CLOSURE APPLIED IN CLOUD BUT MIGRATION MISSING FROM MAIN**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`.
- Current app: `thathman/re-solve-c560d62c` on `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit owner approval.

## Security memory
**ACCEPTED / CANONICAL**
- Roles/permissions/capabilities are server-controlled; browser metadata is never authoritative.
- Auth/authz is enforced at server-function/server-route boundaries and later by RLS, not only UI navigation.
- Never invent helpers that do not exist.
- RLS + least privilege when persistence begins; grants/policies/security config version-controlled.
- Service-role credentials are server-only and never a shortcut around normal user RLS.
- `SECURITY INVOKER` default; `SECURITY DEFINER` only narrow, justified, explicitly reviewed.
- Runtime validation at consequential server boundaries.
- Preserve `createCsrfMiddleware` in `src/start.ts`.
- Vault secrets never browser storage/log/search/notifications/analytics/non-Vault surfaces.
- QR only signed/scoped/short-lived references, never raw secrets.
- Consequential mutations eventually use Action Registry/equivalent audited boundary.
- Sensitive values/tokens/secrets are not logged.
- No vulnerability exceptions accepted.

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
- `/admin` eventually requires authenticated staff access.
- Portal eventually requires authenticated active organisation membership.
- one membership => automatic org context; multiple memberships => explicit selection;
- active-org context is never authorization evidence;
- invite-oriented email/password foundation, MFA-ready; enterprise SSO deferred;
- Supabase Auth remains portable across Lovable Cloud, managed Supabase and self-hosted Supabase.

## FOUND-001F1A — Lovable Cloud + Auth Transport
**ACCEPTED / CANONICAL / FROZEN**
Canonical F1A state:
- Lovable Cloud/Supabase is activated and connected.
- generated `src/integrations/supabase/**` and `supabase/config.toml` remain generated infrastructure and are not hand-edited.
- env contract uses publishable-key naming; old `VITE_SUPABASE_ANON_KEY` is removed.
- generated bearer serverFn transport remains intact: browser-generated client obtains the access token, `attachSupabaseAuth` forwards `Authorization: Bearer`, and generated server middleware validates with `auth.getClaims()`.
- generated `supabaseAdmin` service-role client is PRESENT / GENERATED / QUARANTINED / UNUSED by Re:Solve application code.
- `src/start.ts` preserves error middleware + explicit `createCsrfMiddleware`; generated `attachSupabaseAuth` remains registered as function middleware.
- canonical cookie-backed SSR session uses `@supabase/ssr`, request-scoped server clients, shared browser/server cookie state, Supabase-provided cache directives, and validated `getClaims()` identity.
- bearer serverFn transport remains a separate accepted stateless path.

F1A is frozen. Do not reopen transport without a concrete auth/session regression.

## FOUND-001F1B — User-Facing Authentication Flows
**ACCEPTED / CANONICAL / FROZEN**
Canonical auth UX includes `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`; canonical browser sign-in/reset actions; request-scoped server sign-out; server-side PKCE code exchange into cookie session state; safe internal redirects; provider-neutral errors; no public signup; and no staff/org authorization assumptions. Generated Supabase integration, CSRF, bearer transport and service-role quarantine remain unchanged.

F1B authenticates identity only. It does not determine what the authenticated user may access.

## FOUND-001F2A — Minimal Identity Schema + Baseline RLS
**CONDITIONAL — SCHEMA/POLICIES ACCEPTED; CLOUD GRANT CLOSURE REPORTED CORRECT BUT VERSION-CONTROLLED CLOSURE MIGRATION IS MISSING FROM `main`**

### Verified schema
Version-controlled migration:
`supabase/migrations/20260809051520_identity_foundation.sql`

Creates only:
- `public.organisations(id, name, created_at)`;
- `public.profiles(id -> auth.users, display_name, avatar_url, created_at)`;
- `public.organisation_memberships(id, organisation_id -> organisations, user_id -> auth.users, status, created_at)` with unique `(organisation_id, user_id)` and indexes on user/org;
- `public.staff_members(user_id -> auth.users, status, created_at)`.

Membership/staff statuses are constrained to `active | suspended`. User relationships remain independent: a user may be staff, organisation member, both, or member of multiple organisations.

### Verified RLS policy shape
RLS is enabled on all four public tables.
- profiles: authenticated own-row SELECT, own-row INSERT, own-row UPDATE; no DELETE policy;
- organisation_memberships: authenticated own-row SELECT only;
- organisations: authenticated SELECT only where an active membership for `auth.uid()` exists;
- staff_members: authenticated own-row SELECT only.

Policy dependency is non-recursive: organisation policy reads membership; membership policy depends only on `user_id = auth.uid()`. No `SECURITY DEFINER` function exists. No seed identities/data or onboarding trigger exists.

### Generated types
`src/integrations/supabase/types.ts` contains all four tables with the expected public relationships/nullability.

### Reported Cloud grant closure
Lovable reports that migration `20260809052255_identity_grants_closure.sql` was applied successfully to the connected development project and produced the intended deterministic privilege matrix:
- `anon`: no privileges on all four tables;
- `authenticated.profiles`: SELECT, INSERT only `(id, display_name, avatar_url)`, UPDATE only `(display_name, avatar_url)`, no DELETE;
- `authenticated.organisations`: SELECT only;
- `authenticated.organisation_memberships`: SELECT only;
- `authenticated.staff_members`: SELECT only;
- `PUBLIC`: no meaningful DML privileges;
- `service_role`: privileged backend table access retained;
- generated `supabaseAdmin` remains quarantined/unused by application code.

### Blocking source-control mismatch
Direct canonical repository inspection of `thathman/re-solve-c560d62c` `main` cannot find:
`supabase/migrations/20260809052255_identity_grants_closure.sql`

Exact-path fetch returns 404 and repository code search finds no equivalent `REVOKE ALL PRIVILEGES` closure SQL. Therefore the Cloud privilege state is not currently reproducible from the canonical application repository.

This violates the canonical requirement that grants/policies/security configuration are version-controlled and reviewable. F2A cannot be frozen until the exact already-applied closure migration is present on `main`.

Do not invent a second/different migration or reapply SQL to Cloud merely to fix source control. Restore/commit the exact migration corresponding to the already-applied Cloud change, then verify it matches the reported privilege matrix.

### Source-hygiene residue
The already-applied identity-foundation migration contains a build-slice comment. Do not rewrite migration history solely to remove it. Future migrations must contain database-purpose comments only.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- `/ui` remains dev-only gallery.
- Admin and Portal shells remain frozen.
- Lovable Cloud/Supabase is active.
- F1 auth transport + UX are frozen.
- Four identity tables and baseline RLS exist in Cloud and source control.
- Deterministic least-privilege grant closure is reported applied in Cloud but is not yet represented in canonical `main` source control.
- No Admin/Portal route authorization, organisation selection, invitations, domain tables or broad RBAC exists yet.

## Next action
Run one source-control-only **FOUND-001F2A-FIX2**. Restore/commit the exact already-applied `20260809052255_identity_grants_closure.sql` migration to canonical app `main`, without changing or reapplying database state. Verify its SQL matches the reported revoke/regrant matrix, that the original migration remains untouched, and that no other files change. If present and correct on `main`, freeze F2A and proceed to F2B application identity read primitives.