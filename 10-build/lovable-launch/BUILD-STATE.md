# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5D3 ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5E AUDIT ACCEPTED / IMPLEMENTATION NEXT**

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

## FOUND-001C5E — Core UI Gap Audit
**AUDIT ACCEPTED / IMPLEMENTATION NEXT**
The no-change audit found the existing Core broadly sufficient and classified remaining patterns by actual shell/domain need rather than by component-catalog completeness.

### Build now in C5E
- **Sidebar primitives** — required before Admin shell work. The repository already contains a stock shadcn-style `src/components/ui/sidebar.tsx`; C5E should adapt/normalize that source into the Re:Solve Core boundary rather than inventing a new sidebar system.
- **NavigationMenu** — required as the generic horizontal/hierarchical navigation primitive for the Client Portal and other suitable horizontal navigation contexts. The repository already contains `src/components/ui/navigation-menu.tsx` on the existing Radix Navigation Menu dependency; normalize/adapt rather than reinstall.

### Build in shell (FOUND-001D/E)
- PageHeader
- CommandBar / CommandPalette composition over the frozen Command engine
- AppLayout containers
- DescriptionList / key-value detail composition

These require shell/application intent and should not be frozen prematurely as generic Core primitives.

### Defer to first real domain requirement
- **NumberField / Currency / Percent editing** — do not block shell work. Numeric editing needs a concrete contract for locale, parsing, precision, min/max, negative values, stepping, empty/null behavior, and display-vs-value semantics. Build it when the first business form requires it, using existing Input/FormField/InputGroup foundations unless that domain exposes a genuine reusable Core contract.
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

### C5E implementation boundary
C5E implementation should therefore contain only:
1. Re:Solve Core Sidebar primitive family, normalized from the existing shadcn source and frozen Re:Solve tokens/components.
2. Re:Solve Core NavigationMenu primitive family, normalized from the existing Radix/shadcn source.
3. Gallery/provenance/accessibility/responsive evidence for those two families.

No NumberField implementation in C5E. No shell-specific route hierarchy, product navigation IA, workspace switcher, account menu, notifications, global search, or Àríyá behavior yet.

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
Implement FOUND-001C5E as the final pre-shell Core navigation-foundation slice: normalize/adapt the existing shadcn-style Sidebar and Radix/shadcn NavigationMenu into the canonical Re:Solve Core boundary, with gallery, responsive, accessibility and provenance evidence. Do not implement shell information architecture or NumberField in this slice.