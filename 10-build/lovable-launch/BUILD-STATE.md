# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 ACCEPTED/CANONICAL — FOUND-001F1A AUTH TRANSPORT ACCEPTED/CANONICAL/FROZEN — FOUND-001F1B AUTH UX ACCEPTED/CANONICAL/FROZEN — FOUND-001F2A IDENTITY SCHEMA/RLS ACCEPTED/CANONICAL/FROZEN — FOUND-001F2B IDENTITY READS ACCEPTED/CANONICAL/FROZEN — FOUND-001F3A ADMIN AUTHORIZATION CONDITIONAL / CACHE HEADER MICRO-FIX PENDING — VIS-001A TWO-COLUMN AUTH + VISUAL LANGUAGE NEXT**

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
**ACCEPTED / CANONICAL / FROZEN**
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

Canonical behavior:
- `readCurrentIdentity()` starts from real `getAuthenticatedUser()`;
- all reads use caller-scoped Supabase + RLS;
- unauthenticated, valid absence, active/suspended staff, active/suspended membership and multi-membership states remain distinct;
- active organisations resolve only through caller-scoped RLS;
- every active membership must resolve before the snapshot succeeds;
- database/status/integrity failures fail closed with one stable error;
- raw provider/database/Zod details are not logged or surfaced;
- no service-role use, writes, UI, route guards, RBAC or active-org persistence.

## FOUND-001F3A — Server-authoritative Admin access
**CONDITIONAL — ACCESS MODEL ACCEPTED; ROUTE-FACING CACHE HEADER CLAIM NOT YET IMPLEMENTED**

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

### Pending micro-fix
`src/lib/identity/access.functions.ts` currently comments that the identity-dependent `getAdminAccess` response is `no-store`, but it does not actually set response cache headers. Before F3A can freeze, implement the real local TanStack response header behavior, at minimum `Cache-Control: private, no-store`, and preserve any appropriate `Vary` behavior without touching global middleware or `src/start.ts`.

This is a small known security closure and does not block beginning the independent visual rollout.

## Visual direction — clean reference-led Re:Solve system
**APPROVED DIRECTION / ROLLOUT BEGINNING**
The next visual work should visibly move Re:Solve toward the supplied clean product references rather than generic SaaS styling.

Visual grammar to establish:
- Inter remains the primary UI typeface unless a supervised comparison proves another choice materially better;
- small/medium type with restrained weights; large values rather than oversized generic headings;
- Lucide icons at disciplined 16–18px default sizes with restrained stroke weight;
- quiet neutral canvas, white/light raised surfaces, charcoal dark mode;
- thin subtle borders; near-zero shadows; approximately 14–18px major card radius where appropriate;
- cards use consistent internal anatomy, separators and inset regions rather than floating-card overload;
- content pages should prefer large structured regions, tables, rows, charts and nested surfaces over generic card grids;
- accent colour appears with meaning, especially in icon tiles/status/visualisation, not as pervasive gradients;
- Admin can be denser; Portal can use the same system with more breathing room;
- no generic AI blue/purple gradients, glassmorphism, oversized marketing-dashboard typography or decorative SaaS clutter.

First visible target: the complete auth family becomes a polished two-column product-auth layout on desktop, with a compact single-column adaptation on smaller screens. This is the first supervised proof of the new visual language before propagation into Admin.

## Current architecture facts
- TanStack Start + React 19 + Bun + Tailwind v4.
- Auth transport, auth UX, identity persistence/RLS/grants and identity reads are frozen functionally.
- Admin authorization exists directionally but F3A has one response-cache header micro-fix pending.
- Portal authorization is not active yet.
- No active-organisation selector, invitation/onboarding flow, domain tables or broad RBAC exists yet.
- The clean visual rollout has not yet been applied to runtime UI; VIS-001A is the first visual implementation slice.

## Next action
Pause F3B. Begin **VIS-001A — Two-Column Auth + Visual Language Proof**. Redesign the existing auth family only, preserving all frozen auth behavior/security, to establish the approved clean reference-led Re:Solve visual grammar. Desktop should use a true two-column composition; tablet/mobile should collapse deliberately. Do not yet reskin Admin/Portal in this slice. After VIS-001A is inspected and frozen, propagate the same visual grammar into Admin through a separate visual-system slice, while separately closing the small F3A cache-header issue before further authorization work.