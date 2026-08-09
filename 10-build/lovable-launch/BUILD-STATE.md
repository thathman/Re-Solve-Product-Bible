# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN + CLIENT SHELL FUNCTIONAL CLOSURE ACCEPTED — NON-BLOCKING VISUAL POLISH DEFERRED — FOUND-001G1A PWA INSTALLABILITY ACCEPTED/FROZEN — FOUND-001G1B PARTIALLY IMPLEMENTED BUT BLOCKED: SERVICE WORKER + OFFLINE FALLBACK FILES ARE MISSING FROM CANONICAL MAIN**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client visual authority: `Airix360/AM-Client-Docs` Design System + `Airix360/airixmedia-web`.
- `checklist.design` is UX completeness / pre-freeze QA reference only, never visual authority.
- Owner-supplied mockups/HTML are references unless an interaction/anatomy is explicitly promoted to canonical.
- Legacy/reference app `thathman/Re-Solve` remains untouched absent explicit owner approval.

## Owner build-direction override
**CANONICAL — 2026-08-09**
- Continue building product/foundation logic now.
- Do not spend supervised slices on subjective cosmetic flaws until logic is substantially set.
- Track visual polish for later.
- Visual issues may still block when they affect accessibility, responsive usability, security, legibility, or core interaction correctness.

## Frozen security / architecture
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only; private server functions/routes independently authorize.
- Normal user reads use caller-scoped Supabase + RLS; generated `supabaseAdmin` remains quarantined/unused by application authorization.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Never surface/log raw auth/database/provider/Zod/access errors, tokens, sessions, secrets or privileged values.
- `requireActiveStaff()` / `getAdminAccess()` remain frozen for production Admin authorization.
- `requirePortalAccess()` / Portal parent gate remain frozen for production Portal authorization.
- `requireActiveOrganisation(organisationId)` freshly revalidates exact active organisation access.
- `rs_portal_org` is an untrusted UUID-only context pointer, never authorization evidence.
- No service-role app path, broad RBAC, domain persistence, seed/test identities or public registration yet.
- PWA/offline work must never cache Vault secrets, auth/session material, Supabase responses, server-function responses, organisation-private HTML/data, notifications or other identity-dependent payloads unless a later explicit security design allows a narrow case.

