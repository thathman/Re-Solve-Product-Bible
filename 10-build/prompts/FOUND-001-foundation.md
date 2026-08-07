# FOUND-001 — Re:Solve Application + Core UI Foundation

## Objective
Prepare Re:Solve as a Lovable-first, portable, responsive application foundation without implementing business modules.

After this slice, reviewers must be able to launch the app, authenticate into representative Admin and Client Portal shells, inspect a production-quality Core UI Component Framework, verify strong navigation/application chrome across devices, and confirm the project is ready for bounded feature slices.

## Product Bible sources
Read and follow:
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

## Actor and goal
Internal staff and client users can enter a coherent Re:Solve application shell that resolves their correct experience, feels intentionally designed across devices, and establishes the reusable component/architecture quality required for all future modules.

## In scope

### 1. Inspect current Re-Solve source
Treat the existing application repository as behavior/reference material only. Reuse useful assets/ideas but do not preserve legacy architecture merely because it exists.

### 2. Establish application architecture
Use Lovable's strongest current React/full-stack patterns and Supabase where appropriate.

Create clear boundaries for:
- app shells;
- shared Core UI;
- auth/identity;
- Principal/User/Membership concepts;
- permissions;
- domain/data services;
- plugin/connector extension points.

Do not scaffold every future domain.

### 3. Build the Re:Solve Core UI Component Framework — NON-NEGOTIABLE
This is a primary deliverable, not optional polish.

Mandatory source hierarchy/influence:
1. Re:Solve design language;
2. shadcn/ui;
3. Untitled UI React;
4. Tremor;
5. React Aria / Base UI / Radix where strongest;
6. TanStack-style table/query patterns and approved specialist libraries only where needed.

Use these heavily while normalizing final components into Re:Solve-owned tokens/components. Do not create a library-soup interface.

Establish tokens/primitives for typography, surfaces, spacing, borders, radii, elevation, semantic status, focus, motion, controls, overlays, skeletons, states and navigation.

Establish the first application primitives, including:
- AppShell;
- AdminSidebar;
- PortalNavigation;
- TopBar;
- NavSection/NavItem/NavBadge;
- MobileNav;
- GlobalSearch/Command entry;
- QuickCreate;
- ResolveAvatar;
- AccountMenu;
- NotificationTrigger and demo NotificationTray;
- AriyaTrigger and demo/non-functional AriyaPanel foundation;
- BreadcrumbTrail;
- PageHeader;
- reusable loading/empty/error/permission/offline/not-built/connection states.

### 4. Create a Component Gallery
Create a development-only Component Gallery/Storybook-equivalent route/tooling showing foundational components across realistic variants/states.

At minimum demonstrate:
- buttons/inputs/status;
- avatars/account menu;
- Sidebar states;
- TopBar;
- notification trigger/tray demo;
- Àríyá trigger/panel demo;
- page headers;
- overlays;
- loading/empty/error/permission/offline/not-built states;
- phone/tablet/desktop behavior where useful.

### 5. Establish Admin shell — production-quality foundation
Admin navigation must be simple and obvious, using the shallow hierarchy defined in the Navigation spec.

Do not implement an Odoo-style app grid/module launcher or Twenty-style object/app switching model.

Include:
- strong responsive Sidebar;
- strong TopBar;
- visible Search/Command entry;
- Quick Create demo menu;
- Àríyá entry demo;
- Notification entry/tray demo;
- ResolveAvatar/AccountMenu;
- current context/breadcrumb behavior;
- active-route states;
- collapsed power-user state;
- phone/tablet navigation adaptation.

Routes may point to explicit `Not built in this slice` states. Do not create feature pages behind them.

### 6. Establish Client Portal shell
Create calmer client navigation only.

Include:
- simple Portal navigation;
- responsive/mobile-first composition;
- notification/account chrome;
- support/chat entry placeholder;
- optional Àríyá entry placeholder only if it does not complicate the shell;
- client-safe not-built/empty states.

Do not build Portal Home business content.

### 7. Identity/demo foundation
Using Supabase if appropriate, create only the identity data needed to demonstrate:
- Human User;
- staff versus client context;
- one Workspace;
- Airix Media as Operating Entity;
- client Organisation membership;
- role/capability resolution;
- Admin versus Portal route access;
- permission-denied state.

Do not build complete Team & Access management.

### 8. Permission-gate foundation
Create a reusable capability-aware guard/policy pattern. Do not rely on navigation hiding.

Demonstrate:
- staff allowed into Admin;
- client allowed into Portal;
- client denied from Admin;
- deliberate permission-denied page/state.

