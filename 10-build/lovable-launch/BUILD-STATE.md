# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5D1-D2 ACCEPTED/FROZEN — FOUND-001C5D3 CONDITIONAL (TWO NARROW CLOSURE ITEMS)**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and FOUND-001C1-C5D2 are accepted/canonical/frozen. Do not reopen frozen UI slices without a concrete regression.

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
**STATUS: CONDITIONAL — TWO NARROW CLOSURE ITEMS**

Verified D3 improvements:
- loading/source-empty/filtered-empty state cells use `table.getVisibleLeafColumns().length`, so state rows track current column visibility;
- DataTable source documents the selection identity boundary: index IDs are transient/display-only; persisted/business/action/audit-sensitive selection requires stable consumer-supplied `getRowId`;
- selection remains internally preserved when filtering hides rows while the visible summary reflects filtered selected rows;
- sorting/filtering state remains intact when columns are hidden;
- pagination footer stacks `flex-col` at narrow widths and returns to `sm:flex-row` at larger widths;
- no dependency drift was introduced and the canonical `js-yaml` override remains intact;
- advanced server/manual data mode, URL state, saved views and persistent ordering remain deferred beyond Foundation Core.

### Remaining closure items
1. **Page-size Select accessible name.** The DataTable page-size `SelectTrigger` is visually next to “Rows per page” but is not programmatically associated. Add `aria-label="Rows per page"` (or an equivalent explicit association) to that existing trigger. Do not modify frozen Core Select.
2. **Dedicated TanStack Table provenance entry.** `docs/ui-sources.md` currently mentions TanStack-backed DataTable behavior only inside the broad shadcn modification paragraph. Add a dedicated runtime provenance entry for `@tanstack/react-table` recording version `8.20.5`, MIT license, first Re:Solve Core consumption in FOUND-001C5D1, its role as the headless table engine, and that Re:Solve owns rendering/tokens/responsive/public DataTable API. Record D2 filtering/visibility/selection and D3 deferral of server/manual pagination/sorting/filtering, URL state, saved views, persistence, bulk actions and domain adapters. Preserve the separate frozen semantic `Table` boundary.

This is documentation/accessibility closure only. Do not reopen DataTable architecture or add capability.

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
Execute one narrow FOUND-001C5D3-FIX for the page-size accessible name and dedicated TanStack Table provenance entry, rerun frozen install/build/lint/type, then stop for final DataTable freeze review. Do not begin another FOUND slice until C5D3 is accepted.