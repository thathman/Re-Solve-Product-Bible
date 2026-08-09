# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN + CLIENT SHELL FUNCTIONAL CLOSURE ACCEPTED — NON-BLOCKING VISUAL POLISH DEFERRED — FOUND-001G1A + G1B + G2 ACCEPTED/FROZEN — FOUND-001G3A TEST BASELINE IMPLEMENTED/ACCEPTED WITH CLEANUP ROLLED INTO NEXT BUNDLED ENGINEERING CLOSURE — NEXT: FOUND-001G3 ENGINEERING CLOSURE (TEST CLEANUP + CI + ENGINEERING/PORTABILITY)**

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
- Lovable credits should be conserved: prefer medium/bundled supervised slices that combine closely related work and share the same architecture/review boundary.
- Do not spend a separate Lovable run on tiny non-critical cleanup; roll it into the next related slice.
- Keep database migrations, auth/security model changes, privilege boundaries and destructive operations isolated when bundling would make them unsafe to review.

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
- subjective design polish remains deferred by owner direction.

## FOUND-001G1A — PWA installability
**ACCEPTED / CANONICAL / FROZEN**
Verified app head: `ec8df572306396215debf5f7cc022618358435de`.
- `public/manifest.webmanifest` plus 180/192/512 local icons exist.
- root head links manifest, Apple touch icon and light/dark theme-color metadata.
- `display: standalone`, same-origin `/` start URL/scope.
- no new dependency and no security/domain behavior changes.

## FOUND-001G1B — Offline / cache / update boundary
**ACCEPTED / CANONICAL / FROZEN**
Verified app head: `0db19adc419d1b18cf1f29b3efedf387321b9990`.
- cache name `resolve-public-v1`.
- exact cache allowlist only: `/offline.html`, `/manifest.webmanifest`, `/favicon.ico`, `/icons/resolve-180.png`, `/icons/resolve-192.png`, `/icons/resolve-512.png`.
- install precaches only explicit public assets; no dynamic cache-default path.
- activate removes only prior `resolve-public-*` versions and claims clients.
- `SKIP_WAITING` is explicit/message-driven.
- navigation/HTML is network-first with `/offline.html` fallback only; successful navigation is never cached.
- all other unknown/private requests are network-only.
- controller reload is gated by explicit user Refresh through `refreshRequestedRef`.
- no authenticated/private HTML, server-function/RPC, Supabase/API, auth/recovery, organisation/profile/project/property/billing/support, notification, Àríyá/Chatwoot, Vault, token or session material is authorized in Cache Storage.
- no Workbox/plugin/background sync/offline mutation/business-data IndexedDB.

## FOUND-001G2 — Accessibility / Device / Checklist QA
**ACCEPTED / CANONICAL / FROZEN**
Latest verified app head: `03f8f10a4b4ef762aa0ebadc32293bbe4e1643d2`.
- Admin and Portal expose visible-on-focus skip links to the existing single main landmark.
- both `#rs-main-content` targets have `tabIndex={-1}`.
- Portal bottom nav has `aria-label="Primary"`, `aria-current="page"`, complete frozen focus ring + ring-offset contract, and decorative active marker hidden from the accessibility tree.
- root Not Found/Error controls use the frozen Re:Solve variable-based focus contract.
- Core Alert relies on its `role="alert"` / `role="status"` semantics without redundant explicit `aria-live`.
- PWA offline/update notices constrain phone width, account for bottom safe area and gate entrance animation behind `motion-safe`.
- offline fallback Try again has visible keyboard focus.
- organisation-selection label/focus association improved.
- Core FormField/Input provide label/control, required/invalid/error-description wiring; Login has email/current-password autocomplete and accessible password reveal.
- final offline notice uses the canonical soft danger surface with readable `text-rs-status-danger-foreground` and a restrained matching border in both themes.
- Lovable reports plain lint/build/typecheck exit 0.
- no auth/authorization/RLS/Supabase/DB/PWA-cache/route/DEV-preview behavior changed.

