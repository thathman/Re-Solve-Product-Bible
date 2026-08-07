---
name: resolve-navigation
description: Use when adding, changing, reviewing, or reorganizing Re:Solve Admin or Client Portal navigation, route hierarchy, area tabs, plugin navigation contributions, breadcrumbs, mobile navigation, or discoverability.
---

# Re:Solve Navigation

Read `09-design/navigation-and-application-chrome.md`, the relevant shell spec, information architecture, Core UI Framework and permission rules.

## Non-negotiable direction
Navigation must be simple and predictable like a well-structured service CRM. Preserve a clear mental model closer to Perfex/Brevo clarity than Odoo-style app launchers or Twenty-style object/module switching.

## Admin
Default to one clear labeled desktop sidebar with shallow major areas. Keep child pages inside the area's tabs/views rather than exposing every subpage at root.

Before adding a root item ask:
1. Can this be a tab/view inside an existing major area?
2. Is it frequent/important enough for root navigation?
3. Is the label obvious to a non-technical operator?
4. How does it work on phone?

## Prohibited patterns
- app/module launcher as the primary mental model;
- icon-only root navigation;
- deeply nested accordion trees;
- duplicate destinations in several root groups;
- technical architecture terms as ordinary navigation labels;
- uncontrolled plugin root entries;
- a second permanent sidebar inside every record.

## Top-level behavior
Strong active route/section state, long-label handling, keyboard access, collapsed power-user mode, meaningful counts only, and utility/platform areas separated from daily work.

## Portal
Use even simpler goal-oriented navigation. Hide unavailable destinations cleanly. Global Notifications/Account should not bloat the main destination list.

## Mobile
Recompose, do not shrink desktop. Keep current context, search, notifications and account reachable. Portal may use bottom navigation for validated high-frequency destinations plus a clear More surface.

## Permission behavior
Navigation visibility is convenience only. Server-side authorization remains mandatory. Do not leak inaccessible counts through hidden/disabled entries.

## Completion
Run a first-time-user test: a new staff/client user should be able to predict where major work lives from labels alone. If the root grows noticeably, justify every addition.