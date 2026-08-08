# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5D1 CONDITIONAL (NARROW ACCESSIBILITY/HYGIENE FIX REQUIRED)**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and FOUND-001C1-C5C are accepted/canonical/frozen. C5C includes the Card family, semantic Table family and thin AspectRatio wrapper. Do not reopen frozen UI slices without a concrete regression.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.

## Security memory
**ACCEPTED / CANONICAL**
The scanner-oriented Re:Solve Security Memory is canonical. It describes Re:Solve as a multi-tenant Business Operating System, keeps authentication/authorization server-authoritative, explicitly states that final auth/RLS/Vault/Action Registry are not yet implemented, lists business-logic security invariants, and records no accepted vulnerability exceptions.

Do not reopen the memory merely because a completion message says it was updated. Re-review only if Lovable surfaces different text.

## SECURITY-GATE-001 — Dependency remediation
**ACCEPTED / CLOSED**

Canonical package security state:
- `@tanstack/react-router`: `^1.170.18`
- `@tanstack/react-start`: `^1.168.32`
- `@tanstack/router-plugin`: `^1.168.23`
- no direct `@tanstack/router-core`
- no direct `js-yaml`
- top-level Bun override: `"js-yaml": "4.3.1"`
- `GHSA-5p4m-2wfm-xmqj` cleared in the accepted remediation scan
- no remaining High/Critical findings reported.

The override is temporary supply-chain remediation and should be re-evaluated when upstream dependencies no longer need it.

## FOUND-001C5D1 — DataTable Core Foundation
**STATUS: CONDITIONAL — NARROW ACCESSIBILITY/HYGIENE FIX REQUIRED**

### Verified implementation
- `@tanstack/react-table` is now the justified C5D1 direct dependency at `8.20.5`;
- generic Re:Solve `DataTable<TData, TValue>` exists;
- engine enables only `getCoreRowModel`, `getSortedRowModel`, and `getPaginationRowModel`;
- frozen simple semantic Table is reused for rendering;
- client sorting exists;
- frozen Core Pagination family is reused;
- page-size selector exists with 10/20/50;
- normal/loading/error/empty presentation exists;
- bounded horizontal scrolling remains inherited from Core Table;
- D1 gallery evidence exists;
- `js-yaml` override remains present;
- no C5D2 filtering/visibility/selection engine was intentionally added.

### Remaining verified blockers
1. **`aria-sort` is attached to the sort Button instead of the column-header cell.** `aria-sort` belongs on the relevant column/row header semantic element. Move the current sort state to `TableHead`/`th`; keep the button name describing the next action.
2. **Enabled Previous/Next controls are anchors without `href`.** Frozen `PaginationPrevious`/`PaginationNext` render a normal `<a>` when enabled. C5D1 currently provides only `onClick`, producing anchors without link keyboard semantics. Compose an actually keyboard-operable enabled control without modifying frozen Pagination implementation. A small `href` + preventDefault client-pagination approach is acceptable; another semantic composition using the existing Pagination family is acceptable if it preserves disabled non-link behavior.
3. **Empty-state copy references filters/search that do not exist in D1.** Replace with neutral D1-accurate copy such as no records/data available. Do not introduce filtering/search.
4. **Empty data can produce `Page 1 of 0`.** Do not render nonsensical page information/navigation when there are zero rows; keep the empty state bounded and understandable.
5. **`getRowId` uses an unnecessary forced function cast and is always supplied to `useReactTable`.** With `exactOptionalPropertyTypes`, conditionally spread `getRowId` only when provided. No cast is needed.
6. **Frozen `StatePanel` was modified only to widen optional action properties with `| undefined`.** Revert `StatePanel.tsx` to the accepted C5C/C4 public type contract. DataTable already conditionally constructs action props and does not need this frozen API change.
7. **Stray file `src/routes/__dev/ui.tsx.demo-parts` was committed.** It duplicates gallery data/helpers, includes an `any` status map, and is not a canonical source file. Delete it; keep the actual `/ui` source as the sole gallery evidence.

### Additional scope observation
`src/lib/theme/contract.ts` differs from the earlier C5C baseline by adding a nested try/catch around `localStorage.getItem`. This is outside C5D1 scope. Do not modify it in the C5D1 fix unless the supervisor explicitly reopens it; the narrow fix should focus only on verified D1 regressions above.

### Package/security state
Current `package.json` correctly includes `@tanstack/react-table: 8.20.5` and preserves the `js-yaml: 4.3.1` top-level override. No second table dependency is justified.

### Review classification
The DataTable architecture is directionally correct and should not be rewritten. One narrow correction should fix semantic sorting, keyboard-operable pagination, neutral empty/pagination state behavior, exact-optional `getRowId`, restore frozen StatePanel, and remove the stray demo artifact. Then stop for final D1 review.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- TanStack Query is pre-existing.
- TanStack React Table `8.20.5` is the C5D1 table engine.
- Testing stack not canonical/configured.
- Auth, database/RLS, PWA and domain implementation remain later work.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Simple semantic `Table` remains separate from `DataTable`.
- Keep established Radix/shadcn foundation.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Next action
Execute the supervisor-provided FOUND-001C5D1-FIX only. Do not begin C5D2 until D1 is accepted/frozen.