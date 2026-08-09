# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN + CLIENT SHELL FUNCTIONAL CLOSURE ACCEPTED — OWNER HAS DEFERRED NON-BLOCKING VISUAL POLISH UNTIL PRODUCT LOGIC IS SET — FOUND-001G1A PWA INSTALLABILITY ACCEPTED/FROZEN — NEXT: FOUND-001G1B OFFLINE/CACHE/UPDATE BOUNDARY**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Client-facing visual authority: `Airix360/AM-Client-Docs` Design System + `Airix360/airixmedia-web`
- `checklist.design` is a UX completeness / pre-freeze QA reference only, never a visual authority.
- Owner-supplied mockups/HTML are reference material unless an interaction/anatomy is explicitly promoted to canonical.
- Legacy/reference app: `thathman/Re-Solve` — untouched absent explicit owner approval.

## Owner build-direction override
**CANONICAL — 2026-08-09**
- Continue building product/foundation logic now.
- Do not spend more supervised slices on cosmetic design flaws until logic is substantially set.
- Track visual polish for later.
- Visual issues may still block a slice only when they materially affect accessibility, responsive usability, security, information legibility, or core interaction correctness.

## Frozen security / architecture
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only. Private server functions/routes independently authorize at their server boundary.
- Normal user reads use caller-scoped Supabase + RLS; generated `supabaseAdmin` remains quarantined/unused by application authorization.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Raw auth/database/provider/Zod/access errors, tokens, sessions, secrets and privileged values are not logged or surfaced.
- `requireActiveStaff()` / `getAdminAccess()` remain frozen for production Admin authorization.
- `requirePortalAccess()` / Portal parent access gate remain frozen for production Portal authorization.
- `requireActiveOrganisation(organisationId)` freshly revalidates exact active organisation access.
- `rs_portal_org` is an untrusted UUID-only context pointer, never authorization evidence.
- No service-role application path, broad RBAC, domain persistence, seed/test identities or public registration exists yet.
- PWA/offline work must never cache Vault secrets, auth/session material, Supabase responses, server-function responses, organisation-private HTML/data, or other identity-dependent payloads unless a later explicit security design allows a narrowly scoped case.

## Frozen foundation / functional surfaces
- FOUND-001A stack/repository foundation accepted.
- FOUND-001B token/UI-stack foundation accepted.
- Core UI C1-C5E accepted/frozen.
- `/ui` remains dev-only.
- Admin shell architecture/routes accepted: Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Portal family accepted: `/_portal` wrapping `/`, `/properties`, `/projects`, `/support`, `/billing`.
- Auth routes accepted: `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`.
- `/select-organisation` uses canonical safe redirect and server-revalidated active-organisation context.
- F0-F3C Auth/identity/RLS/Admin access/Portal access/active-organisation context accepted/frozen.
- DEV-PREVIEW-001 accepted until intentional demo identities are introduced.

## Visual dialects
### Admin
- Lucid-style Re:Solve operational dialect remains canonical.
- Inter typography, neutral/graphite structure, restrained Lucide, subtle borders, low shadow, denser operational composition.
- Admin search belongs in expanded Sidebar; collapsed Sidebar uses search IconButton.
- Admin TopBar has no search and no Àríyá trigger.
- Shared Light/Dark/System control and movable floating Àríyá launcher remain.

### Client-facing
- Auth + Client Portal use the Airix/Re:Solve client dialect.
- Space Grotesk = UI/body; Instrument Serif italic = greetings/display; JetBrains Mono = selected currency/date/identifier/technical metadata.
- Warm paper light mode + warm-charcoal dark mode; terracotta brand/action accent.
- Semantic family: info blue, success green, warning amber, danger/coral.
- One strong dark operational anchor is allowed when useful; supplied Client Home HTML contributes principles, not layout.
- Client Portal phone/tablet uses app-style anatomy and bottom navigation; desktop horizontal navigation starts at `xl`.
- Non-blocking visual refinements are deferred under the owner build-direction override.

## AI + support architecture
- Àríyá is Re:Solve's own AI and exists only inside Re:Solve.
- Àríyá is not Captain and is not powered by Captain.
- Re:Solve human escalation: `Re:Solve -> Àríyá -> dedicated owner/provider Re:Solve-support Chatwoot inbox -> human agent`.
- Captain MUST be disabled on that Re:Solve human-takeover inbox.
- Separately, an individual client website/property may use its own Chatwoot inbox with Captain enabled when the provider owns that property's support responsibility.
- Do not cross these domains.
- Full authority: `10-build/lovable-launch/AI-SUPPORT-ARCHITECTURE.md`.

## Auth expansion plan
- No public registration.
- Future first-account path: staff/admin creates account -> invite -> onboarding -> set password -> optional passkey -> optional TOTP -> optional Google/GitHub linking -> finish -> authorized destination.
- Google/GitHub must not create public accounts.
- ALTCHA planned for abuse-prone operations.
- WhatsApp auth remains a later preflight; Baileys is connector/messaging infrastructure, not canonical auth root.
- Full authority: `10-build/lovable-launch/AUTH-EXPANSION.md`.

## Checklist.design QA rule
- Use relevant Checklist Design checklists for states, focus, responsiveness, dark mode, search, loading/error feedback, copy, forms, support, payments and auth/recovery.
- Do not copy Checklist Design visuals.
- Product Bible + Re:Solve Core/visual dialect remain authoritative.

