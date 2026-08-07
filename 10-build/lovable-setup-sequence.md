# Re:Solve Lovable Setup Sequence

## Purpose
Use this sequence to start Re:Solve in Lovable without broad-scope generation or repository confusion.

## 0. Canonical sources
- Public Product Bible: `https://github.com/thathman/Re-Solve-Product-Bible`
- Legacy application/reference: `thathman/Re-Solve`
- New application source: repository created by Lovable Git sync
- Lovable: active build environment, not a required production runtime

The public Product Bible is specification truth and the source for GitHub-imported Re:Solve skills. Public access does not make every documented feature current build scope.

## 1. Create a dedicated Re:Solve workspace/project
Prefer a dedicated Lovable workspace because custom skills are workspace-level.

Create a fresh project named **Re:Solve**. Do not ask Lovable to build the whole OS during project creation.

## 2. Connect GitHub
Connect the correct GitHub account and let Lovable create a new private synced application repository.

Do not attempt to import or overwrite the existing `thathman/Re-Solve` legacy repository. Keep the Product Bible separate from the writable application repository.

Record the new application repository in `10-build/lovable-launch/BUILD-STATE.md`.

## 3. Add Project Knowledge
Paste:

`10-build/lovable-launch/PROJECT-KNOWLEDGE.md`

into **Project settings → Knowledge**.

Do not paste the whole Product Bible into Knowledge. Project Knowledge is for always-on rules; exact public Product Bible files may be referenced by a bounded build slice when needed.

## 4. Import Re:Solve Skills from GitHub
Follow:
- `10-build/lovable-skills/INSTALL.md`
- `10-build/lovable-skills/manifest.md`

Preferred path:
**Settings → Skills → Add → Import from GitHub**

Use one public skill subdirectory per import:

`https://github.com/thathman/Re-Solve-Product-Bible/tree/main/10-build/lovable-skills/<skill-name>`

Before FOUND-001 verify:
- `resolve-feature`
- `resolve-ui`
- `resolve-shell`
- `resolve-navigation`
- `resolve-responsive`
- `resolve-accessibility`
- `resolve-design-review`
- `resolve-security-review`
- `resolve-pwa`
- `resolve-release`
- `self-host-check`

ZIP/`.skill` or exact manual copy are fallback methods only. Do not ask Lovable to regenerate canonical Re:Solve skills.

## 5. Confirm foundation rules
Before the first build, Project Knowledge and skills must already enforce:
- one app with Admin OS + Client Portal;
- source-owned Core UI Component Framework;
- shadcn/ui, Untitled UI React and Tremor as major sources/influences;
- accessible primitives and responsive/PWA behavior from foundation;
- simple shallow business navigation;
- no Odoo-style app grid or Twenty-style primary module/object switching;
- production-quality Sidebar, TopBar, Account, Notifications, Search/Command, Quick Create and Àríyá chrome;
- capability + scope authorization;
- portability/self-hostability;
- no HR, payroll, recruitment, attendance, Timesheets/Time Tracking or Client Service Consumption.

## 6. Backend only as needed
Allow Lovable to use its preferred Supabase/Lovable development flow when FOUND-001 needs identity/demo data.

Create only the minimal Workspace, Operating Entity, User, Membership, Organisation and capability data needed by FOUND-001. Do not pre-create future domain schemas.

## 7. Execute FOUND-001 only
Use:

`10-build/prompts/FOUND-001-foundation.md`

Attach the required foundation skills. Do not append Dashboard, CRM, Properties, Projects, Billing or other business-domain requests.

FOUND-001 creates the application architecture, Core UI Framework, Component Gallery, Admin shell, Portal shell, identity/permission demonstration, PWA baseline, shared states and quality foundation.

## 8. Review before continuing
Run:
1. `/resolve-design-review`
2. `/resolve-security-review`
3. `/resolve-responsive`
4. `/resolve-pwa`
5. `/resolve-accessibility`
6. `/self-host-check`
7. `/resolve-release`

Then complete:

`10-build/lovable-launch/FOUND-001-REVIEW.md`

If foundation design, responsiveness, accessibility, permissions, portability or tests are weak, fix FOUND-001 before adding business modules.

## 9. Record actual build state
Update:

`10-build/lovable-launch/BUILD-STATE.md`

with the actual Lovable repository, stack, dependencies, routes, components, schema/migrations, tests and review result.

## 10. Repository-name transition later
Only after FOUND-001 passes, use:

`10-build/lovable-launch/GITHUB-TRANSITION.md`

for the one-time canonical application repository naming decision. Do not rename/archive repositories during FOUND-001.

## 11. Author the next slice from reality
The next slice is written only after reviewing the actual FOUND-001 output. Public Product Bible access is for precision and traceability, not permission to build future capability early.

## Official references
- https://docs.lovable.dev/features/knowledge
- https://docs.lovable.dev/features/skills
- https://docs.lovable.dev/integrations/github
