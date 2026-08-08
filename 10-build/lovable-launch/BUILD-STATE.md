# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5D1-D2 ACCEPTED/FROZEN — FOUND-001C5D3 NEXT**

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

Canonical D2 contracts:
- `getFilteredRowModel` is added on top of the frozen D1 engine;
- internal global-filter, column-filter, visibility and row-selection state remain client-side and non-persistent;
- typed TanStack `ColumnMeta` supports Re:Solve text/select filter metadata;
- select filters use a non-empty `__all__` sentinel and translate it to `undefined` filter state rather than using an invalid empty Radix SelectItem value;
- filter values are runtime-narrowed without `any`, `as unknown`, or forced string casts in the DataTable engine;
- toolbar visibility is driven by search OR filterable columns OR hideable columns OR enabled selection;
- Columns menu renders only when hideable columns exist and respects TanStack `enableHiding: false`;
- global search, text filters and select-filter triggers have explicit accessible names;
- row selection is opt-in, uses current-page select-all, supports indeterminate state, and selected rows use the existing `data-state="selected"` visual contract;
- consumer `getRowLabel` is preferred for row checkbox naming with a unique index-based fallback;
- selected-row summary is informational only; no bulk mutation actions are part of Foundation D2;
- filtered-empty truth uses the filtered row model, distinct from source-empty state;
- Clear resets only global/column filters and preserves sorting, page size, visibility and selection;
- filter changes reset the page index to the first page;
- D1 Status gallery column remains non-sortable; Property, Monthly Cost and Last Checked remain sortable;
- gallery records are fictional generic operational data, not Airix/client data;
- package.json/bun.lock remain unchanged from D1; `@tanstack/react-table@8.20.5` and the `js-yaml@4.3.1` override remain canonical;
- provenance records filtering, visibility and row-selection capability;
- `/ui` production guard remains intact.

Lovable reported frozen install, build, lint and `tsc --noEmit` passing. GitHub source review verified the accepted contracts; GitHub review does not independently execute Bun.

### Known D3 closure item
Once column visibility exists, loading/empty/filtered-empty DataTable cells should span the current visible leaf-column count rather than the original `columns.length`. Carry this into FOUND-001C5D3 rather than reopening D2.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- TanStack React Table `8.20.5` is the canonical DataTable engine.
- Auth, database/RLS, PWA and domain implementation remain later work.

## Next action
Proceed with supervisor-issued FOUND-001C5D3 — DataTable closure/audit only. Resolve structural residuals such as visibility-aware state colSpan and decide which advanced TanStack capabilities belong in Foundation versus later domain implementation. Do not begin server/manual data mode, saved views, URL persistence, bulk mutations, shell, auth, database or dashboard work unless explicitly approved by the supervisor.