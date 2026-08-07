---
name: airix-data-table
description: Build or refine Re:Solve operational lists and data-heavy tables with filters, saved views, bulk actions, responsive alternatives, and permission-aware behavior.
---

# Airix Data Table

Read the relevant feature spec and design system first.

Define intentionally:
- columns and default order
- sorting
- filtering
- global and field search
- pagination or virtualisation where justified
- saved views
- column visibility
- row selection
- bulk actions
- row actions
- sticky behavior where useful
- permission-sensitive columns/actions
- export only when the product spec allows it

States:
- loading/skeleton
- empty
- no-search-results
- error
- partial data
- permission-limited data

Mobile:
Do not force wide desktop tables into phone layouts. Use compact cards, stacked rows, priority columns, or horizontal detail patterns as appropriate.

Accessibility:
Ensure headers, sort state, selection, bulk actions, keyboard access, and focus are understandable to assistive technology.

Avoid adding a heavyweight grid library unless the current slice truly requires capabilities unavailable in existing primitives.
