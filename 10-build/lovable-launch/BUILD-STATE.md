# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN — FOUND-001F2A IDENTITY SCHEMA + BASELINE RLS NEXT**

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
- `.env` / `.env.*` remain ignored except `.env.example`.
- canonical cookie-backed SSR session uses `@supabase/ssr`, request-scoped server clients, shared browser/server cookie state, Supabase-provided cache directives, and validated `getClaims()` identity.
- bearer serverFn transport remains a separate accepted stateless path.

F1A is frozen. Do not reopen transport without a concrete auth/session regression.

## FOUND-001F1B — User-Facing Authentication Flows
**ACCEPTED / CANONICAL / FROZEN**
Canonical auth UX now includes:
- `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`;
- shared auth components under `src/components/auth/`;
- login via canonical `supabaseAuthBrowser.auth.signInWithPassword()` with RHF/Zod validation and no public signup;
- already-authenticated `/login` requests redirect to `/` based only on authenticated identity, with no staff/org assumption;
- forgot-password uses neutral account-enumeration-safe success copy;
- reset-password uses canonical browser auth client and stable provider-neutral failure copy;
- reusable server-side `signOut` uses the request-scoped cookie-backed client;
- shared `getSafeRedirect()` permits internal application paths only and rejects protocol-relative/external targets;
- PKCE callback code exchange now runs through a server function backed by `createSsrSessionSupabase()`, so the resulting session is written into canonical HTTP cookies before redirect;
- recovery callbacks redirect to `/reset-password`; general callbacks use safe internal redirects;
- raw Supabase/AuthError objects, auth codes, tokens, sessions and password values are not logged or exposed to UI;
- generated `src/integrations/supabase/**`, `src/start.ts`, CSRF, bearer middleware and service-role quarantine remain unchanged;
- no profiles, organisations, memberships, staff records, RLS domain policies, MFA, invitations, organisation selection or Admin/Portal authorization were introduced.

F1B authenticates identity only. It does not determine what the authenticated user is allowed to access.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- `/ui` remains dev-only gallery.
- Admin and Portal shells remain frozen.
- Lovable Cloud/Supabase is active.
- Cookie-backed SSR auth + bearer serverFn transport are frozen.
- User-facing sign-in/password-recovery flows are frozen.
- No application identity schema/RLS/surface authorization exists yet.

## Next action
Begin **FOUND-001F2A — Minimal Identity Schema + Baseline RLS**. Introduce only the canonical identity records required by F0: profiles, organisations, organisation memberships and staff access. Create them through version-controlled Supabase migrations, enable RLS in the same slice, grant only the minimum self-readable/self-profile permissions required for future F3 access checks, regenerate database types, and do not wire UI or route guards yet. Do not create invitations, domain tables, broad RBAC/capability catalogues, organisation switcher, demo users or service-role application flows in F2A.