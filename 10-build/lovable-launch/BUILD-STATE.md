# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B NEXT**

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

Re:Solve-owned auth boundaries under `src/lib/supabase/`:
- `client.ts` exposes the generated tooling client separately from canonical `supabaseAuthBrowser` built with `createBrowserClient`.
- `server.ts` provides request-scoped bearer clients and `getAuthenticatedUser()` with bearer-first then cookie fallback.
- `session.ts` provides request-scoped cookie-backed `createServerClient` using TanStack `getCookies()` / `setCookie()` and validated `getClaims()` identity.

Canonical dual-transport model:
1. **Cookie-backed SSR session** — canonical Re:Solve browser/server auth session, available on initial server requests and future route boundaries.
2. **Bearer serverFn transport** — retained generated Lovable path for stateless server-function RPCs.

Cookie policy closure:
- Supabase-managed auth cookies are **not** forcibly `HttpOnly`; browser `createBrowserClient` can share the session as required by `@supabase/ssr`.
- Supabase-provided cookie attributes are preserved; safe fallbacks apply only for `SameSite=Lax`, production `Secure`, and `Path=/` when absent.
- library-provided expiry/max-age attributes are not replaced.
- installed `@supabase/ssr 0.12.4` `setAll(cookies, headers)` cache directives are forwarded through TanStack `setResponseHeader`, preserving private/no-cache/no-store/must-revalidate/max-age=0 behavior on token rotation.
- authenticated identity is validated with `getClaims()`, not trusted from raw `getSession()` user state.
- no route guards, identity tables, organisation/staff authorization, domain RLS or login UI exist yet.

F1A is frozen. Do not reopen transport unless a concrete auth/session regression is demonstrated.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- `/ui` remains dev-only gallery.
- Admin and Portal shells remain frozen.
- Lovable Cloud/Supabase is active.
- Secure dual auth transport is established.
- No application identity schema/RLS/surface authorization yet.

## Next action
Begin **FOUND-001F1B — User-Facing Authentication Flows** as a small slice. Build invite-oriented sign-in, sign-out, forgot/reset password and required auth callback/session-expiry surfaces using the canonical Re:Solve cookie-backed auth client established in F1A. Do not create profiles, organisations, memberships, staff records, domain RLS, active-organisation selection or Admin/Portal staff/org authorization yet; those remain F2/F3. Preserve the frozen Admin/Portal visual foundations and generated Lovable integration files.