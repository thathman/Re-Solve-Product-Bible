# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN + CLIENT SHELL FUNCTIONAL CLOSURE ACCEPTED — NON-BLOCKING VISUAL POLISH DEFERRED — FOUND-001G1A PWA INSTALLABILITY ACCEPTED/FROZEN — FOUND-001G1B OFFLINE/CACHE/UPDATE BOUNDARY ACCEPTED/FROZEN — FOUND-001G2 ACCESSIBILITY/DEVICE QA IMPLEMENTED, CONDITIONAL ON TINY FOCUS/LIVE-REGION CLOSURE — NEXT AFTER CLOSURE: FOUND-001G3 TESTS / CI / ENGINEERING HARDENING**

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

Subjective design polish remains deferred by owner direction.

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
**ACCEPTED / CANONICAL / FROZEN**
Latest verified app head: `0db19adc419d1b18cf1f29b3efedf387321b9990`.
Final G1B runtime files include:
- `public/offline.html`
- `public/sw.js`
- `src/lib/pwa/PwaRuntime.tsx`
- root-mounted canonical `PwaRuntime`/Toaster from the earlier G1B slice
- Admin-local duplicate Toaster removed

Verified accepted facts:
- cache name is `resolve-public-v1`.
- exact positive precache allowlist is only `/offline.html`, `/manifest.webmanifest`, `/favicon.ico`, `/icons/resolve-180.png`, `/icons/resolve-192.png`, `/icons/resolve-512.png`.
- install precaches only that explicit safe list; no dynamic unknown-response cache path exists.
- activate deletes only old `resolve-public-*` cache versions and calls `clients.claim()`.
- `SKIP_WAITING` remains explicit/message-driven; install never activates a waiting worker automatically.
- non-GET requests are network-only.
- cross-origin requests are network-only.
- explicit public allowlist assets are cache-first.
- navigation/HTML is network-first and falls back to cached `/offline.html` only on network failure; successful navigation responses are never written to Cache Storage.
- all other requests are network-only.
- no route blacklist is needed or used; `/admin`, auth routes, Portal routes and organisation-selection navigation can receive only the generic offline fallback after network failure while their real responses remain uncached.
- `PwaRuntime` registers the worker only in production and uses a fixed generic registration-failure diagnostic.
- first worker activation/controller acquisition cannot force a page reload: `controllerchange` reload is gated by `refreshRequestedRef`, which is set only by the user's explicit Refresh action before sending `SKIP_WAITING`.
- user-requested update reload remains one-shot.
- no authenticated/private HTML, server-function/RPC response, Supabase/API response, auth/recovery payload, organisation/profile/project/property/billing/support data, notification, Àríyá/Chatwoot content, Vault data, token or session material is authorized to enter Cache Storage.
- no Workbox/PWA plugin, background sync, offline mutation or business-data IndexedDB exists.
- final G1B change set did not modify auth, identity, authorization, RLS, Supabase, database, Admin/Portal product behavior or DEV-PREVIEW-001.

Security-memory handling:
- canonical durable source remains `10-build/lovable-launch/SECURITY-MEMORY.md`.
- Lovable reported `mem://security/rules.md` synchronized with that policy plus an explicit authenticated-navigation no-cache rule; `mem://` is editor/project memory and is not independently GitHub-verifiable.

## FOUND-001G2 — Accessibility / Device / Checklist QA
**IMPLEMENTED / FUNCTIONALLY GOOD / CONDITIONAL ON TINY ACCESSIBILITY CLEANUP — DO NOT FULLY FREEZE YET**
Latest reviewed app head: `b018bb9c0912dc61e7adf70e50ed4253685f7a94`.
Compared with G1B head `0db19adc419d1b18cf1f29b3efedf387321b9990`, net changed files are:
- `public/offline.html`
- `src/components/core/feedback/Alert.tsx`
- `src/components/shell/admin/AdminShell.tsx`
- `src/components/shell/portal/PortalBottomNav.tsx`
- `src/components/shell/portal/PortalShell.tsx`
- `src/lib/pwa/PwaRuntime.tsx`
- `src/routes/__root.tsx`
- `src/routes/select-organisation.tsx`

Verified accepted facts:
- both Admin and Portal now expose a visible-on-focus `Skip to main content` link targeting the existing single main landmark.
- Portal bottom nav now has `aria-label="Primary"`, retains `aria-current="page"`, adds ring-offset classes, and marks the decorative active indicator `aria-hidden`.
- PWA offline/update notices now constrain phone width, account for bottom safe area, and gate entrance animation behind `motion-safe`.
- `public/offline.html` adds a visible `:focus-visible` treatment for Try again.
- organisation selection improves radio-label association and focus-within visibility.
- existing Core `FormField` + `Input` already provide label/control association, required/invalid/description wiring; current Login already uses `type="email"`, `autoComplete="email"`, `autoComplete="current-password"`, semantic password visibility control and keyboard form submission.
- Lovable's report says LoginForm was hardened in this slice, but canonical compare shows LoginForm itself was not changed; its key semantics were already present, so this is a reporting overstatement rather than a functional blocker.
- no auth behavior, authorization, RLS, Supabase, DB, PWA cache policy, routes or DEV-preview security boundary changed.

### Tiny G2 closure items
1. `src/routes/__root.tsx` introduced hard-coded `focus-visible:ring-2 focus-visible:ring-offset-2` on Not Found/Error actions. Replace these with the exact frozen variable-based focus-visible contract; do not establish a second focus system.
2. Make both skip-link targets explicitly programmatically focusable with `tabIndex={-1}` on the existing Admin and Portal main landmarks so hash-based skip focus is robust across browser/screen-reader combinations. Do not add another main landmark.
3. `Alert` now explicitly adds `aria-live` while `role="alert"` / `role="status"` already supply assertive/polite live-region semantics. Remove the redundant explicit `aria-live` unless there is a demonstrated compatibility reason; avoid duplicate/noisy announcements.
4. Lovable's phrase "fixable lint" is ambiguous. G2 closure requires plain `bun run lint` to exit 0 without relying on a write/fix mode.

These are accessibility-contract fixes, not subjective visual polish.

## FOUND-001 remaining closure
Completed/frozen: A stack/repo, B UI stack/tokens, C Core C1-C5E, D/E shell architecture, F auth/identity/RLS/authorization/org context, DEV preview, shell functional closure, G1A installability, G1B offline/cache/update boundary.

Still required:
1. **FOUND-001G2-FIX** — tiny focus/skip-target/live-region cleanup + confirm plain lint success.
2. **FOUND-001G3** — automated tests + CI + engineering hardening.
3. **FOUND-001R** — integrated review + self-host check + reconcile original demo-user criterion + final PASS/CONDITIONAL/FAIL record.

Rich Admin Home and real Client Properties/Projects/Support/Billing remain post-FOUND-001 work.

## Sequencing
1. **FOUND-001G2-FIX — tiny accessibility closure only**.
2. inspect/freeze G2.
3. FOUND-001G3 automated tests/CI/engineering hardening.
4. FOUND-001R integrated closure.
5. after FOUND-001: continue operational/domain logic; return to deferred visual polish when appropriate.

## Next action
Run **FOUND-001G2-FIX** only. Do not use it for visual redesign or new product behavior.