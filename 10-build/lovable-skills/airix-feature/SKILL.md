---
name: airix-feature
description: Implement one bounded Re:Solve feature slice from the Product Bible. Use when building a specific page, flow, record workspace, platform capability, or small feature in Lovable.
---

# Airix Feature

## Rule
Build only the requested slice. The Product Bible may describe adjacent future capability; do not implement it unless the current slice explicitly includes it.

## Before building
1. Read the cited Product Bible files/sections.
2. Restate the actor and measurable goal.
3. Restate in-scope work.
4. Restate out-of-scope adjacent work.
5. Identify affected permissions, states, notifications, PWA behavior, API/service boundaries, plugins, and connectors.
6. Reuse existing Re:Solve primitives before adding dependencies or bespoke components.

## During implementation
- Preserve canonical terminology.
- Prefer complete flows over broad scaffolding.
- Use realistic demo data only when needed.
- Keep data/provider logic out of presentational components where practical.
- Do not bypass permission checks because demo data is trusted.
- Do not create generic placeholder dashboards when the spec defines operational hierarchy.

## Required states
Consider and implement where applicable:
- default
- loading/skeleton
- empty
- first-use
- success
- error
- partial data
- permission denied
- read-only/disabled
- mobile
- offline/online-only

## Completion checks
Before completion:
- verify acceptance criteria
- verify phone/tablet/desktop behavior
- verify accessibility basics
- verify permissions/negative paths
- verify no unrelated future feature was added
- report any conflict with Product Bible

## Completion report
Return:
- what was built
- significant files/surfaces changed
- schema/data changes
- tests/checks performed
- known limitations
- out-of-scope items intentionally untouched
