---
name: resolve-responsive
description: Use when designing, implementing, or reviewing Re:Solve layouts across phone, tablet, laptop, desktop, wide desktop, touch, keyboard, and narrow/long-content states without changing the feature's business scope.
---

# Re:Solve Responsive Experience

Read the affected feature spec, `03-platform/pwa.md`, Core UI Framework and performance/device QA spec.

## Rule
Responsive design means intentional recomposition, not stacking every desktop region vertically and calling it mobile.

## Review breakpoints conceptually
- small phone;
- large phone;
- tablet portrait/landscape where relevant;
- common laptop;
- desktop;
- wide desktop only where extra width materially helps.

Use implementation breakpoints that fit the chosen Tailwind/Lovable stack; do not create arbitrary breakpoint sprawl.

## Patterns
- Sidebar becomes deliberate drawer/sheet/mobile navigation;
- record context rails become drawers/sections;
- tables become priority columns, stacked rows/cards, or deliberate horizontal detail only when unavoidable;
- tabs may become scrollable tabs or section menus;
- forms simplify to logical single-column groups;
- sticky actions respect safe areas and the software keyboard;
- charts preserve legibility and data alternatives;
- long labels/names wrap or truncate with accessible full context.

## Admin
Dense desktop is allowed. Essential operations such as navigation, lookup, Attention, Notifications, approvals, incidents and quick updates must remain usable on phone.

## Portal
Common client flows must be first-class on phone.

## State testing
Check loading, empty, error, offline, permission states, maximum counts, long names, long translated copy readiness, large text/zoom and on-screen keyboard interactions.

## Completion
No unexplained page-level overflow, inaccessible actions, tiny touch targets or desktop-only primary flow. Record any intentionally desktop-optimized complex editor explicitly.