---
name: resolve-pwa
description: Review or implement Re:Solve installability, responsive/mobile behavior, offline state, caching, push/deep-links, safe areas, and service-worker lifecycle.
---

# Re:Solve PWA

Verify:
- installability/manifest;
- phone/tablet/laptop/desktop composition;
- deliberate mobile navigation rather than hidden desktop sidebar;
- safe-area/touch behavior;
- online-only sensitive actions;
- explicit cache data classes;
- no Vault secret/confidential-content unsafe caching;
- offline fallback and stale indicators;
- update lifecycle;
- push/deep-link behavior where in scope;
- queued replay only for actions whose idempotency/conflict behavior is safe;
- reconnect/sync failure/success state.
