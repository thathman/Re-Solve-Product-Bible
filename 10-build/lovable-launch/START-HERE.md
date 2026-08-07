# Start Re:Solve in Lovable

Use this document when the Product Bible planning stack is merged and you are ready to spend the first Lovable build credits.

## Before opening the first build prompt
Confirm:
- Product Bible is merged/canonical;
- `thathman/Re-Solve-Product-Bible` is public and available for Lovable skill import/reference;
- you have owner/admin access to the intended Lovable workspace;
- the correct GitHub account is connected/available;
- you understand that Lovable creates a new GitHub repository rather than importing the existing legacy `thathman/Re-Solve` repository;
- no legacy repository rename is being performed yet.

## 1. Create the workspace/project
Prefer a dedicated Re:Solve Lovable workspace because Re:Solve has a substantial workspace-skill catalogue.

Create a fresh project named **Re:Solve**.

Do not ask Lovable to build the OS in the initial project-creation description. Keep the first creation/setup prompt minimal if the UI requires one; substantive work starts only after Knowledge and Skills are configured.

## 2. Connect GitHub
Connect the Re:Solve project to the correct GitHub installation. Allow Lovable to create a new private application repository and start two-way sync.

Do not attempt to attach/import the existing `thathman/Re-Solve` repository.

The public Product Bible is a specification/reference repository and is **not** the application repository Lovable should write application code into.

Record the new application repository name in `BUILD-STATE.md` or your project notes. Keep the old repository unchanged until the post-FOUND-001 transition gate.

## 3. Add Project Knowledge
Open **Project settings → Knowledge** and paste the contents of:

`10-build/lovable-launch/PROJECT-KNOWLEDGE.md`

Do not paste the entire Product Bible.

The public Product Bible may be linked/referenced when a build slice needs an exact supporting spec, but always-on rules belong in Project Knowledge and task-specific rules belong in Skills/current build prompts.

Verify the saved Knowledge includes these unmistakable phrases/concepts:
- `Àríyá`;
- `Core UI Component Framework — NON-NEGOTIABLE`;
- shadcn/ui + Untitled UI React + Tremor;
- simple Perfex/Brevo-like navigation;
- no Odoo/Twenty navigation model;
- no HR/Timesheets/Client Service Consumption;
- native Monitoring;
- Chatwoot boundary;
- portable/self-hostable after export.

## 4. Install canonical Skills from GitHub
Follow `10-build/lovable-skills/INSTALL.md` and `manifest.md`.

Preferred method: **Settings → Skills → Add → Import from GitHub**.

Import each required skill from its public Product Bible subdirectory:

`https://github.com/thathman/Re-Solve-Product-Bible/tree/main/10-build/lovable-skills/<skill-name>`

For FOUND-001, verify at least:
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

ZIP/`.skill` upload or exact manual copy remains a fallback if GitHub import is temporarily unavailable.

Remove/disable any obsolete `airix-*` skills if they exist.

## 5. Read the foundation compatibility guardrails
Before asking Lovable to install or copy UI dependencies, make these two public files part of the FOUND-001 context:

- `10-build/ui-stack-installation.md`
- `10-build/foundation-engineering-guardrails.md`

They define the current Tailwind/shadcn/Untitled/Tremor compatibility path, dependency/source licensing, package-manager/lockfile rules, environment validation, CI, error-boundary/observability foundation, locale/timezone/currency readiness, theme/typography/icon governance and UI provenance requirements.

Important defaults include:
- inspect the generated stack before running any initializer;
- remain on a Tailwind v4-compatible path;
- prefer shadcn's React Aria base for a fresh compatible project;
- integrate Untitled UI component-by-component rather than scaffolding a second application;
- prefer Tremor Raw/current copy-paste components rather than the legacy `@tremor/react` path;
- use free/open-source UI sources by default unless a separate license is explicitly approved;
- do not downgrade the stack to satisfy a component library.

## 6. Backend choice
Do not create the complete future database before the first slice.

When FOUND-001 needs auth/demo identity, allow Lovable to use its current preferred Supabase/Lovable development flow. Create only the minimal Workspace/Operating Entity/User/Membership/Organisation/capability data required by FOUND-001.

## 7. Send FOUND-001
Open:

`10-build/prompts/FOUND-001-foundation.md`

Send the complete slice prompt with its required skills attached. Tell Lovable that `10-build/ui-stack-installation.md` and `10-build/foundation-engineering-guardrails.md` are mandatory companion specifications for this foundation slice.

Do not append requests for Dashboard/CRM/Properties/etc.

The first meaningful build should result in:
- source-controlled app foundation;
- root `AGENTS.md`;
- Core UI Component Framework;
- Component Gallery;
- polished Admin shell;
- polished Portal shell;
- strong Sidebar/TopBar/Avatar/Notifications/Search/Quick Create/Àríyá foundation;
- minimal identity/permission demonstration;
- responsive/PWA/accessibility/test foundation;
- deterministic package/runtime setup;
- environment example/validation boundary;
- minimal CI/source-build gate;
- UI provenance/license ledger;
- locale-aware formatting foundation;
- coherent light/dark/system theme foundation.

## 8. Do not accept the first render automatically
Run the review sequence:
1. `/resolve-design-review`
2. `/resolve-security-review`
3. `/resolve-responsive`
4. `/resolve-pwa`
5. `/resolve-accessibility`
6. `/self-host-check`
7. `/resolve-release`

Use both human review checklists:
- `FOUND-001-REVIEW.md`
- `FOUND-001-ENGINEERING-REVIEW.md`

If the shell looks generic, navigation/application chrome is weak, source build/CI fails, UI licensing is unclear, or the generated stack had to be downgraded to accommodate a library, refine FOUND-001 before building any business module.

## 9. Stop after FOUND-001
Do not ask Lovable for the next feature immediately.

Capture:
- actual new GitHub repository name;
- stack/dependencies selected;
- routes/components created;
- schema/migrations;
- test/CI results;
- UI source/license provenance;
- runtime/package manager/Tailwind/shadcn base;
- theme/typography/icon decisions;
- locale/timezone/currency formatting approach;
- screenshots/visual notes if useful;
- portability concerns;
- Product Bible ambiguities;
- review result: PASS / CONDITIONAL / FAIL.

Only then author the next bounded slice based on the real generated application.

## 10. Repository naming transition
If FOUND-001 passes, review `GITHUB-TRANSITION.md`. Repository renaming/archive actions require explicit owner approval and are not part of FOUND-001 itself.

## Current official Lovable references
- Knowledge: https://docs.lovable.dev/features/knowledge
- Skills: https://docs.lovable.dev/features/skills
- Git sync: https://docs.lovable.dev/integrations/github
