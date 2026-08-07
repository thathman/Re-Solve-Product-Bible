---
name: resolve-pwa
description: Use when implementing or reviewing Re:Solve installability, service-worker behavior, offline/stale states, cache policy, push/deep links, reconnect/update lifecycle, safe areas, or PWA-specific mobile behavior.
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

PWA is a product capability, not permission to cache authenticated data indiscriminately.