## FOUND-001G3A — Test harness + security/foundation regression baseline
**IMPLEMENTED / BASELINE ACCEPTED — SMALL CLEANUP DEFERRED INTO BUNDLED G3 ENGINEERING CLOSURE**
Latest reviewed app head: `c19fc227e1b19254c35020e36b38bd6fa9c95302`.
Compared with G2 head `03f8f10a4b4ef762aa0ebadc32293bbe4e1643d2`, net changes are limited to package/lockfile, Vitest config, one narrowly hardened redirect helper and four test suites.

Accepted facts:
- canonical test runner is Vitest with Node environment.
- scripts exist: `bun run test` -> `vitest run`; `test:watch` -> `vitest`.
- four suites / 26 tests cover redirect safety, staff/Portal/exact-org access primitives, PWA manifest/service-worker source contracts, CSRF presence and service-role source leakage.
- tests use mocks/fictional identifiers; no real Supabase/network/secrets/test users.
- `getSafeRedirect()` was minimally hardened to reject protocol-relative, external and backslash-normalized redirect forms while preserving ordinary internal absolute paths.
- authorization functions themselves are tested while only `readCurrentIdentity()` is mocked.
- production auth/identity/RLS/service-worker logic was otherwise unchanged.

Cleanup/hardening to roll into the NEXT bundled G3 run, not a separate Lovable credit:
1. Remove unnecessary direct `glob` and `@types/glob` dev dependencies. `source-contracts.test.ts` only needs filesystem recursion; use Node built-ins (`fs`/`path`) instead. Keep Vitest as the only new test-framework dependency.
2. Strengthen authorization negative tests to assert the thrown `statusCode` contract (`400`, `401`, `403`) in addition to stable messages. These status codes are part of the frozen server authorization boundary.
3. Tighten the service-role source scan. Do NOT grant `src/lib/supabase/server.ts` a speculative exception. The only canonical allowed source containing/defining `supabaseAdmin` is the generated/quarantined `src/integrations/supabase/client.server.ts` unless a separately supervised privileged boundary is explicitly approved later.
4. Lovable reported Fast Refresh lint warnings while saying errors were resolved. Bundled G3 closure must run plain `bun run lint`, record its actual exit status/warning count, and fix only meaningful foundation warnings without redesigning components.

## FOUND-001G3 — Bundled engineering closure
**NEXT — ONE MEDIUM/LARGE LOVABLE RUN TO CONSERVE CREDITS**
Bundle the closely related remaining engineering work:
- G3A cleanup items above.
- GitHub Actions CI for Bun frozen install, tests, lint, typecheck and production build.
- CI must not require production secrets or a live Supabase project for these foundation checks.
- dependency/provenance review; preserve the TanStack/js-yaml security versions/override and flag rather than casually upgrade unrelated packages.
- environment/secrets audit: `.env*` gitignore boundary, `.env.example`, no committed secrets, private env server-only.
- production-build portability review: no Lovable runtime dependency required by Re:Solve product code; document any build-tool dependency that still needs replacement before fully independent self-host production.
- service-worker/public assets available in production output.
- self-host readiness checks that can be automated safely now.
- concise engineering closure record in repository docs if useful; no visual/product redesign.

## FOUND-001 remaining closure
Completed/frozen: A stack/repo, B UI stack/tokens, C Core C1-C5E, D/E shell architecture, F auth/identity/RLS/authorization/org context, DEV preview, shell functional closure, G1A installability, G1B offline/cache/update boundary, G2 accessibility/device/Checklist QA.

Implemented baseline: G3A tests.

Still required:
1. **FOUND-001G3 ENGINEERING CLOSURE** — test cleanup + CI + engineering/portability hardening in one bundled run.
2. **FOUND-001R** — integrated review + self-host check + reconcile original demo-user criterion + final PASS/CONDITIONAL/FAIL record.

Rich Admin Home and real Client Properties/Projects/Support/Billing remain post-FOUND-001 work.

## Sequencing
1. **FOUND-001G3 ENGINEERING CLOSURE** — bundled medium/large slice.
2. inspect/freeze G3.
3. **FOUND-001R** integrated closure — bundle final review/fixable non-destructive foundation closure where safe.
4. after FOUND-001: continue operational/domain logic; return to deferred visual polish when appropriate.

## Next action
Run **FOUND-001G3 ENGINEERING CLOSURE**. Do not split CI and portability into separate Lovable credits unless the implementation reveals a genuine security/architecture blocker.