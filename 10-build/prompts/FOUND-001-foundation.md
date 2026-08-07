# FOUND-001 — Re:Solve Application + Core UI Foundation

## Send with these Lovable skills
Where Lovable slash-skill invocation is available, attach:

`/resolve-feature /resolve-shell /resolve-navigation /resolve-ui /resolve-responsive /resolve-pwa /resolve-accessibility /self-host-check /resolve-release`

After the first complete visual pass, run `/resolve-design-review` before accepting this slice.

## Objective
Prepare Re:Solve as a Lovable-first, portable, responsive application foundation **without implementing business modules**.

After this slice, reviewers must be able to launch the app, enter representative Admin and Client Portal shells, inspect a production-quality Re:Solve Core UI Component Framework, verify strong navigation/application chrome across devices, and confirm the project is ready for bounded feature slices.

## Context authority
The private `Re-Solve-Product-Bible` is canonical product truth. The paths listed below are **traceability references for reviewers**; do not assume you can browse that private repository from Lovable.

Your direct implementation context is:
1. Re:Solve Project Knowledge already loaded in this Lovable project;
2. the installed canonical `resolve-*` skills invoked for this slice;
3. this complete FOUND-001 prompt.

If this prompt conflicts with Project Knowledge or a loaded Re:Solve skill, stop and report the exact conflict before changing product behavior.

### Product Bible traceability
This slice was derived from:
- `00-foundation/product-thesis.md`
- `00-foundation/principles.md`
- `00-foundation/canonical-expansion-decisions.md`
- `00-foundation/terminology.md`
- `00-foundation/actors-and-roles.md`
- `00-foundation/domain-model.md`
- `00-foundation/information-architecture.md`
- `00-foundation/operating-entities-and-brands.md`
- `09-design/design-direction.md`
- `09-design/design-system.md`
- `09-design/core-ui-framework.md`
- `09-design/navigation-and-application-chrome.md`
- `09-design/performance-device-and-design-qa.md`
- `01-admin/shell.md`
- `02-portal/shell.md`
- `03-platform/pwa.md`
- `04-ai/ariya-experience.md`
- `08-security/security-architecture.md`
- `10-build/lovable-knowledge.md`
- `10-build/architecture-portability-checklist.md`
- `10-build/demo-data-blueprint.md`
- `10-build/lovable-launch/AGENTS.md.template`

## Repository rule
This Lovable project must use the **new GitHub repository created by Lovable Git sync**. Do not attempt to import, overwrite or reproduce the current legacy `thathman/Re-Solve` repository in this slice.

The legacy repository is reference evidence outside this build. FOUND-001 starts a clean Lovable-first application foundation based on the product rules above.

Create a root-level `AGENTS.md` in the new application repository using the canonical repository-instruction content supplied with this launch pack. Keep it consistent with Project Knowledge so durable engineering/product rules also live in exported source control.

## Actor and goal
Internal staff and client users can enter a coherent Re:Solve application shell that resolves their correct experience, feels intentionally designed across devices, and establishes the reusable component/architecture quality required for all future modules.

# In scope

## 1. Establish application architecture
Use Lovable's strongest current React/full-stack patterns and Supabase only where this slice benefits from it.

Establish clear boundaries for:
- app shells/routing;
- shared Re:Solve Core UI;
- auth/identity;
- Principal/User/Membership concepts;
- capability + scope permissions;
- domain/data service or repository access;
- future plugin/connector extension points;
- application configuration/environment handling.

Do not scaffold future domain modules merely to demonstrate architecture.

## 2. Build the Re:Solve Core UI Component Framework — NON-NEGOTIABLE
This is a primary FOUND-001 deliverable, not later polish.

Mandatory source hierarchy/influence:
1. Re:Solve design language;
2. **shadcn/ui**;
3. **Untitled UI React**;
4. **Tremor**;
5. React Aria / Base UI / Radix where they provide the strongest accessible behavior;
6. TanStack-style table/query patterns and approved specialist libraries only where actually needed.

shadcn, Untitled UI and Tremor must **materially influence the implemented foundation**. Use them heavily while normalizing the final patterns into Re:Solve-owned tokens/components. Do not create an interface where different areas visibly look like unrelated libraries.

Establish coherent tokens for:
- typography;
- surfaces/backgrounds;
- semantic foregrounds/borders;
- spacing;
- dimensions;
- radii;
- elevation;
- semantic status/priority;
- focus;
- motion/reduced motion;
- density;
- responsive behavior;
- data visualization basics.

Create/refine the foundational Re:Solve components needed by this slice, including:
- AppShell;
- AdminSidebar;
- PortalNavigation;
- TopBar;
- NavSection / NavItem / NavBadge;
- MobileNav;
- GlobalSearch / CommandPalette entry;
- QuickCreate;
- ResolveAvatar;
- AccountMenu;
- NotificationTrigger;
- demo NotificationTray / NotificationItem;
- AriyaTrigger;
- demo/non-functional AriyaPanel foundation;
- BreadcrumbTrail;
- PageHeader;
- Button/Input/Select/Combobox and basic form primitives required to demonstrate the system;
- Dialog/Drawer/Popover/Menu/Tooltip primitives required by the shell;
- loading/skeleton;
- EmptyState;
- ErrorState;
- PermissionState;
- OfflineState;
- NotBuiltState;
- ConnectionState.

