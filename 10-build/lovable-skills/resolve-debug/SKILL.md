---
name: resolve-debug
description: Use when a Re:Solve feature, build slice, connector, permission path, PWA state, automation, or UI interaction is broken, inconsistent, flaky, or regressed and needs root-cause diagnosis rather than cosmetic patching.
---

# Re:Solve Debug

## Start from the flow
1. Restate expected Product Bible behavior.
2. Reproduce the full failing user flow and affected actor/scope.
3. Identify whether failure is UI, state/query, domain/service, auth/permission, data, connector/provider, job/event, PWA/cache, or environment.
4. Inspect the narrowest evidence needed.

## Rules
- fix root cause, not just visible symptom;
- do not weaken permission/security checks to make a test pass;
- do not replace real error handling with swallowed exceptions;
- preserve data provenance and provider boundaries;
- avoid introducing duplicate business truth or direct provider/database shortcuts;
- verify stale/offline/retry behavior when relevant;
- use correlation/event ids where async flows require them.

## Regression
Add or improve the smallest meaningful automated coverage for the failure: unit/domain, component, integration, permission-negative, or end-to-end as appropriate.

## Adjacent verification
Check normal, loading, empty, error, permission-denied and retry paths immediately adjacent to the fix. For connector/event bugs, verify idempotency and duplicate delivery. For PWA bugs, verify reconnect/update/cache behavior.

## Output
Report root cause, exact fix, evidence/tests, adjacent behavior checked and any Product Bible ambiguity discovered. Do not quietly redesign the feature while debugging.