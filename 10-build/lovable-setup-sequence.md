# Re:Solve Lovable Setup Sequence

## Purpose
Prepare Lovable to build Re:Solve gradually without asking it to generate the entire OS at once. This sequence reflects Lovable's current Git sync, Knowledge and Skills behavior as of 2026-08-07.

## Step 0 — Product Bible must be canonical first
Merge the Product Bible planning stack before the first real Lovable build. The Product Bible remains specification truth even though Lovable will not receive the entire private repository in every prompt.

Keep these source roles distinct:
- `Re-Solve-Product-Bible` — canonical product/specification source;
- current legacy `Re-Solve` repository — read/reference evidence only during transition;
- Lovable-created synced repository — new application source during active build;
- Lovable — build environment, not required production runtime.

## Step 1 — Create a dedicated Re:Solve Lovable workspace/project
A dedicated workspace is preferred because custom Skills are workspace-level and Re:Solve has a substantial project-specific skill set.

Create a fresh Lovable project for Re:Solve. Do **not** attempt to import the existing `thathman/Re-Solve` repository into Lovable.

Current Lovable Git sync does not support importing an existing GitHub repository. Lovable creates a new repository when GitHub is connected.

## Step 2 — Connect GitHub and let Lovable create the new synced repository
From the Re:Solve Lovable project, connect the correct GitHub account and allow Lovable to create a **new private repository** with two-way sync.

Use a temporary unambiguous repository name if Lovable lets you choose one, for example:
- `Re-Solve-Lovable`
- `Re-Solve-Next`

Do not rename, delete, transfer or overwrite the existing `thathman/Re-Solve` legacy repository during initial setup.

Lovable documentation states that renaming the **repository itself** is safe and sync follows the rename. Therefore, after FOUND-001 is accepted and only with explicit owner approval, the legacy repository can be archived/renamed and the Lovable-generated repository can take the canonical `Re-Solve` name. That transition is specified separately in `lovable-launch/GITHUB-TRANSITION.md`.

## Step 3 — Add Project Knowledge
Paste the canonical compact content from `10-build/lovable-knowledge.md` into **Project settings → Knowledge**.

Use Project Knowledge for Re:Solve-specific product truth because it is always present for this project. Keep it below Lovable's current project-knowledge character limit.

Workspace Knowledge may contain only genuinely workspace-wide engineering conventions if the workspace will later host more than Re:Solve. In a dedicated Re:Solve workspace, duplicating Product Knowledge at both levels is unnecessary; Project Knowledge is the canonical Lovable location.

Knowledge should cover durable rules only: architecture, terminology, Core UI/navigation, Principal/permissions, product exclusions, provider boundaries, PWA/accessibility, portability and slice discipline—not every future page specification.

## Step 4 — Install the complete canonical Re:Solve Skills
Follow:
- `10-build/lovable-skills/INSTALL.md`
- `10-build/lovable-skills/manifest.md`

The Product Bible repository is private. Current Lovable `Import from GitHub` accepts public GitHub repositories, so do not depend on direct private-repository import.

Preferred current options:
1. upload each canonical skill package as ZIP/`.skill`; or
2. use `Write manually` and copy the exact name, description and Markdown instructions.

Do not ask Lovable to regenerate/rewrite the skills using `Build with Lovable`.

Before FOUND-001, verify at minimum:
- resolve-feature
- resolve-ui
- resolve-shell
- resolve-navigation
- resolve-responsive
- resolve-accessibility
- resolve-design-review
- resolve-security-review
- resolve-pwa
- resolve-release
- self-host-check

Install the rest of the catalogue before broad domain work. Skills load on demand and do not need to be pasted into every build prompt.

## Step 5 — Confirm the Core UI direction before spending build credits
Project Knowledge and installed skills must already establish:
- Re:Solve Core UI Component Framework is non-negotiable;
- shadcn/ui, Untitled UI React and Tremor are mandatory major sources/influences;
- React Aria/Base UI/Radix are approved accessible primitive sources;
- TanStack Table/Query are preferred headless operational foundations where appropriate;
- final components are Re:Solve-owned/normalized rather than library soup;
- navigation is simple, shallow and service-CRM-like;
- Odoo-style app launchers/module grids and Twenty-style object/module switching are rejected;
- Sidebar, TopBar, ResolveAvatar/AccountMenu, Notifications, Search/Command, Quick Create, Àríyá and mobile navigation are first-class product work;
- Component Gallery is required before broad modules.

Do not install every specialist npm package preemptively. Add dependencies only when FOUND-001 or a later slice genuinely uses them.

