---
name: resolve-design-review
description: Use after a UI-heavy Re:Solve build slice, redesign, or major component change to evaluate visual hierarchy, Core UI consistency, source-library influence, interaction polish, responsive quality, and generic-SaaS drift before acceptance.
---

# Re:Solve Design Review

Read Design Direction, Design System, Core UI Framework, Navigation/Application Chrome and the affected feature spec.

## Review dimensions
### Re:Solve identity
Does the result feel like one coherent Re:Solve product rather than raw shadcn, raw Untitled UI, raw Tremor, or a starter admin template?

### Mandatory influences
Verify shadcn/ui, Untitled UI React and Tremor materially influence the implementation where appropriate. React Aria/Base UI/Radix and TanStack should be used when their interaction/data primitives are the better fit.

### Hierarchy
Check what the eye sees first, second and third. Attention/action/state should outrank decoration. Remove unnecessary card wrappers and visual noise.

### Application chrome
Inspect Sidebar, TopBar, avatar/account, Notifications, Search/Command, Quick Create, Àríyá, breadcrumbs and mobile navigation with the same rigor as feature content.

### Typography and density
Check readable type scale, line length, data density, spacing rhythm, label/value hierarchy, long names, empty space and dense operational screens.

### States
Review loading, skeleton, empty, first-use, error, permission denied, partial/stale, offline, destructive confirmation, long-content and high-count states.

### Responsive
Review phone, tablet, laptop and desktop composition. Mobile must be recomposed rather than desktop stacked blindly.

### Interaction polish
Check hover/focus/pressed/disabled, keyboard flows, touch targets, sticky behavior, overlays, drawers, transitions and reduced motion.

### Data visualization
Every chart/metric must answer an operational question and provide an understandable detail path.

## Anti-patterns
Reject generic KPI walls, oversized marketing-style heroes in operations, meaningless gradients/glass, excessive pills, weak active nav, tiny dense controls, inconsistent radii/spacing, decorative charts, and one-off components that bypass the Core UI Framework.

## Output
Report PASS / NEEDS REFINEMENT / FAIL with concrete findings grouped as critical, important and polish. Recommend specific Core UI changes rather than vague aesthetic comments.