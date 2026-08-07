---
name: resolve-ui
description: Use when creating or refining a Re:Solve page, panel, dashboard, record workspace, Portal surface, shared visual component, or interaction that must follow the Core UI Framework and non-generic product design language.
---

# Re:Solve UI

Read these canonical public Product Bible files first when the task affects UI foundation or component sourcing:
- `09-design/design-direction.md`
- `09-design/design-system.md`
- `09-design/core-ui-framework.md`
- `09-design/navigation-and-application-chrome.md`
- `10-build/ui-stack-installation.md`
- `10-build/foundation-engineering-guardrails.md`

Repository root: `https://github.com/thathman/Re-Solve-Product-Bible`

## Non-negotiable sources
Use shadcn/ui, Untitled UI React and Tremor heavily as primary sources/influences. Use React Aria/Base UI/Radix for strong accessible primitive behavior and TanStack/specialist tools where justified.

For a fresh compatible foundation, prefer the current Tailwind v4 path, shadcn with React Aria base, targeted Untitled UI React component integration, and Tremor Raw/copy-paste components. Never downgrade the stack or initialize a second app merely to use a UI source.

Normalize final components into Re:Solve-owned tokens/composites. Do not produce library soup.

## Source/licensing rule
Prefer free/open-source commercially usable components by default. Record materially imported/copied UI sources and licenses in the application's UI provenance ledger. Untitled UI PRO assets/components require an appropriate owner license and must never be copied into the public Product Bible merely because they are available to a licensed user.

## UI checks
- clear information hierarchy;
- simple understandable navigation;
- strong Sidebar/TopBar/avatar/notifications/Àríyá chrome when affected;
- no generic KPI-card dashboard;
- no Odoo app-grid or Twenty-style object/module navigation;
- coherent light/dark/system theme behavior;
- deliberate licensed typography and one primary icon vocabulary;
- desktop/tablet/phone composition;
- keyboard/touch behavior;
- accessibility/reduced motion;
- complete loading/empty/error/stale/permission/offline states;
- reusable components represented in Component Gallery.
