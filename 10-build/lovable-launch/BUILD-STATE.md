# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so future Lovable prompts are based on actual application state.

## Current stage
**FOUNDATION / CORE / SECURITY / IDENTITY / AUTHORIZATION FROZEN — DEV-PREVIEW-001 FROZEN — ADMIN + CLIENT SHELL FUNCTIONAL CLOSURE ACCEPTED — NON-BLOCKING VISUAL POLISH DEFERRED — FOUND-001G1A + G1B + G2 ACCEPTED/FROZEN — FOUND-001G3 ENGINEERING/PORTABILITY IMPLEMENTED AND CONDITIONALLY ACCEPTED — NEXT: FOUND-001R FINAL INTEGRATED REVIEW + SAFE CLOSURE**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible`
- Current app: `thathman/re-solve-c560d62c` on `main`
- Latest reviewed app head for G3: `a84f84f62d238c65bcfdf2d136a2669c8cb1e9f8`
- Client visual authority: `Airix360/AM-Client-Docs` Design System + `Airix360/airixmedia-web`.
- `checklist.design` is UX completeness / pre-freeze QA reference only, never visual authority.
- Legacy/reference app `thathman/Re-Solve` remains untouched absent explicit owner approval.

## Owner build-direction override
**CANONICAL — 2026-08-09**
- Continue building product/foundation logic now.
- Do not spend supervised Lovable runs on subjective cosmetic flaws until logic is substantially set.
- Track visual polish for later.
- Visual issues may still block when they affect accessibility, responsive usability, security, legibility, or core interaction correctness.
- Conserve Lovable credits: prefer medium/bundled supervised slices sharing the same architecture/review boundary.
- Roll tiny non-critical cleanup into the next related slice.
- Keep database migrations, auth/security model changes, privilege boundaries and destructive operations isolated when bundling would make review unsafe.

## Frozen security / architecture
- Authentication, staff access, organisation access, roles/permissions and capabilities are server-controlled; browser metadata is never authoritative.
- Route `beforeLoad` checks are UX gates only; private server functions/routes independently authorize.
- Normal user reads use caller-scoped Supabase + RLS; generated `supabaseAdmin` remains quarantined/unused by ordinary application authorization.
- Preserve explicit `createCsrfMiddleware` in `src/start.ts`.
- Runtime validation is required at consequential boundaries.
- Never surface/log raw auth/database/provider/Zod/access errors, tokens, sessions, secrets or privileged values.
- `requireActiveStaff()` / Admin server access remain frozen.
- `requirePortalAccess()` / Portal server access remain frozen.
- `requireActiveOrganisation(organisationId)` freshly revalidates exact active organisation access.
- `rs_portal_org` is an untrusted UUID-only context pointer, never authorization evidence.
- No broad RBAC, domain persistence, seed/test identities or public registration yet.
- Service role/private credentials are server-only.
- PWA/offline Cache Storage is positive-allowlist-only for public static assets; authenticated/private HTML/data, Supabase/API/RPC/server-function responses, identity/org/project/property/billing/support/notification/Àríyá/Chatwoot/Vault/token/session material are not authorized for offline caching.
- Canonical concise security memory: `10-build/lovable-launch/SECURITY-MEMORY.md`; Lovable `@security-memory` mirrors it.

## Frozen foundation / functional surfaces
- FOUND-001A repository/stack accepted.
- FOUND-001B token/UI stack accepted.
- Core UI C1-C5E accepted/frozen.
- `/ui` remains dev-only.
- Admin shell/routes accepted: Home, Clients, CRM, Properties, Projects, Sales, Billing, Support, Platform.
- Portal shell accepted: `/`, `/properties`, `/projects`, `/support`, `/billing` under `_portal`.
- Auth routes accepted: `/login`, `/forgot-password`, `/reset-password`, `/auth/callback`.
- `/select-organisation` uses canonical safe redirect and server-revalidated active-org context.
- F0-F3C auth/identity/RLS/Admin access/Portal access/active-org context accepted/frozen.
- DEV-PREVIEW-001 accepted until intentional demo identities are introduced.

## Visual dialects
### Admin
- Lucid-style Re:Solve operational dialect remains canonical.
- Inter, neutral/graphite structure, restrained Lucide, subtle borders, low shadow, denser operational composition.
- Admin search belongs in expanded Sidebar; collapsed Sidebar uses Search IconButton.
- Admin TopBar has no search and no Àríyá trigger.
- Shared Light/Dark/System control and movable floating Àríyá launcher remain.

### Client-facing
- Auth + Client Portal use Airix/Re:Solve client dialect.
- Space Grotesk = UI/body; Instrument Serif italic = greetings/display; JetBrains Mono = selected financial/date/identifier/technical metadata.
- Warm-paper light + warm-charcoal dark; terracotta brand/action; info blue, success green, warning amber, danger/coral semantics.
- Client phone/tablet uses app-style anatomy + bottom navigation below `xl`; desktop horizontal navigation begins `xl+`.
- Subjective visual polish remains deferred.

## AI + support architecture
- Àríyá is Re:Solve's own AI and exists only inside Re:Solve.
- Àríyá is not Captain and is not powered by Captain.
- Re:Solve human escalation: `Re:Solve -> Àríyá -> dedicated owner/provider Re:Solve-support Chatwoot inbox -> human agent`.
- Captain MUST be disabled on that Re:Solve human-takeover inbox.
- A separate client website/property Chatwoot inbox may use Captain when the provider owns that property's support responsibility.
- Full authority: `10-build/lovable-launch/AI-SUPPORT-ARCHITECTURE.md`.

## Auth expansion plan
- No public registration.
- Future path: staff/admin creates account -> invite -> onboarding -> set password -> optional passkey -> optional TOTP -> optional Google/GitHub linking -> finish -> authorized destination.
- Google/GitHub must not create public accounts.
- ALTCHA planned for abuse-prone operations.
- WhatsApp auth remains later preflight; Baileys is messaging/connector infrastructure, not canonical auth root.
- Full authority: `10-build/lovable-launch/AUTH-EXPANSION.md`.

## FOUND-001G1A — PWA installability
**ACCEPTED / CANONICAL / FROZEN**
- manifest + local 180/192/512 icons exist.
- root head links manifest, Apple icon and adaptive theme colors.
- `display: standalone`, same-origin `/` start URL/scope.
- no service worker/cache policy was introduced in G1A.

## FOUND-001G1B — Offline/cache/update boundary
**ACCEPTED / CANONICAL / FROZEN**
- cache `resolve-public-v1`.
- exact allowlist: `/offline.html`, `/manifest.webmanifest`, `/favicon.ico`, `/icons/resolve-180.png`, `/icons/resolve-192.png`, `/icons/resolve-512.png`.
- navigation is network-first with cached generic offline fallback only; successful HTML is never cached.
- unknown/private requests are network-only.
- update activation/reload is explicit user action via `SKIP_WAITING` + gated `controllerchange`.

## FOUND-001G2 — Accessibility/device/Checklist QA
**ACCEPTED / CANONICAL / FROZEN**
- Admin/Portal skip links target the single `#rs-main-content` landmarks with `tabIndex={-1}`.
- Portal bottom nav has `aria-label="Primary"`, `aria-current`, full frozen focus contract and non-color-only active state.
- root error/404 controls use frozen focus variables.
- Core Alert relies on `role="alert"` / `role="status"` without redundant explicit live-region attributes.
- offline/update notices are safe-area-aware and reduced-motion-aware.
- offline notice uses soft danger surface + readable danger foreground.
- auth/Core form semantics are adequate for current scope.

