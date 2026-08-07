---
name: airix-ui
description: Design or refine Re:Solve screens, navigation, dashboards, record workspaces, panels, and portal surfaces with deliberate non-generic operational UX.
---

# Airix UI

## Design intent
Re:Solve should feel dense but calm, fast, legible, and domain-specific. Avoid generic SaaS dashboard composition.

## Use first
Read the relevant Product Bible feature spec plus:
- `09-design/design-direction.md`
- `09-design/design-system.md`

## Rules
- Use shadcn/ui and accessible Radix-style primitives by default.
- Use stronger specialist components only when they materially improve the interaction.
- Reuse established tokens and patterns.
- Do not create a one-off design system inside a page.
- Distinguish information from action and attention from context.
- Prefer strong hierarchy over decorative card grids.
- Avoid meaningless charts, excessive badges, gradients, glassmorphism, and giant empty hero areas.

## Responsive behavior
Design intentionally for:
- phone
- tablet
- laptop
- desktop

Admin may be denser on larger screens; Portal must be especially touch-friendly.
Never squeeze desktop tables/navigation into phone widths without adaptation.

## Interaction quality
Check:
- keyboard access
- focus order
- hover/focus/pressed/disabled states
- touch targets
- dialogs/drawers
- destructive action separation
- reduced motion
- empty/loading/error states

## Completion
Explain the hierarchy and interaction choices. Flag any place where the source spec is ambiguous rather than inventing product behavior silently.