## Step 6 — Connect/create the development backend only when FOUND-001 needs it
Use Lovable/Supabase for development auth/data/storage where useful.

FOUND-001 needs only the identity/access foundation required to demonstrate:
- one Workspace;
- Airix Media Operating Entity;
- Human Users;
- one fictional client Organisation;
- Membership/role/capability context;
- Admin vs Portal route access;
- permission denial.

Do not create the full future schema.
Do not create HR, payroll, recruitment, attendance, Timesheet/Time Tracking or Client Service Consumption tables.

Keep data/provider access behind reasonable service/repository boundaries rather than scattering direct provider calls throughout UI components.

## Step 7 — Execute `FOUND-001` only
Use `10-build/prompts/FOUND-001-foundation.md` as the first application build instruction.

Explicitly invoke the required foundation skills in the same message where Lovable supports slash-skill tags:
`/resolve-feature /resolve-shell /resolve-navigation /resolve-ui /resolve-responsive /resolve-pwa /resolve-accessibility /self-host-check /resolve-release`

Use `/resolve-design-review` after the visual implementation pass before accepting the slice.

FOUND-001 establishes:
- application boundaries;
- root repository instruction file (`AGENTS.md`) derived from the provided canonical launch template;
- Core UI Framework/tokens/primitives;
- Component Gallery;
- production-quality Admin shell;
- production-quality Portal shell;
- strong Sidebar/TopBar/avatar/Notifications/Search/Quick Create/Àríyá foundation;
- minimal identity/Membership/permission gates;
- PWA base;
- shared states;
- accessibility and quality baseline.

Do not build Dashboard business content, CRM, Properties, Projects, Billing or another major domain.

## Step 8 — PWA from foundation
FOUND-001 includes manifest/installability/service-worker/offline-shell/update foundation and cache safety.

Full push/Notification delivery comes later, but shell/mobile/PWA composition starts immediately.

## Step 9 — Quality baseline
Use stack-appropriate:
- strict TypeScript;
- lint/format checks;
- unit/component tests;
- browser/flow tests such as Playwright where compatible;
- accessibility checks;
- development Component Gallery/visual review.

Functional tests are not the only release gate; use `09-design/performance-device-and-design-qa.md`.

## Step 10 — First fictional demo universe
FOUND-001 seeds only what it needs:
- `Re:Solve Demo Workspace`;
- Operating Entity `Airix Media`;
- fictional staff `Amina Bello` and `Chidi Okafor`;
- fictional client Organisation `Westbridge University`;
- fictional client Users/Memberships.

Later slices add canonical demo Properties/Projects/Requests/Billing/etc. from `demo-data-blueprint.md`.

Never seed real credentials, clients or staff identities.

## Step 11 — Foundation review gate
Before authoring the next build slice, run `lovable-launch/FOUND-001-REVIEW.md` and inspect:
- architecture/service/data boundaries;
- routing/auth/permission denial;
- root `AGENTS.md` and Project Knowledge consistency;
- Core UI quality;
- navigation comprehension;
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

If the foundation is visually weak or architecturally coupled, fix FOUND-001 before adding business modules.

## Step 12 — Stabilize the canonical application repository
After FOUND-001 passes, decide the GitHub naming transition using `lovable-launch/GITHUB-TRANSITION.md`.

Do not perform repository renames automatically. This is a one-time source-of-truth transition requiring explicit owner approval because the current `thathman/Re-Solve` repository contains legacy history.

## Step 13 — Author the next slice from actual FOUND-001 output
Do **not** pre-commit Lovable to a long sequence before seeing the generated foundation.

Likely early business progression may include Dashboard/Attention foundation, Organisations/Clients, Contacts/Memberships and Properties hierarchy/Posture, but the actual next slice is written only after reviewing FOUND-001's code and UX.

## Rule for every Lovable build conversation
Provide:
- exact slice id/objective;
- relevant Product Bible requirements copied into the slice prompt or already encoded in Project Knowledge/skills;
- actors/permissions;
- in scope;
- explicitly out of scope;
- required Core UI components/patterns to reuse;
- data/provenance/Attention/Notification/PWA implications;
- acceptance criteria;
- stop condition/completion report.

Product Bible file paths are traceability references; do not assume Lovable can browse the private Product Bible repository unless it is explicitly made available through a future integration.

Never dump the entire Product Bible into one prompt and never tell Lovable `build the CRM` or `build the OS`.

## Official Lovable references checked for this setup
- https://docs.lovable.dev/features/knowledge
- https://docs.lovable.dev/features/skills
- https://docs.lovable.dev/integrations/github
