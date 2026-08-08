# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY-GATE-001 ACCEPTED/CLOSED — FOUND-001C5D READY**

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

### Accepted package state
`package.json` direct TanStack declarations are restored to the accepted foundation ranges:
- `@tanstack/react-router`: `^1.170.18`
- `@tanstack/react-start`: `^1.168.32`
- `@tanstack/router-plugin`: `^1.168.23`

No direct `@tanstack/router-core` dependency remains.
No direct `js-yaml` application dependency remains.

A top-level Bun override is canonical for the current advisory remediation:
```json
"overrides": {
  "js-yaml": "4.3.1"
}
```

The override exists solely to force compatible transitive 4.x consumers onto the patched `js-yaml@4.3.1` release. Re-evaluate/remove it later when upstream dependencies no longer require the override; do not treat it as permanent product architecture.

### Advisory closure
The user/Lovable remediation report confirms:
- `bun why js-yaml` resolves all installed 4.x instances to `4.3.1`;
- `js-yaml@4.3.0` remains: NO;
- dependency/security scan clears `GHSA-5p4m-2wfm-xmqj`;
- remaining High/Critical findings: NONE;
- frozen install/build/lint/`tsc --noEmit`: PASS;
- no C1-C5C source changes were required.

GitHub source review verified the accepted direct package declarations and top-level override. GitHub code search may retain stale indexed matches from earlier commits, so current-lock security closure relies on the returned `bun why` + post-remediation scan evidence together with current package configuration.

### Generated route tree
`src/routeTree.gen.ts` differs from the earlier accepted baseline only by TanStack-generated type registration for the existing routes. No route source or route behavior was intentionally added by the security gate. Treat this generated diff as non-blocking; do not hand-edit generated route behavior.

### AspectRatio provenance
Canonical provenance distinguishes:
- declared package range: `^1.1.8`;
- resolved scanner version at the C5C/security review: `1.1.15`;
- license: MIT;
- pre-existing dependency;
- first Re:Solve Core consumption: FOUND-001C5C.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- TanStack Query is pre-existing.
- TanStack Table is not yet a direct dependency and must not be assumed installed before C5D preflight.
- Testing stack not canonical/configured.
- Auth, database/RLS, PWA and domain implementation remain later work.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Keep the established Radix foundation; no wholesale Base UI/React Aria migration.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.
- Simple semantic `Table` remains separate from the upcoming `DataTable` system.

## Next action
Proceed with supervisor-issued FOUND-001C5D — DataTable Foundation. Keep the slice generic and infrastructure-only: no business-domain screen, no server data fetching, no auth, no database, no shell/dashboard work. Preflight the actual package state before adding TanStack Table; if it is absent, adding `@tanstack/react-table` is allowed only as the explicitly justified C5D dependency.