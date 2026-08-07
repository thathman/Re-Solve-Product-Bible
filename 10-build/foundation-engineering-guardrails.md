# Re:Solve Foundation Engineering Guardrails

## Purpose
These are the last cross-cutting engineering rules that must be established during FOUND-001 so later product slices do not inherit avoidable UI, dependency, environment, localization, or quality debt.

They do **not** expand FOUND-001 into business functionality.

## 1. UI source licensing and provenance
Re:Solve may heavily use source-owned/copy-paste UI components, but every imported source must have a known license and provenance.

### Default policy
- Prefer open-source/free components that are clearly permitted for commercial use.
- shadcn/ui/open-code components are approved sources.
- Untitled UI **FREE/open-source** React components are approved by default.
- Untitled UI PRO components/assets may be used only when the project owner has an appropriate license and that use is recorded. Do not place licensed PRO source/assets into the public Product Bible or any public repository.
- Tremor Raw/open-source components are approved subject to their applicable source license and notice requirements.
- Third-party registries/blocks must be reviewed before installation; public availability is not proof of acceptable license/security.

### UI provenance ledger
FOUND-001 should create a source-controlled `docs/ui-sources.md` (or equivalent) in the application repository recording, for every materially copied/imported UI source:
- component/pattern name;
- upstream library/source;
- source URL or registry identifier;
- upstream version/date when known;
- license classification;
- whether it is FREE/open-source or separately licensed;
- meaningful Re:Solve modifications;
- canonical Re:Solve component that now owns the pattern.

The ledger is maintenance evidence, not a requirement to annotate every trivial line of code.

## 2. Runtime/package-manager baseline
FOUND-001 must record and preserve:
- package manager and one lockfile only;
- supported Node/runtime version using a standard source-controlled mechanism (`packageManager`, `.nvmrc`, `.node-version`, or equivalent chosen by the generated stack);
- React version;
- TypeScript version;
- Tailwind version;
- build tool/framework version.

Do not silently switch package managers or create multiple lockfiles.

## 3. Dependency governance
Every dependency added in FOUND-001 needs a current-slice reason.

Before accepting the foundation verify:
- compatible React/Tailwind/runtime requirements;
- no unnecessary duplicate library for an existing primitive;
- acceptable maintenance/security posture;
- acceptable license for intended commercial/private deployment;
- portability outside Lovable;
- no package installed solely for future scope.

A later automated dependency-update/security service may be added, but FOUND-001 should at minimum leave a clean deterministic lockfile and auditable dependency list.

## 4. Environment and secret boundary
FOUND-001 must establish a predictable environment configuration pattern.

Require:
- committed `.env.example` or equivalent containing names/descriptions only, never secrets;
- explicit distinction between browser-safe/public variables and server-only secrets;
- typed/schema validation for required environment values where compatible with the generated stack;
- clear failure behavior for missing required configuration;
- no production keys in Lovable prompts, demo seed data, committed files, screenshots, logs, or browser bundles;
- connector/provider environment variables grouped consistently when those providers are later introduced.

The application must not depend on undocumented magic environment variables.

## 5. Error boundaries and observability foundation
FOUND-001 should establish ordinary application error handling without prematurely choosing a production monitoring vendor.

Require:
- root/application error boundary;
- route/surface error handling where the framework supports it;
- canonical user-facing `ErrorState` with retry/recovery guidance;
- structured development logging rather than arbitrary repeated `console.log` usage;
- no secrets/Vault values/credentials in logs;
- a small provider-neutral error-reporting/telemetry boundary or documented integration point so Sentry/another provider can be introduced later without rewriting UI code.

Do not install a production observability SaaS merely to satisfy FOUND-001 unless there is a concrete reason.

## 6. Minimal CI gate
Because GitHub is the portability/source boundary, FOUND-001 should create a minimal repository CI workflow compatible with the generated stack.

On pull request and/or protected branch changes, CI should run the available equivalents of:
- dependency install from lockfile;
- typecheck;
- lint;
- unit/component tests;
- production build.

