# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN FUNCTIONALLY — FOUND-001F2A IDENTITY SCHEMA/RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS ACCEPTED/CANONICAL/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION CONDITIONAL / CACHE HEADER MICRO-FIX NEXT — VIS-001A TWO-COLUMN AUTH ACCEPTED/CANONICAL/FROZEN**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval

## Security memory
**ACCEPTED / CANONICAL**
- Authentication, roles, permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route guards are UX gates only. Future private server functions/routes must independently authorize at their own server boundary.
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
**ACCEPTED / CANONICAL / FROZEN / CLOSED FUNCTIONALLY**
- Foundation + Core UI phases C1-C5E remain frozen functionally.
- `/ui` remains the dev-only Core gallery.
- Admin shell lives under `/admin` and contains Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Client Portal shell covers `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Shells may reopen only for a concrete regression or a separately supervised visual-system rollout.

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
Canonical identity facts remain distinct: Auth User, Profile, Organisation, Organisation Membership, Staff Access.

Surface direction:
- `/admin` requires authenticated active staff access.
- Portal requires authenticated active organisation membership.
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
**ACCEPTED / CANONICAL / FROZEN FUNCTIONALLY**
Routes: `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`.

Canonical behavior:
- invite-oriented email/password; no public signup/social login/MFA yet;
- login uses canonical `supabaseAuthBrowser`;
- PKCE exchange is server-side through the cookie-backed request client;
- forgot-password messaging is account-enumeration-safe;
- reset errors are provider-neutral;
- safe internal redirects only;
- reusable server-side sign-out exists;
- F1 authenticates identity only; it does not authorize Admin/Portal access.

The auth UI may evolve under the separate supervised visual rollout without reopening these functional/security contracts.

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
- `readCurrentIdentity()` starts from real `getAuthenticatedUser()`;
- all reads use caller-scoped Supabase + RLS;
- unauthenticated, valid absence, active/suspended staff, active/suspended membership and multi-membership states remain distinct;
- active organisations resolve only through caller-scoped RLS;
- every active membership must resolve before the snapshot succeeds;
- database/status/integrity failures fail closed with one stable error;
- raw provider/database/Zod details are not logged or surfaced;
- no service-role use, writes, UI, route guards, RBAC or active-org persistence.

## FOUND-001F3A — Server-authoritative Admin access
**CONDITIONAL — ACCESS MODEL ACCEPTED; ROUTE-FACING CACHE HEADER MICRO-FIX PENDING**

Verified files:
- `src/lib/identity/access.server.ts`
- `src/lib/identity/access.functions.ts`
- `src/routes/admin.tsx`
- `src/routes/access-denied.tsx`

Verified-good behavior:
- `requireActiveStaff()` is server-only and derives access from frozen `readCurrentIdentity()`;
- unauthenticated => 401 at the reusable server boundary;
- authenticated without staff or suspended staff => 403;
- active staff => allowed;
- staff + client membership coexistence remains valid;
- `checkAdminAccess()` exposes only `allowed | unauthenticated | forbidden`;
- parent `/admin` `beforeLoad` gates the complete Admin route family;
- unauthenticated Admin visits redirect to `/login` with router-derived internal `returnTo`;
- authenticated forbidden visits redirect to `/access-denied` outside the Admin family;
- identity resolution failures propagate fail-closed rather than becoming ordinary access states;
- no Portal, database, auth transport, RBAC or service-role changes were introduced.

Pending micro-fix:
- `src/lib/identity/access.functions.ts` currently claims `getAdminAccess` is `no-store`, but does not actually set the response header.
- Close with the existing real TanStack Start server API already used elsewhere in the app: `setResponseHeader` from `@tanstack/react-start/server`.
- Set at minimum `Cache-Control: private, no-store` locally on the identity-dependent access response; preserve appropriate `Vary` handling if added.
- Do not touch global middleware or `src/start.ts`.

## Visual direction — clean reference-led Re:Solve system
**APPROVED / STANDING PRODUCT REQUIREMENT**
This is not a one-off auth treatment. It is the visual system to be progressively propagated through Auth, Admin, then Portal while preserving frozen behavior/security.

Canonical visual grammar:
- Inter remains the primary UI typeface unless a future supervised comparison proves a materially better choice;
- restrained typography: roughly 11–12px metadata, 12–14px secondary text, 13–15px controls/navigation, 15–17px card headings, larger values rather than oversized generic page headings;
- Lucide icons generally 16–18px, light/technical treatment, colour concentrated in small meaningful icon/status surfaces;
- quiet neutral light mode and charcoal/graphite dark mode;
- subtle 1px borders, near-zero shadows, restrained 14–18px major radii;
- cards use disciplined anatomy, separators/inset regions and nested surfaces instead of floating-card overload;
- content pages should favour structured regions, rows, tables, charts and meaningful metrics over generic dashboard card grids;
- no generic AI blue/purple gradients, glassmorphism, neon borders, oversized marketing typography or decorative SaaS clutter;
- Admin may be denser; Portal uses the same family with more breathing room and selective editorial warmth.

Standing rollout:
1. two-column Auth family;
2. Admin shell + Admin page visual system using the same approved card/font/icon grammar;
3. Client Portal propagation with the same family at lower density;
4. later domain screens continue the same system rather than inventing new styling per module.

This rollout remains queued even when security/data slices temporarily take precedence.

## VIS-001A — Two-column Auth + visual language proof
**ACCEPTED / CANONICAL / FROZEN VISUALLY**

Verified runtime files:
- `src/components/auth/AuthLayout.tsx`
- `src/components/auth/AuthProductPreview.tsx`
- `src/components/auth/LoginForm.tsx`
- `src/components/auth/ForgotPasswordForm.tsx`
- `src/components/auth/ResetPasswordForm.tsx`
- `src/routes/auth.callback.tsx`

Canonical implementation:
- desktop auth is a genuine full-height two-column composition rather than a centered floating card;
- left panel is approximately 45% width on desktop and uses a Re:Solve operational product preview rather than stock/marketing imagery;
- right form column is a restrained ~420px product-auth surface;
- product preview uses Re:Solve metrics/activity, subtle borders, nested neutral surfaces, minimal shadows and disciplined Lucide icons;
- Inter remains the UI typeface; no new visual dependency was introduced;
- mobile intentionally collapses to a form-first single-column experience;
- login, forgot-password, reset-password and auth callback share the same environment;
- frozen auth transport/PKCE/reset/security behavior remains structurally unchanged.

Accessibility closure accepted:
- login and reset password visibility controls are in the normal keyboard tab sequence;
- controls retain `type="button"` and therefore do not submit forms;
- state-aware accessible labels are `Show password` / `Hide password`;
- visibility controls use the canonical Re:Solve focus-visible variables;
- interactive target is 36px within the existing 44px input composition; icon remains 16px.

Do not materially redesign the Auth family again without a supervised visual requirement or concrete regression.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth transport, auth behavior, identity persistence/RLS/grants and identity reads are frozen functionally.
- VIS-001A is frozen as the first approved runtime example of the clean reference-led Re:Solve visual language.
- Admin authorization exists directionally but F3A has one response-cache header micro-fix pending.
- Portal authorization is not active yet.
- No active-organisation selector, invitation/onboarding flow, domain tables or broad RBAC exists yet.
- Admin and Portal visual propagation remain standing requirements and are not considered complete merely because Auth is redesigned.

## Sequencing
Continue supervised implementation in small slices. Security/data work may temporarily precede visual propagation, but the approved visual rollout remains explicitly queued.

Near-term order:
1. close F3A route-facing cache-header micro-fix;
2. resume F3B/F3C Portal authorization and organisation-context foundation in small reviewed slices;
3. continue the approved visual rollout into Admin, then Portal;
4. domain screens inherit the same approved visual language.

## Next action
Run one narrow **FOUND-001F3A-FIX — Admin Access Cache-Control Closure**. Modify only the route-facing Admin access server function as needed to set real identity-dependent response cache headers using the existing TanStack Start server response API. Preserve the accepted Admin access model, route behavior, auth/identity boundaries, Portal state and UI. If clean, freeze F3A and proceed to F3B.