## CLIENT-PWA-VIS-001 closure review
**FUNCTIONALLY ACCEPTED / VISUAL POLISH DEFERRED**
Latest verified app head: `73c303bcdc71a9a9a3fca907641770e51178bdb4`.
Compared with prior reviewed head `843cec5cdfbc2499cc970d54fd23131c5fc4ebe7`, only these source files changed:
- `src/components/shell/shared/MovableAriyaLauncher.tsx`
- `src/components/shell/portal/PortalBottomNav.tsx`
- `src/components/shell/portal/PortalShell.tsx`
- `src/components/shell/portal/PortalTopBar.tsx`
- `src/components/shell/portal/PortalNavigation.tsx`
- `src/components/shell/portal/portal-nav.ts`
- `src/routes/_portal.index.tsx`

Verified implementation facts:
- Àríyá button mounts invisibly while unresolved, allowing `buttonRef` measurement without a visible top-left jump.
- latest/final position is carried through `positionRef` and persisted from that ref.
- Portal launcher reserves 64px bottom-nav clearance below 1280px in addition to safe-area-bottom.
- phone/tablet bottom navigation is `xl:hidden`; desktop navigation is `hidden xl:flex`; Portal shell bottom padding follows the same breakpoint.
- `PORTAL_NAV_ITEMS` is the single navigation metadata source and includes Lucide icons.
- PortalTopBar dead drawer imports/state were removed.
- Home tablet/desktop composition now defers broad desktop columns to `xl`.
- Attention/Home statuses gained surfaced StatusBadge treatment and stronger semantic markers.
- Auth/identity/server/Supabase/database/authorization/DEV-preview files were not changed.

Deferred QA/polish items:
- Bottom-tab focus treatment should be rechecked during FOUND-001G accessibility QA against the full frozen ring + ring-offset contract.
- Remaining subjective client visual flaws are tracked but do not block engineering progression under the owner direction above.

## FOUND-001G1A — PWA installability baseline
**ACCEPTED / CANONICAL / FROZEN**
Latest verified app head: `ec8df572306396215debf5f7cc022618358435de`.
Compared with prior verified app head `73c303bcdc71a9a9a3fca907641770e51178bdb4`, final net changes are only:
- `public/manifest.webmanifest`
- `public/icons/resolve-180.png`
- `public/icons/resolve-192.png`
- `public/icons/resolve-512.png`
- `src/routes/__root.tsx`

Verified implementation facts:
- manifest declares `id`, `name`, `short_name`, description, `/` start URL, `/` scope, `display: standalone`, background/theme colors and `prefer_related_applications: false`.
- root head links the manifest and Apple touch icon and adds light/dark `theme-color` plus mobile/Apple standalone metadata.
- PNG headers verify actual icon dimensions: 180x180, 192x192 and 512x512.
- current centered Re:Solve mark has substantial safe space and is acceptable as a temporary replaceable app icon; manifest exposes normal and maskable entries.
- no dependency/package change was introduced.
- canonical code search found no service-worker, Workbox, Cache API or PWA-plugin implementation.
- Auth, identity, authorization, Supabase, RLS, database, Admin shell, Portal shell/Home and Àríyá behavior were not modified by the final net G1A change set.
- Lovable reported frozen install/build/lint/typecheck verification success.

G1A does **not** authorize offline caching of authenticated application content. Installability and cache policy remain separate security concerns.

## PWA implementation boundary
- One Re:Solve application origin/manifest for now; do not invent separate Admin/Portal manifests unless a later product decision requires it.
- No custom install banner is required at foundation stage.
- **G1B must remain conservative:** authenticated navigation/document responses, server-function/RPC responses, Supabase/API responses, auth callbacks, login/recovery flows, organisation-private data, Vault/secrets, notifications and other identity-dependent payloads are network-only and must not enter Cache Storage.
- If a service worker is introduced, its first foundation role is bounded lifecycle/update control and caching only immutable/public static assets whose safety is explicit.
- Offline business-data access is not a FOUND-001 requirement and must not be invented in G1B.

## FOUND-001 remaining closure
Completed/frozen: A stack/repo, B tokens/UI stack, C Core C1-C5E, D/E functional shell architecture, F auth/identity/RLS/authorization/organisation context, DEV preview, shell functional closure, G1A PWA installability.

Still required:
1. **FOUND-001G1B** — conservative service-worker/offline/update/cache boundary.
2. FOUND-001G accessibility/device/Checklist QA.
3. FOUND-001G automated tests + CI + engineering hardening.
4. **FOUND-001R** — integrated review, self-host check, reconcile original demo-user criterion, final PASS/CONDITIONAL/FAIL record.

Rich Admin Home and real Client Properties/Projects/Support/Billing domain implementations remain post-FOUND-001 work.

## Sequencing
1. **FOUND-001G1B — Offline + Cache + Update Boundary**.
2. inspect/freeze G1B.
3. accessibility/device/Checklist QA.
4. automated tests/CI/engineering hardening.
5. FOUND-001R integrated closure.
6. after FOUND-001: continue real operational/domain logic; return to deferred visual polish when appropriate.

## Next action
Run **FOUND-001G1B — Offline + Cache + Update Boundary** only. Do not add offline business-data storage or cache authenticated/private application responses.