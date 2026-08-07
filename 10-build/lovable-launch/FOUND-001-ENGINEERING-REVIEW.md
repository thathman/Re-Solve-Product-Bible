# FOUND-001 Engineering Review Addendum

Run this together with `FOUND-001-REVIEW.md` before accepting the foundation.

## UI stack compatibility
- [ ] actual package manager/lockfile recorded;
- [ ] runtime/Node version recorded and source-controlled;
- [ ] React/TypeScript/Tailwind versions recorded;
- [ ] shadcn was inspected before initialization/re-initialization;
- [ ] chosen shadcn primitive base is documented;
- [ ] Tailwind was not downgraded for a legacy UI package;
- [ ] Untitled UI was integrated component-by-component rather than scaffolding a second app;
- [ ] Tremor Raw/current copy-paste path is used rather than defaulting to legacy `@tremor/react`;
- [ ] no duplicate lockfiles or competing design-system token sets.

## UI licensing/provenance
- [ ] `docs/ui-sources.md` or equivalent exists;
- [ ] materially copied/imported components have source/license provenance;
- [ ] Untitled UI FREE/open-source components are distinguished from PRO/licensed assets;
- [ ] no Untitled UI PRO source/assets were copied into the public Product Bible;
- [ ] any separately licensed UI/icon/font asset has owner approval/license evidence;
- [ ] third-party registry components were reviewed rather than trusted merely because they were public.

## Environment and secrets
- [ ] `.env.example` or equivalent exists with names only/no secrets;
- [ ] browser-safe vs server-only environment values are clearly separated;
- [ ] required environment values are validated where compatible with the stack;
- [ ] app fails clearly when required configuration is missing;
- [ ] no secret is committed, seeded, logged or bundled client-side.

## CI/source build
- [ ] source-controlled CI workflow exists;
- [ ] clean lockfile install succeeds;
- [ ] typecheck succeeds;
- [ ] lint succeeds;
- [ ] meaningful unit/component tests succeed;
- [ ] production build succeeds outside Lovable preview assumptions;
- [ ] CI does not require production secrets;
- [ ] browser/access smoke test exists where reliable/practical.

## Error handling / observability boundary
- [ ] application/root error boundary exists;
- [ ] canonical ErrorState supports useful recovery/retry guidance;
- [ ] logs are structured/restrained and do not contain secrets;
- [ ] provider-neutral error-reporting/telemetry integration point is documented;
- [ ] no production observability vendor was unnecessarily coupled into foundation code.

## Locale/timezone/currency readiness
- [ ] shared locale-aware date/time formatter exists;
- [ ] shared number/currency/percentage formatter exists;
- [ ] no universal hard-coded currency symbol/date order/timezone appears in Core UI;
- [ ] persisted timestamps use unambiguous canonical representation;
- [ ] formatting is separate from calculation/domain values.

## Theme / typography / iconography
- [ ] semantic light theme exists;
- [ ] semantic dark theme exists;
- [ ] system appearance option exists;
- [ ] theme persistence works safely;
- [ ] foundational Component Gallery can be reviewed in light and dark;
- [ ] typography family/fallback/weights/source/license are documented;
- [ ] typography handles tables, long labels, metrics and Portal reading well;
- [ ] one primary icon vocabulary is visibly dominant;
- [ ] Àríyá treatment is distinct from generic sparkle AI branding;
- [ ] provisional logo/PWA assets are clearly replaceable rather than embedded architectural assumptions.

## Final gate
Any unresolved license conflict, Tailwind/runtime incompatibility, failed source build, leaked secret, duplicate design-system foundation, or hard-coded locale architecture is a **FAIL** for FOUND-001.
