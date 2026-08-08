# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 IDENTITY/AUTH PREFLIGHT ACCEPTED/CANONICAL — FOUND-001F1A CLOUD ACTIVATION CONDITIONAL / SSR COOKIE CLOSURE NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — specification/planning source.
- Current app: `thathman/re-solve-c560d62c` — canonical Lovable development app on `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Security memory
**ACCEPTED / CANONICAL**
- Roles, permissions and capability decisions are server-controlled; browser/client metadata is never authoritative for authorization.
- Authentication and authorization are enforced at server-function/server-route boundaries, not only in UI or client navigation.
- Never invent security helpers that do not exist; inspect and extend real server boundaries deliberately.
- RLS and least privilege are mandatory when persistence is introduced; grants/policies/security configuration are version-controlled and reviewable.
- Service-role credentials and privileged backend secrets are server-only and must never ship in client bundles.
- `SECURITY INVOKER` is the default; `SECURITY DEFINER` must remain narrow, justified and explicitly reviewed.
- Runtime validation is required at consequential server boundaries.
- Preserve `createCsrfMiddleware` in `src/start.ts`.
- Vault secrets never appear in browser storage, logs, search results, notifications, analytics, non-Vault surfaces or ordinary client caches.
- QR codes expose only signed, scoped, short-lived references/tokens; never raw secrets or durable privileged credentials.
- Consequential mutations should eventually route through an Action Registry/equivalent audited mutation boundary.
- Sensitive values, auth tokens, secret payloads and privileged identifiers are not written to application logs or error telemetry.
- No security vulnerability exceptions are accepted.

## SECURITY-GATE-001 — Dependency remediation
**ACCEPTED / CLOSED**
Canonical package state before auth activation:
- `@tanstack/react-router`: `^1.170.18`
- `@tanstack/react-start`: `^1.168.32`
- `@tanstack/router-plugin`: `^1.168.23`
- `@tanstack/react-table`: `8.20.5`
- no direct `@tanstack/router-core`
- no direct `js-yaml`
- top-level Bun override: `"js-yaml": "4.3.1"`
- no accepted High/Critical security finding.

Auth activation may add approved Supabase dependencies only after explicit supervised review; unrelated dependency upgrades remain prohibited.

## Currency display convention
**CANONICAL**
- Currency identity remains explicit via ISO codes in data/API contracts.
- Normal user-facing UI uses locale-appropriate symbols where unambiguous.
- There is no universal default currency.

## FOUND-001A/B — Foundation and design system
**ACCEPTED / CLOSED**
Canonical foundation includes TanStack Start + React 19, Bun, Tailwind v4, semantic OKLCH tokens, light/dark/system themes, Inter + JetBrains Mono, responsive spacing/shell reservations, frozen focus variables, environment/server-only boundaries, UI provenance, `/ui` development gallery with production redirect, and self-hostability/no required Lovable runtime dependency.

## FOUND-001C — Core UI Framework
**ACCEPTED / CANONICAL / FROZEN / CLOSED**
Canonical Core includes actions, forms, overlays/disclosure, feedback/composition, advanced inputs/date, display/layout, generic TanStack DataTable, Sidebar family, and NavigationMenu family. Do not reopen Core absent a concrete regression or a later requirement proving a genuinely missing contract.

## FOUND-001D — Admin Shell
**ACCEPTED / CANONICAL / FROZEN / CLOSED**
Canonical Admin shell remains under `/admin` with route-aware Sidebar/TopBar/PageHeader/Breadcrumbs/Command/Àríyá composition, nine root Admin routes, Cmd/Ctrl+K Command/Search, anchored Notifications placeholder, shared right-side Àríyá Sheet placeholder, deterministic account/avatar placeholder actions, one primary main landmark and no auth/database/domain implementation. Final closure review passed with no blockers. Do not reopen without a concrete regression.

## FOUND-001E — Client Portal Shell
**ACCEPTED / CANONICAL / FROZEN / CLOSED**
Canonical Portal foundation includes:
- pathless `_portal` layout owning `/`, `/properties`, `/projects`, `/support`, `/billing`;
- horizontal Core NavigationMenu on desktop and Core Sheet mobile navigation;
- route-aware active links, Portal breadcrumbs and one shared Portal shell;
- shell-owned Command/Search with Cmd/Ctrl+K;
- anchored Notifications count `2`;
- shell-owned right-side `PortalAriyaPanel` sharing one `ariyaOpen` state across TopBar and Command;
- deterministic fictional Portal identity `Chinedu Okeke / Acme Properties Ltd.` pending real auth;
- canonical focus/gutter/token contracts and one main landmark;
- no business-domain data, real Notifications or AI backend.

FOUND-001E passed final closure review and is frozen.

## FOUND-001F0 — Identity / Authentication Architecture Preflight
**ACCEPTED / CANONICAL — READ-ONLY PREFLIGHT**

### Canonical identity primitives
Keep these distinct:
1. **Auth User** — authentication identity, ultimately Supabase `auth.users` UUID.
2. **Profile** — human-facing application data linked 1:1 to Auth User.
3. **Organisation** — client/business entity.
4. **Organisation Membership** — Auth/Profile user ↔ Organisation relationship with controlled status and later role/capability extension.
5. **Staff Access** — internal Re:Solve access boundary independent of client organisation membership.

Do not collapse these into one editable profile role string.

### Canonical surface authorization
- `/admin` requires authenticated staff access.
- Client Portal routes require authenticated active organisation membership.
- UI navigation and TanStack `beforeLoad` may improve UX but are never the authoritative authorization barrier.
- Server functions/routes must independently validate identity and access.
- Database RLS becomes the canonical final row-level barrier once persistence begins.

### Active organisation decision
- exactly one active membership: automatically use that organisation context;
- multiple active memberships: require an organisation choice before organisation-scoped Portal work;
- any persisted active-organisation selector is context/preferences only, never authorization evidence;
- server/RLS independently revalidates membership for the selected organisation.

### Authentication-method decision
- Initial Re:Solve auth is invite-oriented email/password with an MFA-ready architecture.
- SAML/OIDC/enterprise SSO is deferred until a concrete requirement exists.
- Do not expose unrestricted public self-signup unless later product policy explicitly enables it.

### Session direction
For TanStack Start SSR, Re:Solve requires a cookie-backed Supabase Auth session available to initial server rendering/route boundaries, plus validated server-side identity checks. Raw `getSession()` user data is not authoritative. Header-based bearer auth is acceptable for stateless server/API calls, but it does not replace the cookie session needed for initial SSR route authorization.

### RLS direction
- Least privilege, organisation-scoped policies, explicit membership checks.
- `SECURITY INVOKER` remains the default.
- `SECURITY DEFINER` is never the generic answer to RLS recursion; only a concrete narrowly-reviewed policy design may justify it later.

### Service-role direction
- Server-only.
- Never browser bundled.
- Never a shortcut around ordinary user RLS flows.
- Only use behind a justified privileged server boundary when later requirements demand it.

## FOUND-001F1A — Lovable Cloud Activation & Auth Transport
**CONDITIONAL — CLOUD ACTIVATION ACCEPTED; SSR SESSION CONTRACT NOT YET CLOSED**

### Verified-good activation evidence
- Lovable Cloud/Supabase is now connected and generated standard project integration files.
- `@supabase/supabase-js` is now present; no unrelated auth/session library was added.
- env naming was normalized away from the old `VITE_SUPABASE_ANON_KEY` toward publishable-key naming.
- generated project integration includes browser client, server/admin client, bearer auth middleware/attacher, generated types and `supabase/config.toml`.
- Re:Solve wrappers exist under `src/lib/supabase/`.
- `src/start.ts` preserves the existing error middleware and explicit `createCsrfMiddleware`, while Cloud activation added generated Supabase function middleware registration.
- `.env` / `.env.*` remain ignored while `.env.example` is allowed.
- no identity tables, organisation/member schema, route guards or domain RLS were introduced.
- package override `"js-yaml": "4.3.1"` remains canonical.

### Generated bearer transport — accepted only for server functions/APIs
Lovable generated:
- a browser client whose session persists in browser `localStorage`;
- a client-side `functionMiddleware` that calls `supabase.auth.getSession()` only to obtain the access token and attach `Authorization: Bearer <jwt>` to TanStack server-function RPCs;
- server-side generated auth middleware that validates bearer JWTs via `auth.getClaims()` and builds a caller-scoped Supabase client respecting RLS.

This is a valid stateless bearer transport for server functions/API-style calls. It is **not** sufficient as Re:Solve's sole SSR session architecture because the initial browser request for `/admin` or Portal routes does not yet carry that client-injected bearer header. Future server-authoritative route protection therefore still requires a cookie-backed SSR session boundary.

### Re:Solve server wrapper
`src/lib/supabase/server.ts` currently:
- creates request-scoped anonymous/user clients rather than caching user clients;
- reads bearer access tokens from the current request where present;
- validates identity with `auth.getClaims()` rather than trusting a raw session user object;
- carries no staff/organisation/membership authorization yet.

This is acceptable for bearer-authenticated server functions but must not be treated as the final route/SSR session boundary.

### Privileged generated client quarantine
Cloud activation generated `src/integrations/supabase/client.server.ts` with a `supabaseAdmin` service-role client that bypasses RLS.

Canonical treatment:
- the generated file may remain because it is part of Cloud tooling;
- application code must not import/use `supabaseAdmin` in ordinary auth, Portal or Admin flows;
- generated service-role presence does not authorize service-role usage;
- later privileged use requires an explicit supervised server-only requirement and review;
- never expose its credential or client to browser code.

### F1A blockers to closure
1. **SSR cookie session is missing.** Current generated session storage is browser-local and bearer attachment occurs only after browser execution. Re:Solve still needs a request-visible cookie-backed session so initial SSR/server route boundaries can validate identity.
2. **Do not misclassify the generated bearer pipeline as SSR cookie auth.** Preserve it for serverFn/API transport if useful, but add the separate SSR session lifecycle required by the canonical architecture.
3. **Do not edit generated `src/integrations/supabase/**` files.** Build Re:Solve-owned cookie/session adapters under `src/lib/supabase/**` and minimum TanStack request middleware/routes using current supported APIs.

### External primary-source alignment
Current Supabase guidance distinguishes the auth transports:
- SSR frameworks such as TanStack Start use cookie-backed sessions, typically via `@supabase/ssr`;
- header-based `Authorization: Bearer <jwt>` is a stateless server/API model;
- `getClaims()` is appropriate for validated identity checks, while the user object returned from raw `getSession()` should not be trusted for authorization.

The Re:Solve closure should support SSR cookie identity without discarding the generated bearer transport.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- TanStack React Table `8.20.5` is canonical.
- `/ui` is development/Lovable gallery and redirects to `/` in production.
- `/admin` is the frozen staff/admin application shell.
- `/`, `/properties`, `/projects`, `/support`, `/billing` share the frozen client-facing Portal shell.
- Lovable Cloud/Supabase is now activated.
- No Re:Solve application identity tables/RLS/surface authorization are implemented yet.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Client Portal is calmer and less dense than Admin while remaining clearly Re:Solve.
- Àríyá is Re:Solve's built-in AI surface; Chatwoot keeps Captain separately.
- shadcn-vue is visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Run FOUND-001F1A-FIX as a narrow auth-transport closure. Keep Lovable-generated bearer/serverFn integration intact and unedited, quarantine the generated service-role client from ordinary app usage, and add a Re:Solve-owned cookie-backed SSR Supabase session boundary using current supported TanStack Start + Supabase APIs. Prove the authenticated identity can be validated on an initial server request without relying on browser localStorage or client-injected Authorization headers. Do not add login UI, identity schema, RLS domain policies, staff/org authorization or route guards yet.