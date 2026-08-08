# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5D3 ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5E CONDITIONAL / FINAL CLOSURE NEXT**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and FOUND-001C1-C5D3 are accepted/canonical/frozen. Do not reopen frozen UI slices without a concrete regression.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.

## Security memory
**ACCEPTED / CANONICAL**
The scanner-oriented Re:Solve Security Memory is canonical. Authentication/authorization remain server-authoritative; final auth/RLS/Vault/Action Registry are not yet implemented; no vulnerability exceptions are accepted.

## SECURITY-GATE-001 — Dependency remediation
**ACCEPTED / CLOSED**
Canonical package security state remains:
- `@tanstack/react-router`: `^1.170.18`
- `@tanstack/react-start`: `^1.168.32`
- `@tanstack/router-plugin`: `^1.168.23`
- no direct `@tanstack/router-core`
- no direct `js-yaml`
- top-level Bun override: `"js-yaml": "4.3.1"`
- accepted scan cleared `GHSA-5p4m-2wfm-xmqj` with no remaining High/Critical findings.

## FOUND-001C5D1 — DataTable Core Foundation
**ACCEPTED / CANONICAL / FROZEN**
Canonical D1 includes generic `DataTable<TData, TValue>`, TanStack core/sorted/pagination row models, semantic Core Table rendering, accessible client sorting, frozen Core Pagination reuse, 10/20/50 page-size selector, loading/error/source-empty states, exact-optional-safe `getRowId`, bounded horizontal overflow, and `@tanstack/react-table@8.20.5` as the single DataTable engine dependency.

## FOUND-001C5D2 — Operational Controls
**ACCEPTED / CANONICAL / FROZEN**
Canonical D2 includes typed global/text/select filtering, the non-empty `__all__` Select sentinel, runtime-narrowed filter values, visibility controls independent of search/filter presence, opt-in current-page row selection, unique accessible row-selection labels, filtered-empty truth based on the filtered row model, filter-reset-to-first-page behavior, generic fictional gallery data, non-sortable Status evidence, no dependency changes, and preserved `js-yaml@4.3.1` override.

## FOUND-001C5D3 — DataTable Closure / Structural Audit
**ACCEPTED / CANONICAL / FROZEN**
Canonical D3 closure includes:
- loading/source-empty/filtered-empty state cells use `table.getVisibleLeafColumns().length`, so state rows remain structurally valid after column visibility changes;
- DataTable documents the selection identity boundary: TanStack index IDs are acceptable only for transient display selection, while persisted/business/action/audit-sensitive selection requires stable consumer-supplied `getRowId`;
- filtering can hide selected rows without silently clearing internal selection; visible summary truthfully reflects filtered selected rows;
- sorting/filtering state remains intact when columns are hidden;
- pagination footer stacks on narrow screens and returns to horizontal layout at `sm` and above;
- page-size Select has explicit `aria-label="Rows per page"`;
- dedicated `@tanstack/react-table` provenance records version `8.20.5`, MIT license, first Core consumption in D1, D2 capability additions, and D3 deferrals;
- no dependency drift was introduced and the canonical `js-yaml` override remains intact;
- server/manual pagination/sorting/filtering, URL state, saved views, persistent ordering/visibility, column pinning, bulk actions, exports and domain-specific adapters/actions remain deferred beyond Foundation Core.

The Re:Solve DataTable foundation is structurally closed. Do not reopen it during FOUND-001 unless a later shell/domain requirement exposes a concrete missing foundation contract.

## FOUND-001C5E — Core Navigation Foundations
**CONDITIONAL — FINAL CLOSURE REQUIRED**
The implementation correctly established Re:Solve-owned Sidebar and NavigationMenu foundations by adapting the repository's existing shadcn/Radix source rather than adding dependencies.

Verified-good C5E architecture:
- Sidebar has controlled/uncontrolled open state and separate mobile-open state.
- Core Sidebar contains no cookie/localStorage/sessionStorage persistence and no global Cmd/Ctrl+B listener.
- Sidebar consumes frozen Core Button/Input/Separator/Sheet/Skeleton/Tooltip rather than stock `src/components/ui/*` equivalents.
- Sidebar uses canonical `--spacing-rs-sidebar-width` / `--spacing-rs-sidebar-collapsed` reservations and Re:Solve semantic tokens/focus variables.
- SidebarMenu/SidebarMenuItem preserve `ul`/`li` semantics; `asChild` supports future semantic router links/actions.
- active Sidebar items use selected surface + font weight + action-primary indicator, not color alone.
- collapsed Sidebar tooltips and mobile Sheet title/description are present.
- NavigationMenu is built on the existing `@radix-ui/react-navigation-menu` dependency with Re:Solve tokens/focus treatment and `asChild` support.
- Navigation Foundations gallery section exists and `/ui` remains production-guarded.
- package/security state is unchanged and no dependency was added.

Final C5E blockers:
1. `src/components/core/index.ts` added broad `export *` for Sidebar and NavigationMenu; C5E must use explicit intentional exports.
2. NavigationMenu provenance is inaccurate: package declaration is `^1.2.14`; the current dependency scan resolves `1.2.22`, not `1.2.5`.
3. NavigationMenu viewport/content needs a real narrow-screen width guard; gallery hierarchical content currently uses fixed 400–600px widths that can overflow phone viewports.
4. `SidebarMenuSkeleton` uses `Math.random()` to produce width during render/useMemo, which is unsuitable for deterministic SSR/hydration. Replace with deterministic width behavior or an explicit caller-provided width without random rendering.
5. While touching NavigationMenu visual closure, ensure active/current link evidence has a non-color distinction (for example font weight/indicator) and gallery link focus uses the frozen focus-variable contract rather than ad-hoc `focus:shadow-*` styling.

Do not reopen the Sidebar/NavigationMenu architecture beyond these concrete closure issues.

## FOUND-001C5E — Core UI Gap Audit
**AUDIT ACCEPTED**
The no-change audit found the existing Core broadly sufficient and classified remaining patterns by actual shell/domain need rather than by component-catalog completeness.

### Build now in C5E
- Sidebar primitives — required before Admin shell work; normalize/adapt the existing shadcn source.
- NavigationMenu — required as the generic horizontal/hierarchical navigation primitive; normalize/adapt the existing Radix/shadcn source.

### Build in shell (FOUND-001D/E)
- PageHeader
- CommandBar / CommandPalette composition over the frozen Command engine
- AppLayout containers
- DescriptionList / key-value detail composition

### Defer to first real domain requirement
- NumberField / Currency / Percent editing — do not block shell work; the first business form must define locale/parsing/precision/min/max/negative/step/null/display-value semantics.
- Timeline / activity
- FileUpload
- RichTextEditor
- Charts
- Kanban
- TreeSelect

### Unnecessary as dedicated Core families
- SearchField — compose InputGroup + icon/action
- Menubar
- SectionHeader
- generic Toolbar
- Carousel unless a later product requirement demonstrates an actual need

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- TanStack React Table `8.20.5` is the canonical DataTable engine.
- Auth, database/RLS, PWA and domain implementation remain later work.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Simple semantic `Table` remains separate from `DataTable`.
- DataTable Foundation remains client-side/headless-engine focused; domain adapters own future server/manual data modes and consequential actions.
- Keep established Radix/shadcn foundation.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Next action
Run one narrow FOUND-001C5E-FIX closure for explicit Core exports, correct NavigationMenu provenance, deterministic Sidebar skeleton rendering, narrow-screen NavigationMenu containment, and canonical active/focus gallery evidence. If clean, freeze C5E and begin FOUND-001D Admin Shell.