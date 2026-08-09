# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN + CLIENT SHELL FUNCTIONAL CLOSURE ACCEPTED — NON-BLOCKING VISUAL POLISH DEFERRED — FOUND-001G1A PWA INSTALLABILITY ACCEPTED/FROZEN — FOUND-001G1B IMPLEMENTED BUT CONDITIONAL: TWO SMALL LIFECYCLE/OFFLINE-FALLBACK FIXES REQUIRED BEFORE FREEZE**

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
- Canonical concise security memory: `10-build/lovable-launch/SECURITY-MEMORY.md`. Lovable/project `@security-memory` should mirror it rather than invent parallel rules.

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
- no auth/identity/authorization/Supabase/domain/shell behavior changed.

G1A does not authorize offline caching of authenticated content.

## FOUND-001G1B — Offline / cache / update boundary
**IMPLEMENTED / SECURITY BOUNDARY GOOD / CONDITIONAL — TWO SMALL LOGIC FIXES REQUIRED**
Latest reviewed app head: `c0b87950efd495d97b26019625635fc373bd9bf6`.
Compared with prior G1B runtime head `157327548dfb378d7b0a98d819d31aa5d539fc91`, final net changes are exactly:
- `public/offline.html` added.
- `public/sw.js` added.
- `src/lib/pwa/PwaRuntime.tsx` modified.
- `src/routes/admin.tsx` modified to remove duplicate local Toaster.

Verified accepted facts:
- `public/sw.js` and `public/offline.html` now physically exist in canonical source.
- cache name is `resolve-public-v1`.
- explicit precache assets are only `/offline.html`, `/manifest.webmanifest`, `/favicon.ico`, `/icons/resolve-180.png`, `/icons/resolve-192.png`, `/icons/resolve-512.png`.
- install uses `cache.addAll()` for that explicit list; a failed precache rejects installation rather than silently creating a partial worker.
- activate deletes only prior `resolve-public-*` versions and then calls `clients.claim()`.
- `SKIP_WAITING` is message-driven only; install does not call `skipWaiting()` automatically.
- safe public assets are cache-first; the worker does not dynamically add unknown fetched responses to Cache Storage.
- successful navigation/document responses are returned from network and never stored.
- all non-allowlisted non-navigation requests are network-only.
- offline document is self-contained and contains no user/organisation/private data.
- registration is production-only and failure is handled with a fixed generic console label rather than raw error details.
- root Toaster is canonical; Admin-local duplicate was removed.
- no dependency, auth, identity, authorization, Supabase, RLS, DB, shell, DEV-preview or domain change was introduced.

### G1B closure blockers
1. **Update reload must be explicitly user-gated.** Current `PwaRuntime` reloads on any `navigator.serviceWorker.controllerchange`. Because `sw.js` calls `clients.claim()` during activation, first-time worker activation can trigger `controllerchange` without the user choosing Refresh. MDN documents that `clients.claim()` causes `controllerchange` for newly controlled clients. Keep `clients.claim()`, but reload only when a local `refreshRequested` ref/flag was set immediately before posting `SKIP_WAITING` from the user action. First install/controller acquisition must not force a reload.
2. **Offline fallback ordering is wrong for sensitive navigation paths.** `NEVER_CACHE_URLS` returns before navigation handling, so `/admin`, `/login`, `/auth/*`, `/select-organisation`, etc. fail directly when offline instead of receiving the generic `/offline.html`. The blacklist is unnecessary because caching is already positive-allowlist only. Remove it, or handle navigation before any no-cache early return. Sensitive navigation may receive the generic cached offline document after network failure while still never being cached itself.

### G1B security rule
- Positive cache allowlist is the authority. Unknown requests are network-only.
- No authenticated/private route HTML, server-function/RPC response, Supabase/API response, auth/recovery payload, organisation/profile/project/property/billing/support data, notification, Àríyá/Chatwoot content, Vault data, token or session material may enter Cache Storage.
- No offline mutation, background sync or business-data IndexedDB exists at foundation stage.

## FOUND-001 remaining closure
Completed/frozen: A stack/repo, B UI stack/tokens, C Core C1-C5E, D/E shell architecture, F auth/identity/RLS/authorization/org context, DEV preview, shell functional closure, G1A installability.

Still required:
1. **FOUND-001G1B-FINAL** — user-gated update reload + universal generic navigation offline fallback without caching private HTML.
2. FOUND-001G accessibility/device/Checklist QA.
3. FOUND-001G automated tests + CI + engineering hardening.
4. **FOUND-001R** — integrated review + self-host check + reconcile original demo-user criterion + final PASS/CONDITIONAL/FAIL record.

Rich Admin Home and real Client Properties/Projects/Support/Billing remain post-FOUND-001 work.

## Sequencing
1. **FOUND-001G1B-FINAL — two logic corrections only**.
2. inspect/freeze G1B.
3. accessibility/device/Checklist QA.
4. automated tests/CI/engineering hardening.
5. FOUND-001R integrated closure.
6. after FOUND-001: continue operational/domain logic; return to deferred visual polish when appropriate.

## Next action
Run **FOUND-001G1B-FINAL** only. Also align Lovable/project `@security-memory` with `10-build/lovable-launch/SECURITY-MEMORY.md`; do not weaken any existing stricter rule without explicit review.