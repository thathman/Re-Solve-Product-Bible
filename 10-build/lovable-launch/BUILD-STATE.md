# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5D1 ACCEPTED/FROZEN — FOUND-001C5D2 CONDITIONAL (NARROW FILTER/TOOLBAR/A11Y FIX REQUIRED)**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and FOUND-001C1-C5D1 are accepted/canonical/frozen. Do not reopen frozen UI slices without a concrete regression.

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
**STATUS: CONDITIONAL — NARROW FILTER/TOOLBAR/A11Y FIX REQUIRED**

### Verified implementation
- D2 adds `getFilteredRowModel` and internal global/column filter, column visibility and row-selection state;
- typed TanStack `ColumnMeta` filter metadata supports text/select filters;
- optional global search exists;
- hideable-column DropdownMenu exists;
- opt-in row-selection column uses frozen Core Checkbox and current-page select-all APIs;
- selected rows use `data-state="selected"`;
- filtered-empty state is distinct from source-empty state;
- Clear resets filter state without resetting sorting/visibility/selection;
- toolbar uses existing Core primitives and wraps responsively;
- package.json remains unchanged from accepted D1 and preserves `@tanstack/react-table@8.20.5` plus the `js-yaml@4.3.1` override;
- `/ui` production guard remains present;
- provenance now records filtering/visibility/selection capability.

### Remaining verified blockers
1. **Radix Select empty-value bug.** Select-filter UI renders `<SelectItem value="">All</SelectItem>`. Frozen Core Select is Radix-based; empty string is reserved for clearing the selection and is not a valid SelectItem value. Use a non-empty sentinel such as `__all__` and translate it to `undefined` filter state.
2. **Columns control is coupled to search/filter toolbar existence.** The whole toolbar currently renders only when search is enabled or a column has filter metadata. A table can have hideable columns (or row selection summary) without either, making the Columns control/selection summary unreachable. Compute toolbar visibility from search OR filter metadata OR hideable columns OR enabled selection, and render the Columns trigger only when hideable columns exist.
3. **Text column filters are placeholder-only named.** Add an explicit accessible name (`aria-label`/associated label) derived from filter label/column id. Select filter triggers should also have explicit accessible naming rather than relying only on composed trigger text.
4. **Row checkbox fallback names are duplicated.** When `getRowLabel` is absent every checkbox is named `Select row`. Provide a unique meaningful fallback such as `Select row ${row.index + 1}` while preserving consumer-provided row labels.
5. **D1 gallery regression: Status became sortable.** D1 explicitly froze Status as non-sortable. Restore `enableSorting: false` for the gallery Status column.
6. **Gallery data is not generic.** D2 instructions required fictional generic Re:Solve operational records; current gallery includes `Airix Media Group`. Replace brand-specific owners with fictional generic entities/teams while preserving deterministic evidence.
7. **Type/hygiene cleanup.** D2 engine imports unused `Header` and `Badge` and casts filter values with `as string`. Normalize filter values using runtime string narrowing; keep the generic engine free of unnecessary casts. Use `getFilteredRowModel().rows.length` for filtered-empty truth rather than the paginated row model.

### Review classification
D2 architecture is directionally correct and should not be rewritten. One narrow correction should fix Select sentinel handling, decouple toolbar visibility, improve filter/selection names, restore the frozen non-sortable Status gallery contract, genericize gallery records, and clean filter-value typing. No dependency or frozen primitive changes are required.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- TanStack React Table `8.20.5` is the canonical DataTable engine.
- Auth, database/RLS, PWA and domain implementation remain later work.

## Next action
Execute the supervisor-provided FOUND-001C5D2-FIX only. Do not begin C5D3 or another FOUND slice until D2 is accepted/frozen.