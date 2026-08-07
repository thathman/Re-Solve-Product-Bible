---
name: resolve-dashboard
description: Use when building or reviewing a Re:Solve dashboard, overview, executive summary, operational pulse, analytics landing surface, or other multi-domain summary page.
---

# Re:Solve Dashboard

Read the relevant Dashboard/Reports/Product Bible spec, Attention Engine, Core UI Framework, data provenance, notification boundaries, and permission rules.

## Principle
A Re:Solve dashboard is an operating brief, not a generic KPI-card wall.

Prioritize:
1. unresolved Attention;
2. decisions/actions due;
3. meaningful change;
4. current operational/commercial state;
5. trends only when they help a decision.

## Composition
Prefer strong briefing blocks, prioritized queues, compact metric strips, trackers, lists, timelines and explainable health/posture over repeating identical cards.

Tremor should materially influence metrics/data visualization. shadcn/Untitled UI/Core Framework govern interaction and overall composition.

Every metric/chart must answer a stated question. Provide drill-down/detail paths. Do not use decorative charts.

## Data truth
- permission-filter counts and aggregates server-side;
- show source/freshness for connector-derived or delayed metrics;
- distinguish deterministic facts from Àríyá inference;
- avoid unexplained health scores;
- do not duplicate Notification Center or My Work as shadow datasets.

## Responsive
Desktop may use multi-column density. Tablet adapts to two/one columns. Phone becomes a priority feed led by Attention and current actions, not a long stack of every desktop widget.

## States
Include calm all-clear, loading/skeleton, no-data/first-use, partial sources, stale data, connector degradation, permission-limited sections, error and offline-safe stale snapshot states.

## Completion
Explain why each visual exists, verify every fact can be inspected, verify hidden records do not leak through counts, and run design/accessibility/release review before acceptance.