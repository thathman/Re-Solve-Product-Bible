---
name: resolve-feature
description: Implement one bounded Re:Solve feature slice from the Product Bible. Use for a specific page, flow, record workspace, platform capability, or small feature in Lovable.
---

# Re:Solve Feature

## Rule
Build only the requested slice. Adjacent Product Bible capability is context, not permission to implement it.

## Before building
1. Read the cited Product Bible sources and canonical expansion decisions.
2. Restate actor and measurable goal.
3. Restate in-scope and out-of-scope work.
4. Identify permissions/scope, states, Attention/Notifications, provenance, PWA, API/service boundaries, plugins/connectors and Core UI components.
5. Confirm the slice does not introduce HR, timesheets or Client Service Consumption.

## During implementation
- preserve canonical terminology;
- reuse Core UI components before bespoke UI;
- use shadcn/Untitled UI/Tremor sourcing rules;
- prefer complete flows over broad scaffolding;
- keep provider/data logic behind services/connectors;
- enforce authorization beyond navigation hiding;
- use realistic fictional demo data only when needed.

## Required states
Consider default, loading/skeleton, empty/first-use, success, error, partial/stale, permission denied, read-only, mobile and offline/online-only.

## Completion
Verify acceptance, responsive behavior, accessibility, negative authorization, Core UI consistency, Product Bible drift and explicit out-of-scope items.
