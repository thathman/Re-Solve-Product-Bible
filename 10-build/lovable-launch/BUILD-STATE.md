# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY-GATE-001 CONDITIONAL (DEPENDENCY REMEDIATION STILL REQUIRED BEFORE C5D)**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Accepted foundation
FOUND-001A, FOUND-001B and FOUND-001C1-C5C are accepted/canonical/frozen. C5C includes the Card family, semantic Table family and thin AspectRatio wrapper. Do not reopen frozen UI slices during the security gate.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.

## Security memory
**ACCEPTED / CANONICAL**
The scanner-oriented Security Memory supplied after SECURITY-GATE-001 is accepted. It correctly describes Re:Solve as a multi-tenant Business Operating System, keeps authentication/authorization server-authoritative, explicitly states that final auth/RLS/Vault/Action Registry are not yet implemented, lists security invariants, and records no accepted vulnerability exceptions. No secret material was reported.

Do not reopen the memory merely because a completion message says it was updated. Re-review only if Lovable surfaces different text.

## SECURITY-GATE-001 — Dependency remediation
**STATUS: CONDITIONAL — NOT CLOSED**

### Advisory
User scan and supervisor verification confirm GitHub-reviewed High advisory `GHSA-5p4m-2wfm-xmqj` for `js-yaml`:
- affected 4.x range: `>=4.0.0,<4.3.1`;
- patched 4.x: `4.3.1`;
- impact: quadratic CPU consumption / availability DoS when parsing attacker-influenced YAML.

### Current reported graph
Lovable reported:
- `js-yaml@4.3.1` direct/top-level;
- `js-yaml@4.3.0` remains transitive through `@eslint/eslintrc` and `xmlbuilder2` / `@tanstack/start-plugin-core`;
- no application source currently parses user-controlled YAML;
- remaining exposure is dev/build-time, but the High scanner finding remains unresolved.

### Verified repository drift
Compared with accepted C5C baseline app commit `946763125df3facf208cb68c3d278ff346898d3a`, current `main` changed:
- `package.json`;
- `bun.lock`;
- `docs/ui-sources.md`;
- generated `src/routeTree.gen.ts`.

Current `package.json` contains unauthorized direct dependency drift beyond the requested security investigation:
- `@tanstack/react-router`: accepted `^1.170.18` → current `^1.170.21`;
- `@tanstack/react-start`: accepted `^1.168.32` → current `^1.168.38`;
- new direct `@tanstack/router-core`: `^1.171.18`;
- new direct `js-yaml`: `4.3.1`.

This conflicts with the gate instruction to STOP before changing direct TanStack packages. Adding direct `js-yaml@4.3.1` also did not remediate the vulnerable transitive `4.3.0` copy, so the remaining High finding means the gate cannot be accepted.

### Preferred remediation direction
Bun officially supports top-level `overrides`/`resolutions` for metadependencies. The reported vulnerable transitive constraints (`^4.3.0` from ESLint and `^4.1.1` from xmlbuilder2) are semver-compatible with `4.3.1`, so the next narrow pass should:
1. restore the accepted direct TanStack dependency declarations;
2. remove unnecessary direct `@tanstack/router-core` and direct `js-yaml` dependencies;
3. use a top-level Bun-compatible `overrides` entry for `js-yaml: 4.3.1` only if actual `bun why` confirms every 4.x consumer accepts it;
4. regenerate `bun.lock` with Bun;
5. prove `bun why js-yaml` resolves every 4.x copy to `4.3.1`;
6. rerun build/lint/type and the dependency scan;
7. STOP if any upstream constraint prevents the override or if a direct TanStack update is still required.

Do not mark the remaining High advisory as an accepted risk.

### AspectRatio provenance
Provenance correction is accepted in principle: declared range is `^1.1.8`, while the supplied dependency scan reports resolved `1.1.15`. Preserve that distinction. No AspectRatio source change is needed.

## Current architecture facts
- TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3.
- Tailwind 4.2.1 declaration baseline.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- Testing stack not canonical/configured.
- Auth, database/RLS, PWA and domain implementation remain later work.

## Next action
Execute the supervisor-provided SECURITY-GATE-001-FIX only. Do not begin FOUND-001C5D/DataTable until the dependency scan is clean of this High finding or a genuine upstream blocker is returned for owner/supervisor review.