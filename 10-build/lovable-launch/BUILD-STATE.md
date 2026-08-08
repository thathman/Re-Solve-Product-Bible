# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A CLOUD + SSR TRANSPORT CONDITIONAL / COOKIE-POLICY MICRO-FIX NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`.
- Current app: `thathman/re-solve-c560d62c` on `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit owner approval.

## Security memory
**ACCEPTED / CANONICAL**
- Roles/permissions/capabilities are server-controlled; browser metadata is never authoritative.
- Auth/authz is enforced at server-function/server-route boundaries and later by RLS, not only by UI navigation.
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
Canonical security-sensitive package facts remain:
- `@tanstack/react-router ^1.170.18`
- `@tanstack/react-start ^1.168.32`
- `@tanstack/router-plugin ^1.168.23`
- `@tanstack/react-table 8.20.5`
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
- Supabase Auth acceptable for Lovable Cloud, managed Supabase and self-hosted Supabase portability.

Session direction:
- SSR route identity must be available from cookies on the initial server request;
- validated `getClaims()`/equivalent is used for identity checks;
- raw `getSession()` user data is not authoritative;
- bearer auth remains acceptable for stateless server/API requests.

## FOUND-001F1A — Lovable Cloud + Auth Transport
**CONDITIONAL — ACTIVATION ACCEPTED; ONE SSR COOKIE-POLICY BLOCKER REMAINS**

### Accepted activation and transport facts
- Lovable Cloud/Supabase is activated and connected.
- generated `src/integrations/supabase/**` and `supabase/config.toml` exist and remain generated infrastructure.
- env contract uses publishable-key naming; old `VITE_SUPABASE_ANON_KEY` is gone.
- `@supabase/supabase-js` and `@supabase/ssr ^0.12.4` are present.
- `src/start.ts` still preserves error middleware + explicit `createCsrfMiddleware`; generated `attachSupabaseAuth` remains registered as `functionMiddleware`.
- generated bearer serverFn path is preserved: browser-generated client obtains the token, attaches `Authorization: Bearer`, and generated server middleware validates it with `auth.getClaims()`.
- generated `supabaseAdmin` service-role client is PRESENT / GENERATED / QUARANTINED / UNUSED by Re:Solve application code.
- `.env` / `.env.*` remain ignored except `.env.example`.
- no profiles/organisations/memberships/staff schema, domain RLS, login UI or Admin/Portal access guards exist yet.

### Re:Solve-owned SSR session implementation
`src/lib/supabase/` now contains:
- `client.ts`: generated tooling client plus a separate Re:Solve `createBrowserClient` auth client;
- `server.ts`: request-scoped bearer clients and `getAuthenticatedUser()` with bearer-first then cookie fallback;
- `session.ts`: request-scoped `createServerClient` using TanStack `getCookies()` / `setCookie()` and validated cookie-backed `getClaims()` identity probe.

This structurally closes the earlier initial-request gap: cookie state can be read by the server without browser localStorage or a client-injected Authorization header.

### Blocking cookie-policy issue
`src/lib/supabase/session.ts` currently forces every Supabase auth cookie written by `setAll()` to:

`httpOnly: true`

This is not compatible with the canonical `@supabase/ssr` shared browser/server session model. The browser-side `createBrowserClient` needs access to the auth/refresh cookies to maintain and refresh the same session. Current Supabase SSR guidance explicitly says HttpOnly is not required for these auth cookies and notes that the browser needs the refresh token.

Required closure:
- do **not** force `httpOnly: true` on Supabase-managed SSR auth cookies;
- preserve Supabase-provided cookie options and only supply safe defaults where the library has not already specified them;
- keep `SameSite=Lax`, `Secure` in production and `Path=/` where appropriate without overriding library-required attributes;
- inspect the installed `@supabase/ssr 0.12.4` `CookieMethodsServer.setAll` contract and preserve/apply any response cache headers it provides on token rotation; manual `private, no-store` may remain only if it does not overwrite stronger/more complete supplied headers;
- generated integration files stay untouched;
- bearer serverFn path stays intact;
- service-role client remains quarantined and unused.

### External primary-source alignment
Current Supabase guidance states:
- `@supabase/ssr` is the supported cookie-session package for SSR frameworks including TanStack Start;
- browser and server use shared cookie-backed session state;
- `getClaims()` is suitable for protected identity checks;
- HttpOnly is not appropriate for this shared JS SSR session because browser code must access the refresh token;
- responses that rotate auth cookies must not be publicly cached.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- `/ui` remains dev-only gallery.
- Admin and Portal shells remain frozen.
- Lovable Cloud/Supabase is active.
- Auth transport exists but F1A is not frozen until the SSR cookie-policy micro-fix closes.
- No application identity schema/RLS/surface authorization yet.

## Next action
Run one narrow **FOUND-001F1A-FIX2**: correct the Supabase SSR cookie options so they remain compatible with `createBrowserClient`, preserve any library-provided refresh cache headers, and re-verify the existing cookie/bearer dual transport. Do not add login UI, identity tables, RLS policies or route guards. If clean, freeze F1A and proceed to F1B user-facing auth flows.