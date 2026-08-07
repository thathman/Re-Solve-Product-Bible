---
name: resolve-feature
description: Use when implementing one bounded Re:Solve feature slice, page, flow, platform capability, or small Product Bible-defined increment in Lovable without expanding into adjacent future work.
---

# Re:Solve Feature

## Rule
Build only the requested slice. Adjacent Product Bible capability is context, not permission to implement it.

## Before building
1. Read the cited Product Bible sources and canonical expansion decisions.
2. For FOUND-001 or any foundation/Core UI work, also read `10-build/ui-stack-installation.md` and `10-build/foundation-engineering-guardrails.md` from the public Product Bible.
3. Restate actor and measurable goal.
4. Restate in-scope and out-of-scope work.
5. Identify permissions/scope, states, Attention/Notifications, provenance, PWA, API/service boundaries, plugins/connectors and Core UI components.
6. Confirm the slice does not introduce HR, timesheets or Client Service Consumption.

Public Product Bible root: `https://github.com/thathman/Re-Solve-Product-Bible`

## During implementation
- preserve canonical terminology;
- reuse Core UI components before bespoke UI;
- use shadcn/Untitled UI/Tremor sourcing rules;
- preserve one package manager/lockfile and deterministic dependency setup;
- keep environment/secrets explicit and validated;
- prefer complete flows over broad scaffolding;
- keep provider/data logic behind services/connectors;
- enforce authorization beyond navigation hiding;
- use locale-aware formatting utilities rather than hard-coded currency/date/time display;
- use realistic fictional demo data only when needed.

## Required states
Consider default, loading/skeleton, empty/first-use, success, error, partial/stale, permission denied, read-only, mobile and offline/online-only.

## Completion
Verify acceptance, responsive behavior, accessibility, negative authorization, Core UI consistency, Product Bible drift, CI/source-build health, dependency/license provenance, environment safety and explicit out-of-scope items.
