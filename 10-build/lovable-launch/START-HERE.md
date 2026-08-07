# Start Re:Solve in Lovable

Use this document when the Product Bible is canonical and you are ready to start supervised Lovable development.

## Before the first substantive Lovable message
Confirm:
- `thathman/Re-Solve-Product-Bible` is public and canonical;
- you have owner/admin access to the intended Lovable workspace;
- the correct GitHub account is connected/available;
- you understand that Lovable creates a new GitHub repository rather than importing the existing legacy `thathman/Re-Solve` repository;
- no legacy repository rename is being performed yet.

## 1. Create the workspace/project
Prefer a dedicated Re:Solve Lovable workspace because Re:Solve has a substantial workspace-skill catalogue.

Create a fresh project named **Re:Solve**.

Do not ask Lovable to build the OS in the project-creation description. Keep creation minimal.

## 2. Connect GitHub
Connect the Re:Solve project to the correct GitHub installation. Allow Lovable to create a new private application repository and start two-way sync.

Do not attempt to attach/import the existing `thathman/Re-Solve` repository.

The public Product Bible is specification/reference material and is not the writable application repository.

## 3. Send SETUP-000
The first substantive project-chat instruction is:

`10-build/prompts/SETUP-000-lovable-bootstrap.md`

This tells Lovable to:
- load the canonical Project Knowledge;
- attempt to install/import the canonical `resolve-*` workspace skills itself from the public Product Bible;
- verify the required FOUND-001 skills;
- remove/flag obsolete `airix-*` skills;
- report any one-time workspace-owner UI action that cannot be performed from project chat;
- stop before product implementation.

Do **not** manually recreate skills unless Lovable reports that its current session cannot perform the documented import action. If a one-time Settings action is required, use the exact public URLs in `10-build/lovable-skills/GITHUB-IMPORT-URLS.md`.

## 4. Return the SETUP-000 report to the supervisor
Bring Lovable's setup report back to ChatGPT.

ChatGPT is the build supervisor and will provide the next concise prompt. Do not improvise the next feature or send FOUND-001 until the supervisor reviews setup readiness.

See `10-build/lovable-launch/SUPERVISOR-PROTOCOL.md`.

## 5. Foundation compatibility guardrails
Before FOUND-001, the supervisor will ensure Lovable uses:
- `10-build/ui-stack-installation.md`
- `10-build/foundation-engineering-guardrails.md`

These define Tailwind/shadcn/Untitled/Tremor compatibility, dependency/source licensing, package-manager/lockfile rules, environment validation, CI, error boundaries/observability, locale/timezone/currency readiness, theme/typography/icon governance and UI provenance.

Important defaults include:
- inspect generated stack before running any initializer;
- remain on a Tailwind v4-compatible path;
- prefer shadcn React Aria base for a fresh compatible project;
- integrate Untitled UI component-by-component rather than scaffolding a second app;
- prefer Tremor Raw/current copy-paste components rather than the legacy `@tremor/react` path;
- use free/open-source UI sources by default unless a separate license is explicitly approved;
- do not upgrade/downgrade React/Tailwind merely to satisfy one UI source without compatibility review.

## 6. FOUND-001 comes only after setup review
When setup passes, the supervisor will provide a short execution prompt pointing Lovable at:

`10-build/prompts/FOUND-001-foundation.md`

The supervisor prompt does not repeat the Product Bible. Lovable uses Project Knowledge, installed skills and exact canonical files referenced by the step.

FOUND-001 establishes only:
- source-controlled application foundation;
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

Do not append Dashboard/CRM/Properties/Projects/Billing/etc.

## 7. Review before any next feature
After FOUND-001, return Lovable's completion report and relevant screenshots/results to ChatGPT.

The supervisor will guide the review sequence, using:
- `FOUND-001-REVIEW.md`
- `FOUND-001-ENGINEERING-REVIEW.md`
- relevant `resolve-*` review skills.

Do not move into another business module because Lovable says `done`.

## 8. Stop-and-supervise model
For every subsequent step:
1. Lovable completes the bounded instruction and stops.
2. User returns the result to ChatGPT.
3. ChatGPT reviews actual state.
4. ChatGPT gives the next concise Lovable prompt.
5. Repeat.

The user should not need to restate PRD content, determine build order or choose applicable Re:Solve skills. Those are supervisor responsibilities except where a genuine owner decision is required.

## 9. Repository naming transition
If FOUND-001 passes, the supervisor will review `GITHUB-TRANSITION.md` with the user. Repository rename/archive actions require explicit owner approval.

## Current official Lovable references
- Knowledge: https://docs.lovable.dev/features/knowledge
- Skills: https://docs.lovable.dev/features/skills
- Git sync: https://docs.lovable.dev/integrations/github
