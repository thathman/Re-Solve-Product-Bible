---
name: airix-pwa
description: Review or implement Re:Solve mobile, installability, offline, push, caching, service-worker, and app-update behavior for PWA readiness.
---

# Airix PWA

Read `03-platform/pwa.md` and the relevant feature spec.

Check:
- installability
- manifest and icons
- responsive composition
- safe-area and touch behavior
- service-worker update lifecycle
- offline shell/fallback
- data caching class
- online-only sensitive actions
- push/deep-link behavior where in scope
- retry behavior for safe deferred actions
- reduced connectivity states
- secret and Vault cache prohibitions

The Client Portal should receive especially strong phone ergonomics.
Admin must remain usable on mobile for essential actions even when dense workflows are optimized for larger screens.

Do not silently cache sensitive business data merely to make a page appear offline-capable.

Before completion verify phone, tablet, desktop, install/update behavior, offline state, and return-to-online behavior relevant to the slice.