## FOUND-001G3A — Test baseline
**IMPLEMENTED / ACCEPTED AS FOUNDATION BASELINE**
- Vitest Node environment.
- scripts: `bun run test` and `bun run test:watch`.
- four suites / 26 tests cover redirect safety, Admin/Portal/exact-org access primitives, PWA manifest/service-worker contracts, CSRF presence and service-role source leakage.
- `getSafeRedirect()` hardened against protocol-relative, external and backslash-normalized redirect forms.
- tests use fictional identifiers/mocks only; no real network/Supabase/secrets/test users.

## FOUND-001G3 — Engineering / portability closure
**IMPLEMENTED / CONDITIONALLY ACCEPTED — FINAL NON-DESTRUCTIVE CLEANUP ROLLED INTO FOUND-001R**
Latest reviewed app head: `a84f84f62d238c65bcfdf2d136a2669c8cb1e9f8`.
Compared with prior G3A head, the implementation adds/changes only engineering/portability/test/env/docs files plus tiny Supabase env-reference edits; no domain UI or authorization model changes.

Verified implemented facts:
- `@lovable.dev/vite-tanstack-config` is removed from current `vite.config.ts`; app uses official/standard Vite + TanStack Start plugin + React + Tailwind + Nitro Bun preset.
- `package.json` has production `start: bun .output/server/index.mjs`.
- multi-stage Bun `Dockerfile` and `.dockerignore` exist.
- `.github/workflows/ci.yml` runs install, tests, lint, typecheck, production build and verifies PWA output files.
- `.env.example` distinguishes client VITE Supabase values from server Supabase values and contains placeholders only.
- `.gitignore` / `.dockerignore` exclude `.env*` while allowing `.env.example`.
- `docs/SELF-HOSTING.md` and README document Bun + Supabase-compatible self-host direction.
- source security test now uses Node filesystem recursion and allows `supabaseAdmin` only in `src/integrations/supabase/client.server.ts`.
- authorization tests now assert stable message + actual `400/401/403` statusCode contracts.
- service worker/public PWA files remain part of production-output verification.
- `js-yaml` override remains `4.3.1`; frozen TanStack versions remain unchanged.