Do not build domain composites that belong to later slices.

## 3. Create a Component Gallery
Create a **development-only Component Gallery / Storybook-equivalent** inside the application source.

It must be a serious visual regression/review surface, not a forgotten debug page.

At minimum demonstrate:
- typography/tokens;
- buttons/inputs/basic form controls;
- statuses/badges;
- avatars and AccountMenu;
- AdminSidebar expanded/collapsed/active/count/long-label states;
- TopBar;
- NotificationTrigger/Tray with realistic grouped/unread/priority states;
- Àríyá trigger/panel foundation;
- Search/Command and Quick Create entry;
- PageHeader/breadcrumbs;
- dialogs/drawers/popovers/menus;
- loading/skeleton/empty/error/permission/offline/not-built/connection states;
- representative phone/tablet/desktop shell previews or test routes.

Use realistic Re:Solve copy rather than lorem ipsum.

## 4. Establish the Admin shell — production-quality foundation
Admin navigation must be simple, shallow and understandable like a strong service-CRM application.

**Do not implement:**
- Odoo-style app launcher/module grid;
- Twenty-style object/app/module switching as the primary navigation model;
- icon-only root navigation;
- deeply nested accordion trees;
- every future child page as a root sidebar item.

Use the canonical major-area shape as navigation placeholders only:

```text
Home
  Dashboard
  My Work

Clients
CRM
Properties
Projects
Sales
Billing
Support

Operations
  Monitoring
  Renewals
  Requests
  Knowledge
  Files
  Vault
  Automations
  Reports

Platform
  Connectors
  Plugins
  Audit
  Settings
```

These destinations may render polished `Not built in FOUND-001` states. **Do not build their business functionality.**

Admin shell must include:
- strong responsive labeled Sidebar;
- clear active section/route state;
- collapsed power-user state with accessible tooltips/discoverability;
- strong TopBar;
- current context/breadcrumb behavior;
- visible Search/Command entry;
- Quick Create demo menu;
- Àríyá entry/panel demo;
- Notification entry/tray demo;
- ResolveAvatar/AccountMenu;
- meaningful ConnectionState only when relevant;
- deliberate phone/tablet navigation adaptation;
- keyboard navigation and visible focus.

Stock starter-template shell quality is a failure condition.

## 5. Establish the Client Portal shell
Create a visibly related but calmer client shell.

Use simple destination placeholders such as:
- Home
- Properties
- Projects
- Support
- Billing
- Approvals
- Files
- Knowledge
- Organisation

Vault should not be a default visible destination for a user with no authorized Vault access. Requests may remain contextual/not-built until its own slice.

Include:
- simple Portal navigation;
- strong responsive/mobile-first composition;
- notification/account chrome;
- support/chat entry placeholder;
- optional Àríyá entry placeholder only if it remains calm and unobtrusive;
- explicit client-safe NotBuilt/empty/error/permission states.

Do not build Portal Home business content or Chatwoot integration.

## 6. Identity/demo foundation
Using Supabase where appropriate, create only the data needed to demonstrate:
- one Workspace;
- Airix Media as Operating Entity;
- Human User;
- staff vs client context;
- one fictional client Organisation;
- Membership/role/capability context;
- Admin vs Portal route access;
- a reusable permission-denied state.

Do not build Team & Access administration.
Do not model Airix Media as a client Organisation.
Do not use email alone as canonical identity.

## 7. Permission-gate foundation
Create a reusable capability-aware route/action guard/policy pattern. UI visibility is convenience only; authorization must not depend on hidden navigation.

Demonstrate:
- staff allowed into Admin;
- client allowed into Portal;
- client denied from Admin even by direct URL;
- representative permission denial/read-only behavior.

Add at least one negative authorization test or equivalent verifiable path appropriate to the chosen stack.

## 8. PWA base
Establish:
- manifest;
- app icons/placeholders appropriate to Re:Solve;
- installable configuration;
- service-worker/offline-shell strategy;
- app update lifecycle foundation;
- safe offline fallback;
- explicit cache classification/boundaries;
- no sensitive/Vault data caching;
- future push-compatible structure without implementing full push delivery.

## 9. Responsive baseline
Design and verify intentionally for:
- small/large phone;
- tablet;
- common laptop;
- desktop.

Do not simply stack the entire desktop shell vertically.

Phone must keep Search, Notifications, Account and current context reachable. Àríyá must not obstruct primary work. No unexplained page-level horizontal overflow.

## 10. Accessibility baseline
Target WCAG 2.2 AA for foundational components.

