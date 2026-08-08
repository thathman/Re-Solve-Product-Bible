# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E1-E2 CLIENT PORTAL SHELL ACCEPTED/FROZEN — FOUND-001E3 NEXT**

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
**ACCEPTED / CANONICAL / FROZEN**
Canonical E2 includes:
- pathless Portal layout `src/routes/_portal.tsx` composing `PortalShell` + `Outlet`;
- Home moved to `src/routes/_portal.index.tsx`, so `/` is a true child of the shared Portal layout rather than a root-level sibling;
- `/properties`, `/projects`, `/support`, `/billing` as placeholder-only children of the same `_portal` layout;
- generated route tree confirms `/_portal/` owns browser path `/` and all five Portal destinations share one shell;
- obsolete standalone `src/routes/index.tsx` removed;
- shared shell-local `portal-nav.ts` contains five real destinations;
- desktop/mobile navigation use real TanStack Links with route-aware active state and `aria-current="page"`; mobile selection closes the Sheet;
- `PortalBreadcrumbs` provides `Home / Current Section` for non-Home routes while Home remains breadcrumb-free;
- `PortalPageHeader` composes Portal breadcrumbs without entering Core;
- `PortalShell` owns one local `commandOpen` state and Cmd/Ctrl+K listener with `preventDefault`, functional toggle and cleanup;
- `PortalCommandMenu` composes frozen Core Command primitives, uses TanStack navigation, closes after selection, and keeps Notifications/Àríyá as truthful placeholder quick-access actions;
- optional unused React/Search imports in `PortalCommandMenu` removed during final closure;
- no new dependencies, auth, database, domain state, Admin/Core changes or security drift introduced.

Do not reopen E2 without a concrete route/search regression.

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
Begin FOUND-001E3 as the final Client Portal shell-composition slice: define the Portal Àríyá placement, close Notifications/account placeholder contracts, review desktop/tablet/mobile shell composition, and perform a no-feature closure audit without implementing auth, database, domain data, real notifications or AI backend.