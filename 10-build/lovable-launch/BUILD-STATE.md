# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 IDENTITY/AUTH PREFLIGHT ACCEPTED/CANONICAL — FOUND-001F1 NEXT**

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

### Verified repository facts
- No Supabase/Auth client package is currently declared in `package.json`; `@supabase/supabase-js`, `@supabase/ssr` and other auth/session libraries are absent.
- No repository migrations, generated database types, profile/membership/staff tables, RLS policies, auth routes, auth server functions or session helpers are evidenced.
- `src/start.ts` currently contains only the existing error middleware plus explicit `createCsrfMiddleware`; this security contract remains frozen.
- No `createServerFn` auth boundary currently exists.
- Supabase/Lovable environment **scaffolding is already partial**, not zero: `src/lib/env/index.ts` validates optional `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`, and `.env.example` documents them.
- Repository evidence does **not** prove whether a Lovable Cloud backend has been activated outside source control. Lovable Cloud connection status is therefore `UNKNOWN`, not canonically `ABSENT`, until Lovable Cloud/project evidence confirms it.
- Remote database/schema state is also `UNKNOWN`; what is canonically absent is repository migration/schema/type evidence.
- Local Supabase development infrastructure is absent; ordinary Bun/Vite local development does not itself constitute a database/auth local-development strategy.
- Current application code remains portable and has no required Lovable runtime dependency.

### Canonical identity primitives
Keep these distinct:
1. **Auth User** — authentication identity, ultimately Supabase `auth.users` UUID.
2. **Profile** — human-facing application data linked 1:1 to Auth User.
3. **Organisation** — client/business entity.
4. **Organisation Membership** — Auth/Profile user ↔ Organisation relationship with controlled status and later role/capability extension.
5. **Staff Access** — internal Re:Solve access boundary independent of client organisation membership.

Do not collapse these into one editable profile role string.

### Canonical surface authorization
- `/admin` requires authenticated **staff access**.
- Client Portal routes require authenticated **active organisation membership**.
- UI navigation and TanStack `beforeLoad` may improve UX but are never the authoritative authorization barrier.
- Server functions/routes must independently validate identity and access.
- Database RLS becomes the canonical final row-level barrier once persistence begins.

### Staff model direction
- Staff access is controlled by an application-owned server-authoritative record/capability, not `user_metadata` or a browser-controlled role.
- A person may later be both staff and a member of one or more client organisations; those relationships remain independent.
- Start with a minimal staff-access primitive rather than a large RBAC catalogue.

### Organisation membership direction
- One organisation may have multiple users.
- One user may belong to multiple organisations.
- Future domain rows will scope through `organisation_id` where appropriate.
- Membership status/capability must be validated server-side for organisation-scoped reads/writes.

### Active organisation decision
Canonical UX direction:
- exactly one active membership: automatically use that organisation context;
- multiple active memberships: require an organisation choice before entering organisation-scoped Portal work;
- any persisted active-organisation selector is only a preference/context pointer, never authorization evidence;
- server/RLS must revalidate membership for the selected organisation on every protected boundary.

No organisation switcher is implemented in F0/F1.

### Authentication-method decision
- Initial Re:Solve auth is **invite-oriented email/password with an MFA-ready architecture**.
- Do not require SAML/enterprise SSO in Foundation.
- SAML/OIDC/enterprise SSO remains a later capability when a concrete customer/staff requirement justifies it.
- Do not expose unrestricted public self-signup unless later product policy explicitly enables it.

### Session direction
For SSR/TanStack Start, the intended architecture is cookie-backed Supabase Auth with separate browser/server clients and per-request server validation. Do not trust a raw client session object for authorization. F1 must use the actual current Supabase/TanStack-supported APIs discovered at implementation time rather than copied framework assumptions.

### RLS direction
- Least privilege, organisation-scoped policies, explicit membership checks.
- Do not grant all authenticated users broad read/write access.
- Avoid recursive policy design.
- `SECURITY INVOKER` remains the default.
- Do **not** pre-authorize `SECURITY DEFINER` as a generic recursion workaround. A definer helper is acceptable only if a concrete RLS design proves it necessary, with narrow purpose and explicit security review.