Verify:
- semantic landmarks/headings;
- keyboard navigation;
- visible focus;
- menus/overlays focus behavior;
- accessible names/descriptions;
- contrast/non-color status cues;
- touch targets;
- reduced motion;
- screen-reader-understandable states.

## 11. Quality/tooling baseline
Use tooling appropriate to the generated stack for:
- strict TypeScript;
- linting/formatting;
- unit/component tests;
- browser/flow testing such as Playwright where compatible;
- accessibility/design review where practical.

Add only dependencies needed for FOUND-001. Do not install future domain libraries merely because the Product Bible mentions them.

# Explicitly out of scope
Do **not** implement:
- Dashboard business widgets or real Attention Engine behavior;
- Organisations/Contacts CRUD;
- CRM;
- Properties or monitoring execution;
- Projects/Tasks;
- Requests;
- Client Lifecycle;
- Sales/Document Studio;
- Billing/payment integration;
- Chatwoot/WhatsApp/Cloudflare integrations;
- Secure Vault;
- Notification delivery engine/preferences;
- Automations;
- real Plugin runtime beyond extension-friendly boundaries;
- Connector management UI;
- public API product surface;
- MCP;
- functional Àríyá provider/tools;
- Monitoring/Property Posture;
- Reports;
- full Settings;
- Custom Fields;
- Import/Export/Data Quality;
- HR/payroll/recruitment/leave/attendance/performance features;
- Timesheets or Time Tracking;
- Client Service Consumption/usage-credit metering.

Do not create placeholder database schemas for these future domains.

# Demo data
Use fictional development identities only:
- Workspace: `Re:Solve Demo Workspace`;
- Operating Entity: `Airix Media`;
- staff user `Amina Bello` — Owner/Administrator demo;
- staff user `Chidi Okafor` — Account Manager demo;
- client Organisation `Westbridge University`;
- client user `Dr. Nneka Okorie` — Organisation Admin demo;
- restricted client user `Samuel Mensah` — limited-scope demo where useful.

Credentials/auth setup must be obviously development-only. Do not use real clients, real staff identities or real secrets.

# Security checks
- no secrets in client bundle/source/demo data;
- client cannot access Admin through URL manipulation;
- permission checks are not visual-only;
- demo auth configuration is clearly non-production;
- sensitive cache policy is explicit;
- no future high-risk Actions are implemented casually.

# Portability checks
Run `self-host-check` before completion.

Confirm:
- exported source is ordinary maintainable application code;
- no product-critical Lovable-only runtime dependency;
- Supabase/provider usage is reasonably centralized;
- Re:Solve identity/permission concepts are not merely provider metadata;
- PWA/config/components are source-controlled;
- root `AGENTS.md` exists;
- no production infrastructure work was invented.

# Acceptance criteria
1. App launches cleanly in Lovable.
2. New Lovable GitHub repository is synced successfully.
3. Root `AGENTS.md` contains the durable Re:Solve repository rules.
4. Staff demo user enters Admin shell.
5. Client demo user enters Portal shell.
6. Client cannot access Admin shell directly.
7. Admin and Portal share Core UI tokens but visibly differ in density/navigation.
8. shadcn/ui, Untitled UI React and Tremor materially influence the implemented Core UI foundation.
9. AdminSidebar is a strong production-quality component with clear active/collapsed/responsive states.
10. TopBar is strong and includes visible Search/Command, Quick Create, Àríyá, Notifications and useful Account access.
11. ResolveAvatar/AccountMenu is polished and useful, not merely `Profile / Log out`.
12. NotificationTrigger/Tray demo establishes the canonical interaction.
13. Àríyá has a distinctive global trigger/panel foundation without provider integration.
14. Navigation is shallow/labeled and does not use the rejected Odoo/Twenty mental models.
15. Component Gallery exists and demonstrates foundational components/states.
16. phone/tablet/laptop/desktop layouts are intentional.
17. PWA manifest/service-worker/offline-shell/update foundation exists with safe cache policy.
18. shared loading/error/empty/permission/offline/not-built/connection states exist.
19. configured quality checks pass or exact blockers are reported.
20. WCAG-oriented keyboard/focus/touch baseline is present.
21. portability review finds no unnecessary Lovable runtime lock-in.
22. no major business module was prematurely implemented.
23. no HR, Timesheet/Time Tracking or Client Service Consumption schema/feature was introduced.

# Required completion report
Return:
- architecture chosen and why;
- GitHub sync/repository state;
- root `AGENTS.md` confirmation;
- Core UI source/library decisions and actual use;
- Core Framework components created;
- Component Gallery coverage;
- meaningful files changed;
- dependencies added and why;
- identity/demo schema/data;
- routes;
- tests/checks/results;
- responsive/PWA checks;
- accessibility checks;
- design review findings;
- security/permission checks;
- portability concerns;
- Product Bible/Knowledge contradictions found;
- explicit adjacent features intentionally left unbuilt.

# Stop condition
After FOUND-001 and its review pass, **stop**. Do not proceed into Dashboard, Clients, CRM, Properties, Projects, Billing or another business module until a new bounded build slice is supplied.