### 9. PWA base
Establish manifest, icons/placeholders, installable configuration, service-worker/offline-shell strategy, update lifecycle foundation, safe fallback shell and explicit sensitive-cache policy.

Do not implement full push delivery yet.

### 10. Accessibility baseline
Verify keyboard navigation, focus visibility, semantic landmarks, overlay focus behavior, touch targets, contrast and reduced motion.

### 11. Quality baseline
Use tooling appropriate to the Lovable-generated stack for TypeScript, linting, component/unit testing and browser/flow testing.

Add only dependencies needed by FOUND-001.

## Explicitly out of scope
Do not implement:
- Dashboard business widgets/Attention engine behavior;
- Organisations/Contacts CRUD;
- CRM;
- Properties or native monitoring execution;
- Projects;
- Requests;
- Client Lifecycle;
- Sales/Document Studio;
- Billing;
- Chatwoot/WhatsApp/Cloudflare integrations;
- Secure Vault;
- Notifications delivery engine;
- Automations;
- plugin runtime beyond extension-friendly boundaries;
- Connectors UI;
- public API product surface;
- MCP;
- functional Àríyá provider/tools;
- Monitoring/Property Posture;
- Reports;
- full Settings;
- Custom Fields;
- Import/Export/Data Quality;
- HR;
- Timesheets/Time Tracking;
- Client Service Consumption.

Do not create placeholder schemas for all future modules.

## Demo data
Use fictional development data.

Seed only:
- Workspace: `Re:Solve Demo Workspace`;
- Operating Entity: `Airix Media`;
- staff user `Amina Bello` — Owner/Administrator demo;
- staff user `Chidi Okafor` — Account Manager demo;
- client Organisation `Westbridge University`;
- client user `Dr. Nneka Okorie` — Organisation Admin demo;
- restricted client user `Samuel Mensah` — limited-scope placeholder if useful without building Properties.

Credentials/auth setup must be obviously development-only. Do not use real clients, real staff identities or real secrets.

## Responsive expectations
### Phone
- Portal genuinely usable;
- Admin essential navigation usable;
- no squeezed desktop sidebar;
- no page-level horizontal overflow;
- Search, Notifications, Account and current context reachable;
- Àríyá entry does not obstruct primary work.

### Tablet
Adaptive navigation and near-desktop shell where appropriate.

### Laptop/Desktop
Efficient navigation, strong hierarchy and no excessive empty space.

Review representative widths from the performance/device spec.

## Security checks
- no secrets in client bundle/source;
- client cannot access Admin via URL manipulation;
- permission checks are not visual-only;
- demo configuration is clearly non-production;
- auth/session handling follows provider best practice.

## Portability checks
Run `self-host-check` before completion.

Confirm exported source is portable, Lovable-only runtime dependencies are not product-critical, Supabase/provider usage is reasonably centralized and Re:Solve identity/permission concepts are represented independently from provider-specific UI calls.

## Acceptance criteria
1. App launches cleanly in Lovable.
2. Staff demo user enters Admin shell.
3. Client demo user enters Portal shell.
4. Client cannot access Admin shell.
5. Admin and Portal share Core UI tokens but visibly differ in density/navigation.
6. AdminSidebar and TopBar are strong production-quality foundation components, not generic placeholders.
7. ResolveAvatar/AccountMenu is polished and useful.
8. NotificationTrigger/Tray demo is polished enough to establish the canonical interaction.
9. Search/Command and Quick Create entry patterns are canonical.
10. Àríyá has a distinctive global trigger/panel foundation without functional provider integration.
11. shadcn, Untitled UI and Tremor materially influence the Core UI Framework.
12. Component Gallery exists and demonstrates foundational states/components.
13. phone/tablet/desktop layouts are intentional.
14. PWA manifest/service-worker foundation exists with safe cache policy.
15. shared loading/error/empty/permission/offline/not-built states exist.
16. no major business module was prematurely implemented.
17. WCAG-oriented keyboard/focus/touch baseline is present.
18. configured quality checks pass.
19. portability review finds no unnecessary Lovable runtime lock-in.
20. no HR, timesheet or Client Service Consumption schema/feature was introduced.

## Required Lovable completion report
Return:
- architecture chosen and why;
- Core UI source/library decisions;
- Core Framework components created;
- Component Gallery coverage;
- meaningful files changed;
- dependencies added;
- identity/demo schema;
- routes;
- tests/checks/results;
- responsive/PWA checks;
- accessibility/design QA checks;
- portability concerns;
- Product Bible contradictions found;
- explicit adjacent features intentionally left unbuilt.

## Stop condition
After FOUND-001 passes, stop. Do not proceed into Dashboard, Clients, CRM, Properties, Projects or another business module until a new build slice is provided.