Final-review cleanup / verification items — DO NOT spend a separate Lovable credit:
1. Lovable reported `glob` and `@types/glob` removed, but canonical `package.json` at the reviewed head still contains both even though no test uses them. Remove both in FOUND-001R and refresh `bun.lock`.
2. `vitest.config.ts` no longer carries the previously requested `clearMocks: true` and `restoreMocks: true`; decide in FOUND-001R whether to restore those deterministic defaults or explicitly document why unnecessary.
3. CI workflow is committed, but supervisor connector has not independently observed an Actions run/check for the reviewed head. FOUND-001R must distinguish “workflow source verified” from “remote CI execution verified”.
4. Plain lint reportedly exits 0 with 15 Fast Refresh warnings. FOUND-001R should record warning count and only fix meaningful foundation warnings; warnings alone need not block if framework-standard/non-actionable.
5. Self-host docs call the PWA fallback a “public shell”; actual policy is a generic offline fallback for failed navigation with no private cached HTML. Correct wording if still inaccurate.
6. Run/check final portability contract: no product-critical Lovable runtime/build dependency in current source/package/lock/config, while Lovable remains an optional development environment.
7. **Production runtime environment blocker:** current Dockerfile sets `NODE_ENV=production` only in the build stage, while `.env.example` defaults to `NODE_ENV=development` and self-host docs tell operators to pass that file into `docker run`. `writePortalContextCookie()` sets `secure` from `process.env.NODE_ENV === "production"`, so a production container accidentally running with `NODE_ENV=development` could lose the production `Secure` cookie flag. FOUND-001R must set `NODE_ENV=production` explicitly in the release image/runtime guidance and ensure example self-host instructions cannot override it back to development.

## Original demo-user criterion
The original FOUND-001 review requested fictional staff/client demo accounts. This was intentionally superseded by:
- real auth/identity/RLS/authorization architecture; plus
- DEV-PREVIEW-001 for visual inspection.
No canonical demo credentials/test users exist yet by owner decision. FOUND-001R must record this as an explicit acceptance-criterion amendment, not as an accidental omission.

## FOUND-001 remaining closure
Completed/frozen: A, B, C1-C5E, shell architecture D/E, F0-F3C auth/identity/RLS/authorization/org context, DEV preview, G1A installability, G1B offline/cache/update, G2 accessibility/device QA.

Implemented/conditionally accepted: G3 tests + CI + portability/self-host baseline.

Still required:
1. **FOUND-001R** — final integrated review; safe cleanup above; self-host/portability check; demo-user criterion amendment; section-by-section PASS/CONDITIONAL/FAIL record.

Rich Admin Home and real Client Properties/Projects/Support/Billing remain post-FOUND-001 work.

## Sequencing
1. Run **FOUND-001R FINAL INTEGRATED REVIEW + SAFE CLOSURE** as one bundled Lovable run.
2. Supervisor inspects canonical repo and final review record.
3. If no architectural/security blockers: mark FOUND-001 closed.
4. Continue into post-foundation operational/domain logic; deferred visual polish remains tracked for later.

## Next action
Run **FOUND-001R FINAL INTEGRATED REVIEW + SAFE CLOSURE**. Bundle safe non-destructive cleanup with the review to conserve Lovable credits; do not introduce new domain features, auth models, migrations or privilege boundaries.