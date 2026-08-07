# Re:Solve Design Direction

## 1. Purpose
This document defines the visual and interaction direction for Re:Solve before individual screens are designed. Re:Solve must not drift into a generic SaaS dashboard assembled from interchangeable cards, charts and admin templates.

Re:Solve is an operational system. Its visual language must make dense business information calm, legible, fast to scan and easy to act on.

## 2. Design thesis
Re:Solve should feel like a **high-trust operations workspace**: precise enough for finance and confidential access, fast enough for operational work, calm enough for all-day use and polished enough for client-facing use.

The interface communicates:
- control without heaviness;
- density without clutter;
- confidence without aggression;
- modernity without novelty for its own sake;
- flexibility without looking like a no-code builder;
- premium quality without decorative excess;
- simplicity without hiding important state.

## 3. Non-negotiable Core UI direction
Re:Solve uses a mandatory Core UI Component Framework.

Primary implementation/design sources and influences:
1. Re:Solve Product Design Language
2. shadcn/ui
3. Untitled UI React
4. Tremor
5. React Aria / Base UI / Radix where their primitive behavior is strongest
6. TanStack Table / TanStack Query and approved specialist libraries

These sources should heavily influence and be used throughout the product, but final components must be normalized into Re:Solve-owned tokens, components and composites. The product must not look like several libraries stitched together.

See `09-design/core-ui-framework.md`.

## 4. Navigation thesis
Navigation must be immediately understandable. Re:Solve should feel closer to the clarity of well-structured service CRM/navigation such as Perfex/Brevo than systems that begin with app grids, module launchers or abstract object switching.

Re:Solve must avoid:
- Odoo-style app-launcher/module-grid navigation as the main mental model;
- Twenty-style object/app navigation that requires product knowledge to find ordinary work;
- deeply nested expanding root navigation;
- showing every child page in the sidebar;
- icon-only root navigation;
- making users choose technical modules before they understand the business task.

Use a strong left navigation, strong top bar and shallow major-area structure. Secondary tabs/views appear after the user enters an area.

See `09-design/navigation-and-application-chrome.md`.

## 5. Other anti-patterns
Avoid:
- generic rows of identical KPI cards;
- gratuitous gradients, glassmorphism or decorative charts;
- excessive card nesting;
- giant headings that consume operational space;
- low-information whitespace on staff screens;
- tiny text used to fake density;
- tables that become unusable horizontal scroll on phones;
- client screens that feel like reskinned staff screens;
- admin screens that feel like marketing sites;
- generic AI sparkle buttons as the primary Àríyá identity;
- weak placeholder-quality navigation, avatar or notifications chrome.

## 6. Experience split
### Admin OS
The staff/admin experience is:
- dense but calm;
- keyboard-friendly;
- information rich;
- optimized for repeated workflows;
- interruption tolerant;
- capable of advanced actions through progressive disclosure;
- based around a simple persistent navigation model.

### Client Portal
The client experience is:
- task-focused;
- calmer;
- guided;
- explanatory;
- lower-density;
- mobile-first in practical use;
- focused on actions, status, transparency and trust.

The Portal must never expose internal complexity simply because Admin has it.

## 7. Reference qualities
Re:Solve may learn from, but should not imitate blindly:
- Perfex/Brevo: simple understandable navigation and business-area labeling;
- Linear: speed, keyboard fluency and disciplined density;
- Stripe Dashboard: financial hierarchy and high-trust transaction presentation;
- GitHub: relationship-heavy records and clear information architecture;
- Notion: flexible content surfaces;
- shadcn/Untitled UI/Tremor ecosystems: component craft, accessible primitives and data presentation.

## 8. Application chrome is a product feature
The following are first-class design work:
- side navigation;
- top bar;
- avatar/account control;
- notification trigger/tray;
- command/search entry;
- Quick Create;
- Àríyá entry and panel;
- breadcrumbs/context;
- connection/offline/update state;
- mobile navigation.