A lightweight browser/access smoke test may be included when reliable in the chosen stack. Full expensive E2E suites do not need to block every FOUND-001 commit.

CI must not require production secrets.

The foundation is not accepted if it only works inside Lovable preview but fails an ordinary source build in CI.

## 7. Locale, timezone, currency and number formatting
Re:Solve is not allowed to hard-code one country's formatting into reusable UI.

FOUND-001 should establish lightweight formatting utilities/providers based on standard locale-aware APIs (for example `Intl`) for:
- dates;
- date/time;
- relative time where useful;
- numbers;
- currency;
- percentages.

Architecture rules:
- persisted timestamps should use an unambiguous canonical representation, normally UTC;
- display uses the relevant Workspace/User/Operating Entity timezone/locale once those settings exist;
- demo defaults may be chosen, but components must not hard-code `₦`, `$`, `DD/MM/YYYY`, `MM/DD/YYYY`, or a fixed timezone as universal truth;
- financial values are stored as numbers/minor-unit-safe domain values, not formatted strings;
- formatting remains separate from calculation/business truth.

Full localization/translation is later scope; **localization readiness is foundation scope**.

## 8. Theme and appearance baseline
Light/dark/system appearance must be treated as Core UI capability, even if only light mode receives the deepest initial visual polish.

FOUND-001 should establish:
- semantic theme tokens rather than raw page-specific colors;
- light theme;
- dark theme with accessible contrast;
- system preference option;
- safe theme persistence;
- PWA/browser theme-color handling where appropriate;
- Component Gallery coverage of both themes for foundational chrome/components.

Operating Entity branding may later adjust approved accents/logo surfaces, but cannot override semantic accessibility tokens.

## 9. Typography and font licensing
The exact Re:Solve typeface is a visual design decision, not something Lovable may choose accidentally and bury in implementation.

During FOUND-001:
- select an initial typography system deliberately;
- prefer high-quality open-source/system fonts unless a paid font license is explicitly approved;
- record family, fallback stack, weights actually used, loading strategy and license/source;
- avoid downloading or embedding unknown font files;
- test long labels, numbers, tables and Portal reading;
- support tabular numerals for finance/metrics where available.

The typography choice remains reviewable at the FOUND-001 design gate, but it must be coherent and documented before business modules multiply it.

## 10. Iconography
Use one canonical primary icon family for normal application chrome.

Rules:
- do not visibly mix Lucide, Untitled UI Icons, Remix and other icon vocabularies without purpose;
- normalize size/stroke/optical alignment through Core UI wrappers/tokens;
- unfamiliar icons retain text labels/tooltips as appropriate;
- Àríyá receives a distinct Re:Solve-native treatment rather than a generic sparkle icon;
- any paid/licensed icon asset follows the same provenance rule as UI components.

## 11. Brand assets at foundation
FOUND-001 must not invent a complex permanent logo just to fill space.

Until a dedicated Re:Solve brand mark is approved:
- use a high-quality typographic Re:Solve wordmark treatment and clearly identified provisional app/PWA icon if necessary;
- keep logo/favicon/PWA assets replaceable through the Brand/Core UI token system;
- do not embed Airix Media branding as the product's permanent Re:Solve brand;
- Àríyá's visual mark may be provisional but must be intentionally differentiated from generic AI sparkle branding.

A later brand-design decision can replace provisional assets without changing application architecture.

## 12. FOUND-001 review evidence
The completion report/review should explicitly record:
- package manager/runtime versions;
- Tailwind/shadcn base and UI-source choices;
- `docs/ui-sources.md` or equivalent;
- licenses/provenance of materially copied UI code;
- typography/icon choices;
- theme behavior;
- `.env.example` and environment validation approach;
- error-boundary/observability integration point;
- CI workflow and result;
- locale/timezone/currency formatting approach;
- any intentional deviation from these guardrails.

## Stop rule
If a generated dependency or UI source requires a license/version migration that conflicts with the foundation rules, stop and report the choice. Do not silently downgrade the stack, copy restricted assets, or create a parallel UI system.
