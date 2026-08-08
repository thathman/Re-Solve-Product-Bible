# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A-B ACCEPTED/CLOSED — FOUND-001C1-C5E ACCEPTED/FROZEN/CLOSED — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001D ADMIN SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001E CLIENT PORTAL SHELL ACCEPTED/CLOSED/FROZEN — FOUND-001F0 IDENTITY/AUTH ARCHITECTURE PREFLIGHT NEXT**

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

## FOUND-001E — Client Portal Shell
**ACCEPTED / CANONICAL / FROZEN / CLOSED**

### E1 — Chrome & visual foundation
Canonical Portal shell includes:
- client-facing surface at `/` with the old Lovable blank placeholder removed;
- shell-owned `PortalShell`, `PortalTopBar`, `PortalNavigation`, `PortalPageHeader`, and `portal-nav.ts` with no Admin-shell imports;
- horizontal Core NavigationMenu on desktop and purpose-built Core Sheet navigation on mobile;
- Re:Solve brand, Search, Notifications count `2`, Àríyá entry point, and deterministic fictional identity `Chinedu Okeke / Acme Properties Ltd.` with `CO` fallback;
- one Portal main landmark, canonical focus variables, semantic OKLCH tokens and responsive gutter tokens;
- Notifications trigger semantics on the actual button; Core public boundary for NavigationMenu/toast; canonical destructive/status tokens;
- no auth, database/RLS/domain implementation, real Notifications or AI backend.

### E2 — Route skeletons & Command/Search
Canonical Portal route family:
- pathless `src/routes/_portal.tsx` composes `PortalShell` + `Outlet`;
- Home is `src/routes/_portal.index.tsx` at browser path `/`;
- `/properties`, `/projects`, `/support`, `/billing` are placeholder-only children of the same `_portal` layout;
- desktop/mobile navigation use real TanStack Links with route-aware active state and `aria-current="page"`; mobile selection closes the Sheet;
- non-Home routes use `Home / Current Section` breadcrumbs while Home remains breadcrumb-free;
- `PortalShell` owns local `commandOpen` state and Cmd/Ctrl+K listener with `preventDefault`, functional toggle and cleanup;
- `PortalCommandMenu` composes frozen Core Command primitives, uses TanStack navigation, closes after selection, and keeps Notifications/Àríyá as shell-level quick access.

### E3 — Composition closure
Canonical Portal composition includes:
- shell-owned `PortalAriyaPanel` as a right-side frozen Core Sheet with title `Àríyá`, description `Re:Solve AI workspace.`, and truthful not-connected `StatePanel`;
- `PortalShell` owns exactly two local shell states: `commandOpen` and `ariyaOpen`;
- desktop/mobile TopBar Àríyá controls and Command `Open Àríyá` open the same Sheet state;
- Notifications remain anchored in the TopBar with deterministic unread count `2`;
- Account, Organisation, Preferences and Sign out remain truthful placeholders with no account/auth routes.

### E4 — Final closure review
**PASS — NO BLOCKERS**
Verified as one system across desktop/tablet/mobile:
- `/`, `/properties`, `/projects`, `/support`, `/billing` are all children of the shared pathless `_portal` layout and inherit one `PortalShell`;
- `/admin` remains isolated under the frozen Admin shell;
- desktop/mobile navigation, active-route semantics and mobile Sheet close behavior are coherent;
- breadcrumbs, Cmd/Ctrl+K Command/Search, Notifications, shared Àríyá Sheet and account placeholder contracts remain intact;
- exactly one Portal `main` landmark; named icon controls, keyboard/focus behavior and light/dark semantic tokens remain coherent;
- canonical gutter tokens remain in use;
- placeholder pages contain no business mock records, KPI cards, charts or forms;
- instruction/task-style Foundation comments were removed from Portal shell runtime source while concise architecture comments remain acceptable;
- Core/Admin/package/security boundaries remain unchanged;
- reported `bun run build`, `bun run lint`, and `bunx tsc --noEmit` checks pass.

FOUND-001E is closed. Do not reopen it without a concrete regression or a later requirement exposing a missing shell contract.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- TanStack React Table `8.20.5` is canonical.
- `/ui` is development/Lovable gallery and redirects to `/` in production.
- `/admin` is the frozen staff/admin application shell.
- `/`, `/properties`, `/projects`, `/support`, `/billing` share the frozen client-facing Portal shell.
- Auth, database/RLS and PWA are not yet implemented.

## UI/product direction
- Re:Solve Core is the public UI boundary.
- Client Portal is calmer and less dense than Admin while remaining clearly Re:Solve.
- Àríyá is Re:Solve's built-in AI surface; Chatwoot keeps Captain separately.
- shadcn-vue is visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- No timesheets, HR, or client service-consumption concepts.

## Next action
Run FOUND-001F0 as a **read-only Identity/Auth Architecture Preflight** before implementing authentication. Inspect the actual app/Lovable Cloud/Supabase integration, environment/server boundaries and existing dependencies; identify what auth infrastructure really exists; define the minimal identity, organisation-membership, staff/client surface-access and authorization model; map where server-enforced guards/RLS will eventually belong; and return a staged F1+ implementation plan. Do not install packages, create tables, enable providers, add route guards, or alter UI during F0. Only after supervisor review of F0 should authentication implementation begin.