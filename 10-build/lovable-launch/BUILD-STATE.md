# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5D1 ACCEPTED/FROZEN — FOUND-001C5D2 NEXT**

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
**ACCEPTED / CANONICAL / FROZEN**

Canonical D1 contracts:
- `@tanstack/react-table` is the single justified DataTable engine dependency at `8.20.5`;
- Re:Solve owns the generic `DataTable<TData, TValue>` boundary;
- rendering composes the frozen semantic Core `Table` primitives;
- enabled TanStack row models are only `getCoreRowModel`, `getSortedRowModel`, and `getPaginationRowModel`;
- client-side sorting is supported;
- `aria-sort` belongs on the relevant `TableHead`/`th` rather than the sort Button;
- sort interaction remains a real Core Button with accessible next-action naming;
- frozen Core Pagination is reused;
- enabled Previous/Next controls are keyboard-operable anchors with client-side `preventDefault` navigation;
- disabled Previous/Next remain frozen non-link states;
- page-size options are 10/20/50 with default 10;
- pagination/footer is suppressed while loading and when no data exists, avoiding `Page 1 of 0`;
- explicit normal/loading/error/empty states exist;
- default empty copy is neutral and does not claim D2 filters/search exist;
- optional `getRowId` is supplied through exact-optional-safe conditional spreading with no forced cast;
- generic engine contains no `any`/`as unknown` workaround;
- bounded horizontal scrolling remains inherited from Core Table;
- `StatePanel` was restored to its frozen public API;
- stray `src/routes/__dev/ui.tsx.demo-parts` artifact was removed;
- `/ui` D1 gallery remains the sole canonical gallery evidence;
- no D2 filtering, visibility, selection or toolbar features are part of D1.

Lovable reported frozen install, build, lint and `tsc --noEmit` passing with only the existing Fast Refresh warnings. GitHub source review verified the accepted contracts; GitHub review does not independently execute Bun.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- TanStack Query is pre-existing.
- TanStack React Table `8.20.5` is the canonical DataTable engine.
- Testing stack not canonical/configured.
- Auth, database/RLS, PWA and domain implementation remain later work.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Simple semantic `Table` remains separate from `DataTable`.
- Keep established Radix/shadcn foundation.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Next action
Proceed with supervisor-issued FOUND-001C5D2 only: global/column filtering, column visibility, row selection, and a restrained operational toolbar on top of the frozen D1 engine. Do not begin server/manual pagination, saved views, URL persistence, shell, auth, database, dashboard, or business-domain screens.