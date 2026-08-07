---
name: airix-release
description: Verify a Re:Solve Lovable build slice against acceptance criteria before it is considered complete.
---

# Airix Release

Before declaring a slice complete:
- compare implementation against cited Product Bible specs
- verify acceptance criteria
- verify in-scope/out-of-scope discipline
- run available type, lint, test, and build checks
- verify permission and denial paths
- verify loading, empty, error, and success states
- verify phone/tablet/desktop behavior
- verify PWA/offline expectations where relevant
- verify accessibility basics
- verify migrations/data changes are intentional
- run security and portability checks when relevant
- identify any spec drift

Return:
- pass/fail by acceptance criterion
- checks performed
- known limitations
- regressions found/fixed
- deferred work
- any Product Bible update required

Do not mark a slice complete merely because the happy path renders.
