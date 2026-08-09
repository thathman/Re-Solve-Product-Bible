# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN — FOUND-001F2A IDENTITY SCHEMA/RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS ACCEPTED/CANONICAL/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION CONDITIONAL / CACHE HEADER MICRO-FIX PENDING — VIS-001A TWO-COLUMN AUTH CONDITIONAL / PASSWORD-TOGGLE A11Y FIX NEXT**

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
Canonical identity facts are distinct: Auth User, Profile, Organisation, Organisation Membership, Staff Access.

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
- `src/lib/identity/access.functions.ts` says the identity-dependent `getAdminAccess` response is `no-store`, but does not actually set the response cache header.
- Before F3A freezes, implement real local TanStack response headers, at minimum `Cache-Control: private, no-store`, without changing global middleware or `src/start.ts`.

## Visual direction — clean reference-led Re:Solve system
**APPROVED / STANDING PRODUCT REQUIREMENT**
The owner-approved visual direction is not a one-off auth treatment. It is the visual system to be progressively propagated through Auth, Admin, then Portal while preserving functional/security boundaries.

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

The requested rollout remains:
1. two-column Auth family;
2. Admin shell + Admin page visual system using the same approved card/font/icon grammar;
3. Client Portal propagation with the same family at lower density;
4. later domain screens continue the same system rather than inventing new styling per module.

## VIS-001A — Two-column Auth + visual language proof
**CONDITIONAL — VISUAL DIRECTION IMPLEMENTED; PASSWORD-TOGGLE ACCESSIBILITY FIX REQUIRED**

Verified runtime files:
- `src/components/auth/AuthLayout.tsx`
- `src/components/auth/AuthProductPreview.tsx`
- `src/components/auth/LoginForm.tsx`
- `src/components/auth/ForgotPasswordForm.tsx`
- `src/components/auth/ResetPasswordForm.tsx`
- `src/routes/auth.callback.tsx`

Verified visual implementation:
- desktop auth is now a genuine two-column full-height composition rather than the old centered floating Card;
- left panel is approximately 45% width on desktop and uses a Re:Solve product preview rather than stock/marketing imagery;
- right form column is a restrained ~420px product-auth surface;
- product preview uses Re:Solve metrics/activity, subtle borders, nested neutral surfaces, minimal shadows and Lucide icons;
- Inter remains in use; no new font or visual dependency was added;
- mobile intentionally collapses to a form-first single-column experience;
- login, forgot-password, reset-password and auth callback share the same visual environment;
- frozen auth transport/PKCE/reset/security behavior remains structurally unchanged.

Pending accessibility closure:
- login password visibility button and reset-password visibility button currently use `tabIndex={-1}` and have no accessible name;
- these controls must be keyboard reachable, have an explicit accessible label reflecting Show/Hide password state, use the canonical focus-visible contract, and preserve the existing 44px input composition;
- this is a UI accessibility correction only; do not change auth behavior.

VIS-001A should freeze after that narrow fix.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth transport, auth behavior, identity persistence/RLS/grants and identity reads are frozen functionally.
- Admin authorization exists directionally but F3A has one response-cache header micro-fix pending.
- Portal authorization is not active yet.
- No active-organisation selector, invitation/onboarding flow, domain tables or broad RBAC exists yet.
- The visible clean redesign has begun in Auth; Admin and Portal propagation remain explicitly scheduled and are not forgotten.

## Sequencing
Continue supervised implementation in small slices. Visual requirements are standing requirements and remain queued even when security/data slices temporarily take precedence.

Near-term order:
1. close VIS-001A password-toggle accessibility;
2. close F3A cache-header micro-fix;
3. resume F3B/F3C Portal authorization and organisation-context foundation in small reviewed slices;
4. continue the approved visual rollout into Admin and Portal without reopening frozen security behavior.

## Next action
Run one narrow **VIS-001A-FIX — Password Toggle Accessibility Closure**. Change only the auth form visibility controls required to make them keyboard accessible, explicitly named for assistive technology and compliant with the canonical focus-visible treatment. Preserve the approved two-column composition and all frozen auth behavior. Then freeze VIS-001A.