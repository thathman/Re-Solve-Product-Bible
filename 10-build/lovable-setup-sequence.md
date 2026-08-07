# Re:Solve Lovable Setup Sequence

## Purpose
Prepare Lovable to build Re:Solve gradually without asking it to generate the entire OS at once.

## Step 1 — Connect source control
Connect Lovable to `thathman/Re-Solve`.

Rules:
- GitHub is the source-controlled application record;
- inspect legacy Re-Solve only as behavior/reference;
- prefer Lovable's strongest current compatible architecture;
- do not rewrite/build every future feature during setup.

## Step 2 — Add persistent Knowledge
Load/refine `10-build/lovable-knowledge.md` as durable Project/Workspace Knowledge.

It should include canonical product boundaries, Core UI/navigation requirements, portability, Principal/permissions, exclusions, provider boundaries and build-slice discipline—not every page specification.

## Step 3 — Prepare mandatory Core UI direction
Before business modules, Lovable must know:
- Re:Solve Core UI Component Framework is non-negotiable;
- shadcn/ui, Untitled UI React and Tremor are primary mandatory sources/influences;
- React Aria/Base UI/Radix provide strongest accessible primitive behavior where appropriate;
- TanStack Table/Query are preferred headless operational foundations where appropriate;
- final components are Re:Solve-owned/normalized rather than library soup;
- navigation is simple/shallow and must avoid Odoo/Twenty-style app/module navigation;
- Sidebar, TopBar, avatar/account, Notifications, Search/Command, Quick Create, Àríyá and mobile nav are first-class product work.

Do not install every possible specialist dependency preemptively. Add libraries when FOUND-001/current slice actually uses them.

## Step 4 — Create initial custom skills
Canonical initial skills:
1. `resolve-feature`
2. `resolve-ui`
3. `resolve-shell`
4. `resolve-form`
5. `resolve-data-table`
6. `resolve-security-review`
7. `resolve-pwa`
8. `resolve-release`
9. `self-host-check`

Source templates live under `10-build/lovable-skills/`.

Do not create/use deprecated `airix-*` names. Re:Solve is the product; Airix Media is the first Operating Entity/deployment.

Domain-specific skills such as `resolve-monitoring`, `resolve-document`, `resolve-ai`, `resolve-connector`, `resolve-plugin`, `resolve-api` and `resolve-mcp` are added when their first relevant slice approaches.

## Step 5 — Connect development Supabase
Use Supabase where useful for development auth/data/storage.

Initial expectations:
- one Workspace;
- Airix Media Operating Entity;
- Human User/Profile/Membership foundation;
- canonical permission/scope pattern;
- clean migration history;
- fictional demo data;
- safe storage policies;
- data/provider access centralized behind services/repositories where feasible.

Do not create the full future Re:Solve schema.

Do not introduce HR, Timesheets/Time Tracking or Client Service Consumption tables.

## Step 6 — Execute `FOUND-001` only
`10-build/prompts/FOUND-001-foundation.md` is the first application build instruction.

FOUND-001 itself establishes:
- architecture boundaries;
- Core UI Framework/tokens/primitives;
- Component Gallery;
- production-quality Admin shell;
- production-quality Portal shell;
- strong Sidebar/TopBar/avatar/Notifications/Search/Quick Create/Àríyá foundation;
- minimal identity/Membership/permission gates;
- PWA base;
- shared states;
- accessibility and quality baseline.

Do not split these foundational shell components into low-quality temporary slices merely to move faster.

## Step 7 — PWA from foundation
FOUND-001 includes manifest/installability/service-worker/offline-shell/update foundation and cache safety.

Full push/Notification delivery comes later, but shell/mobile/PWA composition starts immediately.

## Step 8 — Quality baseline
Use stack-appropriate:
- strict TypeScript;
- lint/format checks;
- unit/component tests;
- browser/flow tests such as Playwright where compatible;
- accessibility checks;
- development Component Gallery/visual review.

Functional tests are not the only release gate; use `09-design/performance-device-and-design-qa.md`.

## Step 9 — First fictional demo universe
FOUND-001 seeds only what it needs:
- `Re:Solve Demo Workspace`;
- Operating Entity `Airix Media`;
- fictional staff `Amina Bello` and `Chidi Okafor`;
- fictional client Organisation `Westbridge University`;
- fictional client Users/Memberships.

Later slices add canonical demo Properties/Projects/Requests/Billing/etc. from `demo-data-blueprint.md`.

Never seed real credentials, clients or staff identities.

## Step 10 — Foundation review gate
Before authoring the next build slice, inspect:
- architecture/service/data boundaries;
- routing/auth/permission denial;
- Core UI quality;
- simple navigation comprehension;
- Sidebar/TopBar/avatar/Notification/Àríyá polish;
- Component Gallery coverage;
- phone/tablet/laptop/desktop;
- PWA/offline/update state;
- accessibility;
- dependency choices;
- test/quality output;
- `self-host-check`;
- whether any future module was prematurely scaffolded;
- whether any Product Bible contradiction surfaced.

If the foundation is visually weak, fix the foundation before adding business modules.

## Step 11 — Author the next slice from actual FOUND-001 output
Do **not** pre-commit Lovable to a long sequence before seeing the generated foundation.

Likely early business progression may include:
- Dashboard deterministic Attention shell/prototype;
- Organisations/Clients;
- Contacts/Memberships;
- Properties hierarchy/Posture foundation;

But the exact `FOUND-002`/next slice must be written only after reviewing FOUND-001's real code and UX.

## Rule for every Lovable build conversation
Provide:
- exact slice id/objective;
- exact Product Bible references;
- actors/permissions;
- in scope;
- explicitly out of scope;
- required Core UI components/patterns to reuse;
- data/provenance/Attention/Notification/PWA implications;
- acceptance criteria;
- stop condition/completion report.

Never dump the entire Product Bible into one prompt and never tell Lovable `build the CRM` or `build the OS`.