### Service-role direction
- Server-only.
- Never browser bundled.
- Never a shortcut around normal user RLS flows.
- Only use behind a justified privileged server boundary when later requirements demand it.

### Demo identity transition
- `Amara Okafor / Administrator` and `Chinedu Okeke / Acme Properties Ltd.` remain deterministic shell evidence only.
- Do not silently create matching production auth users.
- Once auth-backed identity is implemented, shell identity should derive from the authenticated profile/membership context; demo fixtures may remain only in explicit development/demo-data paths.

### Environment-key normalization for F1
Current source uses optional `VITE_SUPABASE_ANON_KEY`, but current Lovable Cloud conventions use a publishable key naming pattern. F1 must inspect the actual activated backend credentials and deliberately normalize the env contract rather than introducing duplicate competing key names.

### Self-hostability
Supabase-based auth is acceptable for Re:Solve portability because the target architecture can move from Lovable Cloud to managed/self-hosted Supabase. Avoid Lovable-only runtime APIs in application auth boundaries. Authentication provider configuration, secrets and user migration remain deployment concerns that must be documented before production onboarding.

### F0 risk register
**HIGH**
- trusting user/app metadata for staff/organisation authorization;
- cross-organisation leakage from missing `organisation_id` boundaries;
- service-role leakage or use as a normal user data path.

**MEDIUM**
- client-only route guards;
- SSR/browser session disagreement;
- stale/revoked session assumptions;
- recursive RLS policy design;
- unjustified `SECURITY DEFINER` helpers;
- duplicated profile vs auth identity sources;
- active-organisation context treated as authorization;
- Lovable-specific backend assumptions leaking into portable app code.

**LOW / DEFERRED**
- enterprise SSO requirement before a real customer requirement exists.

### Accepted implementation staging
**FOUND-001F1 — Auth transport/session foundation**
- confirm/activate actual Lovable Cloud/Supabase backend;
- normalize current Supabase public env contract;
- add only required current Supabase auth packages;
- implement browser/server Supabase client primitives and secure SSR cookie/session transport;
- create minimal login/callback/logout/reset foundations as justified;
- no application identity tables/RLS yet.

**FOUND-001F2 — Identity schema + RLS baseline**
- profiles;
- organisations;
- memberships;
- minimal staff-access record;
- migrations/types;
- least-privilege baseline RLS.

**FOUND-001F3 — Server-authoritative surface access**
- real server auth/access helpers based on existing primitives;
- `/admin` staff boundary;
- Portal membership/active-organisation boundary;
- TanStack UX redirects layered on top, never replacing server/RLS enforcement.

**FOUND-001F4 — Invitation/onboarding + identity transition + closure review**
- controlled staff/client invitations;
- onboarding binding auth identity to profile/access records;
- shell demo identity transition;
- MFA policy decision/enforcement where required;
- final auth-foundation security/portability review.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- TanStack React Table `8.20.5` is canonical.
- `/ui` is development/Lovable gallery and redirects to `/` in production.
- `/admin` is the frozen staff/admin application shell.
- `/`, `/properties`, `/projects`, `/support`, `/billing` share the frozen client-facing Portal shell.
- No active application auth/session/database/RLS implementation exists yet.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Client Portal is calmer and less dense than Admin while remaining clearly Re:Solve.
- Àríyá is Re:Solve's built-in AI surface; Chatwoot keeps Captain separately.
- shadcn-vue is visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Begin FOUND-001F1 as a small auth **transport/session foundation** slice only. First establish/confirm the actual Lovable Cloud/Supabase backend and current credentials, then normalize the Supabase env contract and implement secure SSR-compatible browser/server auth clients plus minimal sign-in/session/logout plumbing. Do not create profiles, organisations, memberships, staff tables, RLS domain policies or Admin/Portal authorization gates in F1; those belong to F2/F3 after the session transport is proven.