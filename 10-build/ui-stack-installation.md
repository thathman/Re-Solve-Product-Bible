# Re:Solve UI Stack Installation & Compatibility Playbook

## Purpose
This is the canonical build-side instruction for installing and combining the Re:Solve Core UI Component Framework sources in Lovable.

The goal is **not** to install every UI package available. The goal is to establish one coherent Re:Solve-owned component system while drawing heavily from shadcn/ui, Untitled UI React and Tremor.

## Canonical stack decision
For a fresh Re:Solve application, prefer:

1. React + TypeScript using Lovable's current generated stack;
2. Tailwind CSS **v4-compatible** styling;
3. shadcn/ui as the primary source-owned component registry;
4. **React Aria as the preferred shadcn component base** for a fresh project, because Untitled UI React also uses React Aria;
5. Untitled UI React for high-quality application patterns/components and visual treatment;
6. **Tremor Raw / copy-and-paste components** for dashboards, monitoring, metrics and data visualization;
7. TanStack Query for server/async state where needed;
8. TanStack Table for operational data tables when the first real table slice requires it;
9. specialist dependencies only when a selected component/flow actually requires them.

Do not create three competing component systems. External sources feed the Re:Solve Core UI Framework; feature code should consume Re:Solve-owned components/patterns.

## Mandatory preflight before installing anything
Lovable must first inspect the generated repository and report:
- React version;
- package manager/lockfile;
- Tailwind version and configuration;
- whether shadcn is already initialized (`components.json`, existing `components/ui`, aliases, CSS variables);
- which primitive base existing shadcn components use, if already present;
- existing React Aria, Base UI or Radix dependencies;
- existing chart/table/query dependencies;
- any version conflict that would require a migration rather than a normal install.

**Do not blindly rerun an initializer over an existing configured project.**

If the generated project already has shadcn configured on another supported base and switching would overwrite working components, stop and report the migration choice instead of mixing bases unpredictably.

## 1. Tailwind compatibility
Re:Solve should remain on the current Tailwind v4-compatible path used by the fresh Lovable application.

Hard rules:
- do not downgrade Tailwind to v3 merely to install the legacy Tremor component package;
- do not maintain separate Tailwind theme systems for shadcn, Untitled UI and Tremor;
- normalize external tokens into Re:Solve semantic tokens;
- document any required Tailwind/plugin dependency introduced by a copied component.

## 2. shadcn/ui
### Preferred fresh-project base
For a fresh project that is not already initialized, prefer the current shadcn React Aria base:

```bash
npx shadcn@latest init --base aria
```

Use the equivalent command for the repository's package manager where appropriate.

If Lovable already initialized shadcn correctly, **do not run `init` again**. Inspect and extend the existing configuration.

### Add only components required by the current slice
FOUND-001 will likely need a subset such as:

```bash
npx shadcn@latest add button input label select combobox avatar badge tooltip popover dropdown-menu dialog alert-dialog sheet tabs separator skeleton command sidebar
```

The exact list is determined after inspecting what Lovable already generated. Do not reinstall/overwrite an existing component without reviewing the diff.

### Re:Solve ownership rule
Components added through shadcn become source-owned application code. They must be normalized into Re:Solve tokens/variants and then reused through canonical Re:Solve components such as `ResolveAvatar`, `AdminSidebar`, `TopBar`, `NotificationTray`, and `CommandPalette`.

Do not leave stock shadcn styling as the product identity.

## 3. Untitled UI React
Untitled UI React is a mandatory major source/influence, but it should be integrated into the existing Re:Solve application rather than used to scaffold a second application.

### Do not run a new-project initializer inside Re:Solve
Do **not** run `untitledui init` in a way that creates/replaces the existing Lovable app.

For an existing React/Tailwind application, use component-level installation/copying.

Untitled UI's documented core dependencies for manual integration include:

```bash
npm install @untitledui/icons react-aria-components tailwindcss-react-aria-components tailwind-merge tailwindcss-animate
```

Use the actual project package manager.

Where the CLI supports adding an individual required component, prefer targeted component import, for example:

```bash
npx untitledui@latest add <component-name>
```

Before copying/importing any Untitled component:
- inspect its dependencies;
- map its theme values into Re:Solve tokens;
- reuse existing React Aria/shadcn primitives where sensible;
- avoid creating duplicate Button/Input/Dialog/Select implementations unless the Untitled implementation is explicitly chosen to replace the canonical one;
- record the component in the Component Gallery.

Untitled UI should strongly influence navigation, application chrome, forms, settings, filters, tables, record headers, menus and polished state design.

## 4. Tremor
### Default choice: Tremor Raw
Use **current Tremor Raw / copy-and-paste React components** as the preferred Re:Solve Tremor path.

Tremor Raw is Tailwind v4-compatible and source-owned after copying, which fits the Re:Solve component strategy.

**Do not install the older `@tremor/react` component package by default.** Its older installation path was designed around the previous Tailwind v3-era Tremor library and should not cause Re:Solve to downgrade or fork the styling stack.

