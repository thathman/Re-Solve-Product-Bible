---
name: resolve-release
description: Use at the end of every Re:Solve Lovable build slice to run the go/no-go completion review across Product Bible acceptance criteria, tests, security, responsive/PWA, accessibility, Core UI/design quality, portability, and scope drift.
---

# Re:Solve Release Review

Before declaring a slice complete, report:
- acceptance criteria status;
- type/lint/test/build checks available in the chosen stack;
- negative permission/security checks;
- phone/tablet/desktop/PWA review;
- accessibility review;
- Core UI/component reuse and Component Gallery updates;
- Sidebar/TopBar/avatar/notifications/Àríyá regression when shell is affected;
- loading/empty/error/stale/offline states;
- provenance/sync correctness where relevant;
- migration/demo-data impact;
- portability/self-host concerns;
- known limitations;
- Product Bible contradictions/drift;
- explicit adjacent features left unbuilt.

Functional correctness alone is not release completion. Return PASS, CONDITIONAL PASS, or FAIL with blockers.