## Frozen foundation / functional surfaces
- FOUND-001A stack/repository accepted.
- FOUND-001B token/UI-stack accepted.
- Core UI C1-C5E accepted/frozen.
- `/ui` remains dev-only.
- Admin shell/routes accepted: Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Portal family accepted: `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Auth routes accepted: `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`.
- `/select-organisation` uses canonical safe redirect and server-revalidated active-org context.
- F0-F3C Auth/identity/RLS/Admin access/Portal access/active-org context accepted/frozen.
- DEV-PREVIEW-001 accepted until intentional demo identities are introduced.

## Visual dialects
### Admin
- Lucid-style Re:Solve operational dialect remains canonical.
- Inter, neutral/graphite structure, restrained Lucide, subtle borders, low shadow, denser operational composition.
- Admin search belongs in expanded Sidebar; collapsed Sidebar uses Search IconButton.
- Admin TopBar has no search and no Àríyá trigger.
- Shared Light/Dark/System control and movable floating Àríyá launcher remain.

### Client-facing
- Auth + Client Portal use the Airix/Re:Solve client dialect.
- Space Grotesk = UI/body; Instrument Serif italic = greetings/display; JetBrains Mono = selected financial/date/identifier/technical metadata.
- Warm-paper light mode + warm-charcoal dark mode; terracotta brand/action accent; info blue, success green, warning amber, danger/coral semantics.
- One strong dark operational anchor is allowed when useful; supplied Home HTML contributes principles, not layout.
- Client phone/tablet uses app-style anatomy + bottom navigation; desktop horizontal navigation starts at `xl`.
- Non-blocking visual refinements are deferred.

## AI + support architecture
- Àríyá is Re:Solve's own AI and exists only inside Re:Solve.
- Àríyá is not Captain and is not powered by Captain.
- Re:Solve human escalation: `Re:Solve -> Àríyá -> dedicated owner/provider Re:Solve-support Chatwoot inbox -> human agent`.
- Captain MUST be disabled on that Re:Solve human-takeover inbox.
- Separately, a client website/property may use its own Chatwoot inbox with Captain enabled when the provider owns that property's support responsibility.
- Do not cross these domains.
- Full authority: `10-build/lovable-launch/AI-SUPPORT-ARCHITECTURE.md`.

## Auth expansion plan
- No public registration.
- Future first-account path: staff/admin creates account -> invite -> onboarding -> set password -> optional passkey -> optional TOTP -> optional Google/GitHub linking -> finish -> authorized destination.
- Google/GitHub must not create public accounts.
- ALTCHA planned for abuse-prone operations.
- WhatsApp auth remains later preflight; Baileys is messaging/connector infrastructure, not canonical auth root.
- Full authority: `10-build/lovable-launch/AUTH-EXPANSION.md`.

## Checklist.design QA rule
- Use relevant Checklist Design checklists for states, focus, responsiveness, dark mode, search, loading/error feedback, copy, forms, support, payments and auth/recovery.
- Do not copy Checklist Design visuals.
- Product Bible + Re:Solve Core/visual dialect remain authoritative.

## CLIENT-PWA-VIS-001 closure
**FUNCTIONALLY ACCEPTED / VISUAL POLISH DEFERRED**
Verified app head before PWA infrastructure: `73c303bcdc71a9a9a3fca907641770e51178bdb4`.
Accepted facts:
- Àríyá mounts invisibly while initial coordinates resolve, avoiding visible load jump.
- final launcher position uses `positionRef` persistence.
- Portal launcher reserves bottom-nav clearance + safe area below 1280px.
- phone/tablet bottom nav is active below `xl`; desktop Portal nav is `xl+`.
- `PORTAL_NAV_ITEMS` is the shared navigation metadata source.
- Home broad desktop composition waits until `xl`.
- StatusBadge treatment and stronger semantic markers exist.
- security/identity/server/DEV-preview boundaries were not changed.

Deferred QA:
- bottom-tab focus treatment recheck against frozen ring + ring-offset contract during accessibility QA.
- subjective design polish remains deferred by owner direction.

## FOUND-001G1A — PWA installability
**ACCEPTED / CANONICAL / FROZEN**
Verified app head: `ec8df572306396215debf5f7cc022618358435de`.
Net files:
- `public/manifest.webmanifest`
- `public/icons/resolve-180.png`
- `public/icons/resolve-192.png`
- `public/icons/resolve-512.png`
- `src/routes/__root.tsx`

Verified facts:
- manifest declares id/name/short_name/description, `/` start URL/scope, standalone display, background/theme colors and `prefer_related_applications: false`.
- root head links manifest + Apple touch icon and light/dark theme-color/mobile metadata.
- icon dimensions verified as 180x180, 192x192 and 512x512.
- temporary centered Re:Solve icon is replaceable and has substantial safe space.
- no dependency/package changes.
- at G1A close there was no service worker, Workbox, Cache API or PWA plugin.
- no auth/identity/authorization/Supabase/domain/shell behavior changed.

G1A does not authorize offline caching of authenticated content.

## FOUND-001G1B — Offline / cache / update boundary
**PARTIALLY IMPLEMENTED / BLOCKED — DO NOT FREEZE**
Latest reviewed app head: `157327548dfb378d7b0a98d819d31aa5d539fc91`.
Compared with G1A head `ec8df572306396215debf5f7cc022618358435de`, final canonical net changes are only:
- `src/lib/pwa/PwaRuntime.tsx` added.
- `src/routes/__root.tsx` modified to mount `PwaRuntime` and a root `Toaster`.

Verified implemented facts:
- `PwaRuntime` listens for online/offline events.
- service-worker registration is gated by `import.meta.env.PROD` and attempts `/sw.js` with scope `/`.
- waiting-worker detection exists and user Refresh sends `SKIP_WAITING`.
- `controllerchange` guards reload with an in-listener one-shot boolean.
- offline/update notices are rendered from the root runtime.
- no new dependency was added by the final net change set.

### Canonical blockers
1. **CRITICAL — `public/sw.js` does not exist on canonical `main`.** Direct GitHub fetch returns 404 and repository search finds no service-worker implementation. The production runtime therefore attempts to register a missing file; no cache policy, fetch strategy, install/activate lifecycle, or `SKIP_WAITING` message handler actually exists.
2. **CRITICAL — `public/offline.html` does not exist on canonical `main`.** Direct GitHub fetch returns 404. Therefore navigation cannot fall back to the promised safe offline document.
3. Because the worker is absent, Lovable's claims about exact precache allowlist, network-only private-data behavior, cache cleanup, offline fallback and never-cached categories are **not implemented in canonical source and cannot be accepted**.
4. `navigator.serviceWorker.register('/sw.js')` currently has no rejection handling. While the missing worker is the primary defect, registration should fail quietly/generically rather than creating an unhandled promise rejection.
5. Root now mounts a global `Toaster` while `/admin` still mounts its own `Toaster`. Review whether one canonical root Toaster should replace the Admin-local instance; avoid duplicated toast containers. Do not expand scope unless duplication is confirmed to affect behavior.

### Required G1B closure
- Commit a real `public/sw.js` implementing the explicit safe-public-asset allowlist only.
- Commit a real self-contained `public/offline.html`.
- Worker navigation must remain network-only with cached offline fallback only after network failure; successful route HTML must never enter Cache Storage.
- non-GET, cross-origin, server-function/API/Supabase/auth/private requests remain network-only and uncached.
- worker install cache contains only explicit safe assets from G1A plus offline page.
- activate deletes prior Re:Solve worker cache versions and claims clients.
- no automatic `skipWaiting()` at install; only explicit `SKIP_WAITING` message invokes it.
- add generic SW registration failure handling without raw logging or user-secret exposure.
- verify actual production output serves `/sw.js` and `/offline.html`.

## PWA security boundary
- One Re:Solve origin/manifest for now.
- No custom install banner required at foundation stage.
- Authenticated navigation/document responses, server-function/RPC responses, Supabase/API responses, auth callbacks/recovery, organisation-private data, Vault/secrets, notifications and identity-dependent payloads are network-only and must not enter Cache Storage.
- Service-worker cache uses positive allowlist only; unknown requests are network-only.
- Offline business-data access is not a FOUND-001 requirement.
- No Workbox, PWA plugin, background sync, offline mutations or business-data IndexedDB in G1B.

## FOUND-001 remaining closure
Completed/frozen: A stack/repo, B UI stack/tokens, C Core C1-C5E, D/E shell architecture, F auth/identity/RLS/authorization/org context, DEV preview, shell functional closure, G1A installability.

Still required:
1. **FOUND-001G1B-FIX** — make canonical service worker/offline fallback real and verify cache/update boundary.
2. FOUND-001G accessibility/device/Checklist QA.
3. FOUND-001G automated tests + CI + engineering hardening.
4. **FOUND-001R** — integrated review + self-host check + reconcile original demo-user criterion + final PASS/CONDITIONAL/FAIL record.

Rich Admin Home and real Client Properties/Projects/Support/Billing remain post-FOUND-001 work.

## Sequencing
1. **FOUND-001G1B-FIX — Service Worker + Offline Files Closure**.
2. inspect/freeze G1B.
3. accessibility/device/Checklist QA.
4. automated tests/CI/engineering hardening.
5. FOUND-001R integrated closure.
6. after FOUND-001: continue operational/domain logic; return to deferred visual polish when appropriate.

## Next action
Run **FOUND-001G1B-FIX** only. Do not proceed to accessibility/CI until the actual worker and offline fallback are committed and verified.