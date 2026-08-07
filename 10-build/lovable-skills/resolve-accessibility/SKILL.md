---
name: resolve-accessibility
description: Use when reviewing or implementing a Re:Solve interface for WCAG 2.2 AA, keyboard/focus behavior, screen-reader semantics, contrast, reduced motion, touch targets, accessible forms/tables/overlays, and non-color state communication.
---

# Re:Solve Accessibility

Read the affected feature spec, Core UI Framework, responsive/PWA requirements and any sensitive-action flow.

## Baseline
Target WCAG 2.2 AA for core Admin and Client Portal surfaces. Prefer mature accessible primitives over custom imitation.

## Review
Check:
- semantic headings/landmarks;
- accessible names/descriptions;
- keyboard reachability and logical focus order;
- visible focus;
- dialogs/drawers/popovers focus trap/restore;
- menus/comboboxes/date pickers/table controls;
- skip/navigation behavior where useful;
- form labels, help, required state, inline + summary errors and announcements;
- contrast and status not conveyed by color alone;
- text zoom/large text and long labels;
- reduced motion;
- touch target size/spacing;
- drag/drop keyboard alternative;
- charts with understandable textual/table alternative;
- data tables with headers, sort/selection state and mobile alternative;
- loading/success/error announcements where material;
- timeouts/session/security actions with understandable recovery.

## PWA/mobile
Test standalone mode, screen zoom, orientation, safe areas and on-screen keyboard. Client Portal common flows must be fully accessible on phone.

## Output
List blockers first, then important issues and polish. Include exact affected component/flow and expected accessible behavior. Do not mark complete merely because automated scans pass.