# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E1 CLIENT PORTAL SHELL ACCEPTED/FROZEN — FOUND-001E2 CONDITIONAL / ROUTE-LAYOUT FIX NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — specification/planning source.
- Current app: `thathman/re-solve-c560d62c` — canonical Lovable development app on `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Security memory
**ACCEPTED / CANONICAL**
- Roles, permissions and capability decisions are server-controlled; browser/client metadata is never authoritative for authorization.
- Authentication and authorization must be enforced at server-function / server-route boundaries, not only in UI or client navigation.
- Never invent security helpers that do not exist; inspect and extend real server boundaries deliberately.
- RLS and least privilege are mandatory when persistence is introduced; database grants/policies/security configuration must be version-controlled and reviewable.
- Service-role credentials and privileged backend secrets are server-only and must never ship in client bundles.
- `SECURITY INVOKER` is the default; `SECURITY DEFINER` must remain narrow, justified and explicitly reviewed.
- Runtime validation is required at consequential server boundaries.
- Preserve `createCsrfMiddleware` in `src/start.ts`.
- Vault secrets must never appear in browser storage, logs, search results, notifications, analytics, non-Vault surfaces or ordinary client caches.
- QR codes may expose only signed, scoped, short-lived references/tokens; never raw secrets or durable privileged credentials.
- Consequential mutations should eventually route through an Action Registry / equivalent audited mutation boundary.
- Sensitive values, auth tokens, secret payloads and privileged identifiers must not be written to application logs or error telemetry.
- No security vulnerability exceptions are accepted.

## SECURITY-GATE-001 — Dependency remediation
**ACCEPTED / CLOSED**
Canonical package state:
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

## FOUND-001E1 — Client Portal Shell Chrome & Visual Foundation
**ACCEPTED / CANONICAL / FROZEN**
Canonical E1 includes:
- `/` as the Client Portal Home surface; old Lovable blank placeholder removed;
- shell-owned `PortalShell`, `PortalTopBar`, `PortalNavigation`, `PortalPageHeader`, and `portal-nav.ts` with no Admin-shell imports;
- horizontal Core NavigationMenu on desktop and purpose-built Core Sheet navigation on mobile;
- Re:Solve brand, Search placeholder, Notifications count `2`, Àríyá placeholder and deterministic fictional client identity `Chinedu Okeke / Acme Properties Ltd.`;
- one Portal main landmark, canonical focus variables and responsive gutter tokens;
- Notifications trigger semantics on the actual button; Core public boundary for NavigationMenu/toast; canonical destructive/status tokens;
- factual auth/authz deferral to FOUND-001F;
- no auth, database, RLS/domain implementation, real Search, real Notifications or AI backend.

Do not reopen E1 unless a concrete Portal-shell regression appears.

## FOUND-001E2 — Portal Route Skeletons & Command/Search
**CONDITIONAL — ROUTE-LAYOUT REGRESSION MUST BE FIXED**

Verified-good E2 work:
- pathless Portal layout exists at `src/routes/_portal.tsx` and composes `PortalShell` + `Outlet`;
- `/properties`, `/projects`, `/support`, `/billing` are generated as children of the pathless `_portal` layout and remain placeholder-only surfaces;
- shell-local `portal-nav.ts` now contains five real root destinations;
- desktop and mobile navigation use real TanStack Links with route-aware active state and `aria-current="page"`; mobile links close the navigation Sheet;
- `PortalBreadcrumbs` uses frozen Core Breadcrumb primitives, links Home with TanStack Router, and suppresses breadcrumbs on `/`;
- `PortalPageHeader` composes Portal breadcrumbs without moving the component into Core;
- `PortalShell` owns one local `commandOpen` state and installs Cmd/Ctrl+K with `preventDefault`, functional-state toggle and listener cleanup;
- `PortalCommandMenu` composes frozen Core Command primitives, uses TanStack navigation, closes after route selection, and keeps Notifications/Àríyá as truthful placeholder quick-access actions;
- no new dependencies, auth, database, domain state or Admin/Core changes are accepted in this slice.

### Blocking regression
The Home route is **not actually inside the shared `_portal` layout**.

Repository evidence:
- `src/routes/index.tsx` is still declared as `createFileRoute("/")` and now renders only `PortalPageHeader` + `StatePanel` with no `PortalShell` wrapper;
- generated `src/routeTree.gen.ts` places `IndexRoute` directly under `rootRouteImport`, while `_portal` is a separate sibling; only Billing/Projects/Properties/Support are children of `_portal`.

Result: `/` no longer receives the Portal TopBar, main layout, mobile navigation or Portal Command/Search even though E2 intended all five Portal routes to share one shell.

Required closure:
- move Home into the pathless Portal layout using the correct TanStack file-route convention (expected `src/routes/_portal.index.tsx` unless repository/router generation proves another canonical form);
- remove the obsolete standalone root `src/routes/index.tsx` route rather than leaving duplicate `/` routes;
- preserve Home browser URL `/`, metadata and validation content;
- regenerate `routeTree.gen.ts` so `/` is a child of `_portal` and there is no standalone root Index route;
- do not change working E2 shell/nav/breadcrumb/Command behavior.

Non-blocking hygiene: `PortalCommandMenu.tsx` currently has unused React/Search imports if lint permits them; they may be removed during the narrow routing fix without changing behavior.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- TanStack React Table `8.20.5` is canonical.
- `/ui` is development/Lovable gallery and redirects to `/` in production.
- `/admin` remains the frozen staff/admin application shell.
- Auth, database/RLS and PWA remain later work.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Client Portal is calmer and less dense than Admin while remaining clearly Re:Solve.
- Àríyá is Re:Solve's built-in AI surface; Chatwoot keeps Captain separately.
- shadcn-vue is visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Run one narrow FOUND-001E2-FIX to place Home under the shared pathless Portal layout and regenerate the route tree. Preserve all verified-good E2 navigation, breadcrumbs, Command/Search, E1 chrome, frozen Admin/Core, package/security state and explicit CSRF middleware. If clean, freeze E2 and proceed to the final Portal-shell composition slice E3.