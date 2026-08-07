# Start Re:Solve in Lovable

Use this document when the Product Bible planning PR stack is merged and you are ready to spend the first Lovable build credits.

## Before opening the first build prompt
Confirm:
- Product Bible is merged/canonical;
- you have owner/admin access to the intended Lovable workspace;
- the correct GitHub account is connected/available;
- you understand that Lovable creates a new GitHub repository rather than importing the existing legacy `thathman/Re-Solve` repository;
- no legacy repository rename is being performed yet.

## 1. Create the workspace/project
Prefer a dedicated Re:Solve Lovable workspace because Re:Solve has a substantial workspace-skill catalogue.

Create a fresh project named **Re:Solve**.

Do not ask Lovable to build the OS in the initial project-creation description. Keep the first creation/setup prompt minimal if the UI requires one; substantive work starts only after Knowledge and Skills are configured.

## 2. Connect GitHub
Connect the Re:Solve project to the correct GitHub installation. Allow Lovable to create a new private repository and start two-way sync.

Do not attempt to attach/import the existing `thathman/Re-Solve` repository.

Record the new repository name in `BUILD-STATE.md` or your project notes. Keep the old repository unchanged until the post-FOUND-001 transition gate.

## 3. Add Project Knowledge
Open **Project settings → Knowledge** and paste the contents of:

`10-build/lovable-launch/PROJECT-KNOWLEDGE.md`

Do not paste the entire Product Bible.

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

## 4. Install canonical Skills
Follow `10-build/lovable-skills/INSTALL.md` and `manifest.md`.

Because the Product Bible is private, use ZIP/`.skill` upload or exact manual copy unless a dedicated public skills mirror is created later.

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

Remove/disable any obsolete `airix-*` skills if they exist.

## 5. Backend choice
Do not create the complete future database before the first slice.

When FOUND-001 needs auth/demo identity, allow Lovable to use its current preferred Supabase/Lovable development flow. Create only the minimal Workspace/Operating Entity/User/Membership/Organisation/capability data required by FOUND-001.

## 6. Send FOUND-001
Open:

`10-build/prompts/FOUND-001-foundation.md`

Send the complete slice prompt with its required skills attached. Do not append requests for Dashboard/CRM/Properties/etc.

The first meaningful build should result in:
- source-controlled app foundation;
- root `AGENTS.md`;
- Core UI Component Framework;
- Component Gallery;
- polished Admin shell;
- polished Portal shell;
- strong Sidebar/TopBar/Avatar/Notifications/Search/Quick Create/Àríyá foundation;
- minimal identity/permission demonstration;
- responsive/PWA/accessibility/test foundation.

## 7. Do not accept the first render automatically
Run the review sequence:
1. `/resolve-design-review`
2. `/resolve-security-review`
3. `/resolve-responsive`
4. `/resolve-pwa`
5. `/resolve-accessibility`
6. `/self-host-check`
7. `/resolve-release`

Use `FOUND-001-REVIEW.md` as the human checklist.

If the shell looks generic or navigation/application chrome is weak, refine FOUND-001 before building any business module.

## 8. Stop after FOUND-001
Do not ask Lovable for the next feature immediately.

Capture:
- actual new GitHub repository name;
- stack/dependencies selected;
- routes/components created;
- schema/migrations;
- test results;
- screenshots/visual notes if useful;
- portability concerns;
- Product Bible ambiguities;
- review result: PASS / CONDITIONAL / FAIL.

Only then author the next bounded slice based on the real generated application.

## 9. Repository naming transition
If FOUND-001 passes, review `GITHUB-TRANSITION.md`. Repository renaming/archive actions require explicit owner approval and are not part of FOUND-001 itself.

## Current official Lovable references
- Knowledge: https://docs.lovable.dev/features/knowledge
- Skills: https://docs.lovable.dev/features/skills
- Git sync: https://docs.lovable.dev/integrations/github
