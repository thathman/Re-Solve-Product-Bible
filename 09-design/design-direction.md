# Re:Solve Design Direction

## 1. Purpose

This document defines the visual and interaction direction for Re:Solve before individual screens are designed. It is intentionally product-specific. The goal is to prevent the system from drifting into a generic SaaS dashboard assembled from interchangeable cards, charts, and admin templates.

Re:Solve is an operational system. Its visual language must make dense business information calm, legible, fast to scan, and easy to act on.

## 2. Design thesis

Re:Solve should feel like a **high-trust operations workspace**: precise enough for finance and credentials, fast enough for support and project work, calm enough for all-day use, and polished enough to be client-facing.

The interface should communicate:

- control without heaviness;
- density without clutter;
- confidence without visual aggression;
- modernity without novelty for novelty's sake;
- flexibility without looking like a no-code builder;
- premium quality without decorative excess.

## 3. Anti-reference

Re:Solve must avoid:

- generic dashboard templates with rows of identical KPI cards;
- gratuitous gradients, glassmorphism, floating blobs, or decorative charts;
- excessive card nesting;
- one visual treatment reused for every data type;
- giant headings that consume operational space;
- low-information whitespace on staff screens;
- tiny text used to fake density;
- endless sidebars with every possible route visible at once;
- icon-only controls when meaning is not obvious;
- tables that collapse into unusable horizontal scrolling on mobile;
- client screens that feel like a reskinned staff dashboard;
- admin screens that feel like a marketing site.

## 4. Experience split

Re:Solve has two primary human-facing modes that share one design system but not one information density.

### Admin OS

The staff/admin experience is:

- dense;
- keyboard-friendly;
- information rich;
- interruption tolerant;
- optimized for repeated workflows;
- comfortable for long sessions;
- capable of exposing advanced actions without making every screen look complicated.

### Client Portal

The client experience is:

- task-focused;
- calmer;
- more guided;
- more explanatory;
- lower-density by default;
- mobile-first in practical use;
- focused on actions, status, transparency, and trust.

The client portal must never expose internal complexity simply because the staff system has it.

## 5. Reference qualities

Re:Solve may learn from, but should not visually imitate:

- Linear: speed, keyboard fluency, disciplined density;
- Stripe Dashboard: financial hierarchy and high-trust transaction presentation;
- GitHub: relationship-heavy records and strong information architecture;
- Notion: flexible content surfaces and calm document treatment;
- modern shadcn/Radix ecosystems: component quality and accessibility primitives;
- high-end operations software: predictable patterns and deeply considered empty/error states.

## 6. Visual hierarchy

Every screen should answer three questions within seconds:

1. Where am I?
2. What changed or needs attention?
3. What can I do next?

Hierarchy should come primarily from:

- spatial grouping;
- typography;
- contrast;
- status treatment;
- progressive disclosure;
- persistent page structure.

Do not rely on color alone.

## 7. Page anatomy

Most operational pages should use a predictable structure:

1. global shell;
2. contextual page header;
3. primary action zone;
4. summary/attention layer where warranted;
5. primary working surface;
6. secondary context or related records;
7. activity/history where appropriate.

Not every page needs every layer.

## 8. Record workspaces

First-class records such as organisations, properties, projects, invoices, contracts, and connector instances should use a consistent record workspace pattern.

A record workspace should typically provide:

- identity/header;
- status;
- ownership;
- primary actions;
- contextual metadata;
- tabs or sections;
- related records;
- activity timeline;
- audit-sensitive actions where applicable;
- plugin extension slots.

The user should feel that they are entering a workspace for the record, not opening a generic details page.

## 9. Data density

Density is contextual.

### Staff

Use compact controls, tables, inline metadata, grouped actions, and secondary information without forcing repeated navigation.

### Client

Prefer concise summaries, guided actions, strong status explanations, and fewer simultaneous controls.

### Mobile

Do not simply shrink desktop layouts. Recompose information into touch-friendly blocks, prioritized actions, expandable details, and mobile-appropriate navigation.

## 10. Color strategy

The design system should define semantic color tokens rather than hard-code feature-specific colors.

Required semantic groups:

- surface/background;
- text hierarchy;
- border/divider;
- primary action;
- neutral status;
- success;
- warning;
- danger;
- informational;
- selected/focused;
- muted/disabled.

Domain colors may exist for quick scanning, but must remain secondary to labels and icons.

## 11. Typography

Typography must support both reading and operational scanning.

Requirements:

- clear hierarchy between page titles, section titles, record names, table content, metadata, labels, and helper copy;
- numeric/tabular treatment for financial and metric-heavy surfaces;
- monospace treatment only where data benefits from it, such as API keys, IDs, code, endpoints, hashes, and certain timestamps;
- no decorative serif dependence for core usability;
- comfortable body text for knowledge, proposals, contracts, and longer client-facing content.

## 12. Motion

Motion should explain change, not decorate it.

Use motion for:

- drawers/sheets opening;
- navigation transitions where useful;
- reordering;
- state changes;
- progress;
- success confirmation;
- focus/context preservation.

Avoid excessive entrance animations on operational screens.

Respect reduced-motion preferences.

## 13. Feedback

Every user action needs an appropriate feedback mode:

- immediate inline feedback for local actions;
- toast for successful background-safe actions;
- persistent banner for important system state;
- modal confirmation for destructive/high-impact actions;
- progress state for long-running work;
- activity/audit entry for sensitive work.

Do not use toasts as the only evidence for critical actions.

## 14. State design

Every designed surface must consider:

- loading;
- skeleton;
- first-use;
- empty;
- partially configured;
- stale data;
- disconnected connector;
- permission denied;
- read-only;
- offline;
- failed action;
- retrying action;
- success;
- archived/deleted;
- degraded service.

These states are part of the design, not cleanup work after implementation.

## 15. Accessibility

Target WCAG 2.2 AA.

Mandatory:

- keyboard access;
- visible focus;
- semantic structure;
- screen-reader names;
- sufficient contrast;
- touch target sizing;
- reduced motion;
- non-color status cues;
- accessible dialogs, sheets, menus, tables, forms, and charts;
- meaningful mobile navigation.

## 16. PWA and responsive direction

Responsiveness is foundational.

The product must be designed for:

- phone;
- tablet;
- laptop;
- desktop;
- wide desktop;
- installed standalone PWA mode.

Portal mobile usage is a primary scenario. Admin mobile usage is supported, but complex staff operations may progressively disclose or defer advanced controls rather than forcing desktop density onto a phone.

## 17. Design review questions

Before approving any major flow, ask:

- Does this look specific to Re:Solve or could it be any SaaS dashboard?
- Is the most important information visually dominant?
- Are actions placed where users need them rather than where a template expects them?
- Does the screen remain useful with real, messy data?
- Does the mobile version feel designed, not collapsed?
- Are empty, error, permission, offline, and partial states intentional?
- Can a keyboard-heavy staff user move quickly?
- Can a client understand the state without internal terminology?

## 18. Lovable usage

Lovable should use its strongest current design capabilities, design skills, shadcn-based components, and compatible alternatives where they improve usability. Component choice must serve the product flow; shadcn is a foundation, not a requirement to force every interaction into the nearest stock component.

When a standard primitive is insufficient, create a Re:Solve composite component with a documented purpose and reusable behavior rather than page-specific styling.