### Add Tremor components only when they answer a real operational question
For FOUND-001, use Tremor influence/components only where useful to demonstrate data-visualization tokens or a small Component Gallery example. Do not build Dashboard business content yet.

Later likely uses include:
- Metric / MetricDelta;
- spark charts;
- progress circles;
- trackers;
- BarList;
- uptime/availability visuals;
- monitoring/renewal summaries;
- financial/reporting charts.

Tremor Raw components may require dependencies such as `recharts`, `@remixicon/react`, or a specific Radix primitive. Install only the dependency required by the selected component, e.g.:

```bash
npm install recharts @remixicon/react
```

or the specific documented Radix package for the copied component.

Do not introduce Tremor's colors/spacing as a parallel design system. Adapt the component to Re:Solve tokens and Component Gallery states.

## 5. React Aria / Base UI / Radix policy
Re:Solve does not install all three primitive systems globally just because they are approved.

Preferred approach for a fresh foundation:
- React Aria = primary interactive primitive base through shadcn + Untitled UI;
- Base UI = approved specialist alternative when it materially provides a better primitive and does not duplicate/conflict with the canonical implementation;
- Radix = approved when required by a Tremor Raw/specialist component or when it is the stronger implementation for a specific control.

Never mix primitive bases for the same canonical component casually.

If a component has multiple candidate implementations, choose once at the Core UI layer and document the choice.

## 6. TanStack Query
Install when FOUND-001 or the first data-backed slice needs explicit async/server-state behavior:

```bash
npm install @tanstack/react-query
```

Use it for controlled loading, error, retry, invalidation, caching and mutation state rather than scattering bespoke request state across components.

Do not add it only because it is listed in the Product Bible if Lovable's generated stack already provides an equivalent that is clearly superior and portable. Report such a deviation.

## 7. TanStack Table
Install when the first operational table/list requires it:

```bash
npm install @tanstack/react-table
```

Do not install/build a large table framework during FOUND-001 merely to satisfy future scope. The Core UI may define the DataTable contract without implementing every future table capability yet.

## 8. Icon strategy
Use one primary icon vocabulary in ordinary Re:Solve chrome. Prefer the icon system already selected by the generated shadcn/Lovable foundation (commonly Lucide) unless the Core UI review deliberately changes it.

Untitled UI icons or Remix icons may be used where a selected source component requires them, but do not visibly mix icon styles throughout ordinary navigation.

Normalize icon size, stroke/weight, alignment and semantic use through Re:Solve components.

## 9. Forms and validation
When actual forms are introduced, prefer:
- React Hook Form;
- Zod;
- the canonical Re:Solve form primitives.

Install only when the current slice needs them and they are not already present:

```bash
npm install react-hook-form zod @hookform/resolvers
```

FOUND-001 may include only the minimal form primitives needed for the Component Gallery/shell.

## 10. Dependency ownership and package-manager rule
Never assume `npm` if the Lovable-generated repository uses `pnpm`, `bun` or another lockfile.

Use the repository's established package manager consistently. Do not create multiple lockfiles.

Every added dependency must have:
- a current-slice reason;
- compatible React/Tailwind requirements;
- acceptable license/maintenance posture;
- portability outside Lovable;
- no overlap with an already chosen canonical component unless justified.

## 11. FOUND-001 expected installation outcome
At the end of FOUND-001, reviewers should be able to identify:
- the actual Tailwind version/configuration;
- shadcn configuration and chosen primitive base;
- which Untitled UI components/patterns were materially incorporated;
- which Tremor Raw component(s)/patterns were materially incorporated;
- all added UI dependencies and why;
- Re:Solve semantic tokens;
- Re:Solve-owned Core UI components built on those sources;
- Component Gallery evidence;
- no Tailwind downgrade or duplicate parallel design system.

## 12. Prohibited setup patterns
Do not:
- scaffold a second Untitled UI application inside the Lovable project;
- initialize shadcn repeatedly over an existing setup;
- install `@tremor/react` and downgrade Tailwind to satisfy it;
- install React Aria + Base UI + Radix wholesale without a component-level reason;
- add every future dashboard/table/form dependency during FOUND-001;
- copy external components without reconciling tokens/accessibility/responsive behavior;
- preserve external component names/styles as separate mini design systems throughout feature code;
- create multiple lockfiles;
- let a package installation silently alter the product's navigation or visual language.

## Official references checked for this decision
- shadcn Vite/install docs: https://ui.shadcn.com/docs/installation/vite
- shadcn React Aria base: https://ui.shadcn.com/docs/changelog/2026-07-react-aria
- Untitled UI installation: https://www.untitledui.com/react/docs/installation
- Untitled UI CLI: https://www.untitledui.com/react/docs/cli
- Tremor Raw installation: https://www.tremor.so/docs/getting-started/installation
- Tremor Raw model: https://www.tremor.so/docs/getting-started/about
- TanStack Query: https://tanstack.com/query/latest/docs/framework/react/installation
- TanStack Table: https://tanstack.com/table/latest
