---
name: resolve-record-workspace
description: Use when building or refining a Re:Solve 360/detail workspace for a first-class record such as an Organisation, Contact, Property, Project, Opportunity, Invoice, Incident, Request, Service, or other durable business record.
---

# Re:Solve Record Workspace

Read the record's Product Bible spec plus `09-design/core-ui-framework.md`, `09-design/navigation-and-application-chrome.md`, Collaboration, Attention, Activity, Files/Vault, provenance, and permission rules that apply.

## Goal
Create a record workspace that answers: what is this, what state is it in, what needs attention, what can I do next, and what related truth matters here?

## Structure
Use a strong `RecordHeader` with identity, human-readable reference, status/health where relevant, ownership/context, restrained badges, primary action and overflow actions.

Use compact tabs/sections for secondary views. Do not create a permanent second sidebar inside every record.

Overview should prioritize meaningful summary, Attention, next action, relationships, recent activity and upcoming commitments rather than duplicating every field.

## Rules
- preserve one canonical source record; related panels are projections/links, not copies;
- use Action Registry entries for reusable mutations;
- show source/freshness for synced or derived values when material;
- keep internal and client-visible information clearly separated;
- ordinary Files and protected Vault Items must not share an access path;
- comments/mentions/following use the shared collaboration primitive;
- Activity is business chronology; Audit remains evidentiary security history;
- plugins may use only declared record extension slots;
- never expose inaccessible related-record counts or summaries.

## States
Cover loading, skeleton, empty related sections, partial/degraded connector data, stale data, permission-limited data, read-only, archived, error, offline where safe, and record-not-found/revoked access.

## Responsive
Desktop may use dense summary columns and context rails. Tablet collapses secondary panels. Phone prioritizes identity, Attention, primary action, core summary, then section navigation; do not squeeze desktop tabs/tables.

## Completion
Verify the workspace remains understandable without module hopping, actions are permission checked, related data is not duplicated, client-safe projections remain safe, and the component composition is represented in the Component Gallery when reusable.