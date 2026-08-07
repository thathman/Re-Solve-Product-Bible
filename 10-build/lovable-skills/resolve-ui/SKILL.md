---
name: resolve-ui
description: Use when creating or refining a Re:Solve page, panel, dashboard, record workspace, Portal surface, shared visual component, or interaction that must follow the Core UI Framework and non-generic product design language.
---

# Re:Solve UI

Read `09-design/design-direction.md`, `09-design/design-system.md`, `09-design/core-ui-framework.md`, and `09-design/navigation-and-application-chrome.md` first.

## Non-negotiable sources
Use shadcn/ui, Untitled UI React and Tremor heavily as primary sources/influences. Use React Aria/Base UI/Radix for strong accessible primitive behavior and TanStack/specialist tools where justified.

Normalize final components into Re:Solve-owned tokens/composites. Do not produce library soup.

## UI checks
- clear information hierarchy;
- simple understandable navigation;
- strong Sidebar/TopBar/avatar/notifications/Àríyá chrome when affected;
- no generic KPI-card dashboard;
- no Odoo app-grid or Twenty-style object/module navigation;
- desktop/tablet/phone composition;
- keyboard/touch behavior;
- accessibility/reduced motion;
- complete loading/empty/error/stale/permission/offline states;
- reusable components represented in Component Gallery.