They must not remain generic starter-template components after FOUND-001.

## 9. Visual hierarchy
Every screen should answer within seconds:
1. Where am I?
2. What needs attention or changed?
3. What can I do next?

Hierarchy comes primarily from spatial grouping, typography, contrast, status treatment, progressive disclosure and predictable structure. Do not rely on color alone.

## 10. Page anatomy
Typical operational page:
1. global shell;
2. compact contextual page/record header;
3. primary actions;
4. attention/summary layer when useful;
5. primary working surface;
6. secondary context/related records;
7. collaboration/activity/history where appropriate.

Not every page needs every layer.

## 11. Record workspaces
First-class records such as Organisations, Properties, Projects, Invoices, Proposals, Contracts and Connector Instances use a consistent record-workspace pattern:
- identity/header;
- status;
- ownership;
- primary actions;
- contextual metadata;
- tabs/sections;
- related records;
- collaboration/activity;
- audit-sensitive actions;
- plugin extension slots.

The experience should feel like entering the record's workspace, not opening a generic details page.

## 12. Attention over dashboard decoration
Dashboards and summary surfaces should begin with decisions/actions/attention, then supporting information. Avoid a sea of equal KPI cards.

Tremor-style metrics/trackers/charts may be used heavily where they answer real operational questions.

## 13. Data density
### Staff
Use compact controls, tables, inline metadata, grouped actions and secondary context without requiring constant navigation.

### Client
Prefer concise summaries, guided actions and strong status explanations.

### Mobile
Recompose the experience. Never simply shrink desktop density.

## 14. Color and status
Use semantic tokens for surface, text, borders, primary action, neutral, success, warning, danger, informational, selected/focus and muted states. Domain colors may assist scanning but never replace labels/icons.

## 15. Typography
Typography supports operational scanning and longer documents. Use tabular numerals where useful for finance/metrics. Use monospace only for data that benefits from it, such as identifiers, endpoints and hashes.

## 16. Motion
Motion explains change rather than decorates it. Respect reduced motion. Avoid excessive entrance animations on operational screens.

## 17. Feedback and states
Every meaningful surface considers loading, skeleton, first-use, empty, stale, disconnected, permission denied, read-only, offline, retrying, failure, success, archived and degraded states.

Toasts are not the only evidence for critical actions.

## 18. Accessibility
Target WCAG 2.2 AA. Keyboard access, visible focus, semantic structure, screen-reader names, contrast, touch targets, reduced motion, accessible overlays/forms/tables/charts and meaningful mobile navigation are mandatory.

## 19. Responsive/PWA
Design for phone, tablet, laptop, desktop, wide desktop and installed PWA. Portal mobile is a primary scenario. Admin mobile remains useful for essential operational work without pretending every dense workflow should look identical to desktop.

See `09-design/performance-device-and-design-qa.md`.

## 20. Component Gallery and design QA
FOUND-001 establishes a development-only Component Gallery/Storybook-equivalent surface. Major feature completion includes functional, security, responsive/PWA, accessibility, Core UI consistency, visual-polish and degraded/performance review.

## 21. Design review questions
Before approving a major flow ask:
- Is this unmistakably Re:Solve?
- Could a new user predict where this feature lives?
- Is the important information dominant?
- Is the correct Core UI component being reused?
- Does it remain useful with real messy data?
- Does the mobile version feel designed?
- Are empty/error/permission/offline/stale states intentional?
- Can keyboard-heavy staff move quickly?
- Can a client understand the state without internal jargon?
- Have shadcn, Untitled UI and Tremor been used/influenced appropriately rather than ignored?

## 22. Lovable usage
Lovable must use its strongest current design capabilities and the Re:Solve Core UI Framework. Do not accept stock starter-template chrome as final foundation work.

When a standard primitive is insufficient, create a documented reusable Re:Solve composite rather than page-specific styling.
