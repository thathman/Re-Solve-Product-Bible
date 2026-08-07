# Re:Solve Lovable Skills

## Purpose
Re:Solve uses reusable Lovable skills so recurring engineering/design work is handled consistently. Skill naming belongs to the reusable Re:Solve product, not the Airix Media deployment.

All former `airix-*` skill names are deprecated. Canonical custom skill namespace is `resolve-*`, with `self-host-check` retained as a generic portability skill.

## Skill authoring rules
Each skill should:
- have a narrow trigger;
- read the applicable Product Bible source first;
- produce bounded output;
- use the Core UI Framework;
- include completion checks;
- avoid silently implementing unrelated future work;
- enforce explicit exclusions including no HR, timesheets or Client Service Consumption.

## Required skills

### `/resolve-feature`
Implement one bounded feature slice. Identify actors, permissions, states, flows, data/provenance, UI components, responsive/PWA behavior, acceptance criteria and out-of-scope work.

### `/resolve-ui`
Create/refine Re:Solve interfaces using `09-design/core-ui-framework.md`, `design-direction.md` and navigation rules. shadcn, Untitled UI and Tremor are mandatory major sources/influences.

### `/resolve-form`
Create forms with schema validation, help/defaults, sensitive handling, async/server errors, unsaved-change behavior, responsive layout and accessible focus/error states.

### `/resolve-data-table`
Create operational lists using the canonical Re:Solve DataTable/TanStack-style contract: search/filter/sort, saved views, bulk actions, permission-sensitive columns/actions, full states and mobile alternate presentation.

### `/resolve-record-workspace`
Build first-class record workspaces with RecordHeader, status, actions, tabs, related records, collaboration/activity, Attention, Files/Vault boundaries and extension slots.

### `/resolve-dashboard`
Build summary surfaces from Attention/decisions/actions rather than generic card grids. Use Tremor-style data presentation only where it answers real operational questions.

### `/resolve-notifications`
Define events, recipients, priority, channels, grouping/dedupe, deep links, delivery state, escalation and PWA behavior. Distinguish Notification from Attention.

### `/resolve-security-review`
Review authorization, cross-scope isolation, sensitive data, Audit, step-up, Action Registry risk, connector/plugin boundaries and offline cache.

### `/resolve-plugin`
Design/implement a plugin manifest, compatibility, permissions, migrations, settings, routes/extension slots, events/jobs, notifications, actions, API/MCP and lifecycle.

### `/resolve-connector`
Design/implement connector contracts, instances, credentials references, mappings, provenance/sync direction, health, events, retries, rate limits and security.

### `/resolve-automation`
Design/implement trigger, conditions, actions, branches, delays, approval gates, run history, retry/idempotency and shared Action Registry use.

### `/resolve-api`
Versioned resources/actions, scopes, record authorization, idempotency, errors, audit, rate limits, OpenAPI and webhook implications.

### `/resolve-mcp`
MCP tools/resources with scope, read/write risk, permission inheritance, field redaction, confirmation, audit and no arbitrary SQL/unrestricted Vault access.

### `/resolve-pwa`
Installability, responsive behavior, cache data class, online-only sensitive operations, push/deep links, service-worker lifecycle, offline fallback and safe areas.

### `/resolve-accessibility`
WCAG 2.2 AA review for semantics, keyboard/focus, screen readers, contrast, reduced motion, touch targets, forms, tables and overlays.

### `/resolve-debug`
Reproduce complete affected flow, locate failure boundary, fix root cause, add regression coverage and verify adjacent states.

### `/resolve-release`
Run acceptance, type/lint/test/build where available, security, responsive/PWA, accessibility, Core UI/design QA, known limitation, migration/data and Product Bible drift review.

### `/resolve-monitoring`
Use when building native monitors, Monitoring Workers, Property Posture, Renewal/Expiry signals, Incidents or monitoring connectors. Preserve source/freshness and distinguish provider outage from target outage.

### `/resolve-document`
Use for Document Studio, Proposal, Estimate, Contract and generated documents. Preserve business record truth, template/version lifecycle, Secure External Access and immutable accepted/executed snapshots.

### `/resolve-ai`
Use for Àríyá surfaces/provider/tools/actions. Preserve user-facing Àríyá identity, caller permissions, evidence/freshness, Action Registry use and Chatwoot Captain separation.

### `/resolve-shell`
Use for Sidebar, TopBar, avatar/account, notifications chrome, Search/Command, Quick Create, Àríyá entry and mobile navigation. Enforce simple Perfex/Brevo-like navigation clarity and reject Odoo/Twenty-style navigation complexity.

### `/self-host-check`
Review Lovable-only runtime assumptions, provider lock-in, direct Supabase coupling, environment configuration and self-host portability without forcing premature production infrastructure.

## Built-in Lovable skills
Use Lovable's strongest available design/review/accessibility/skill-creation capabilities in addition to these custom rules. Custom skills complement rather than duplicate useful built-ins.

## Skill sequencing examples

### Admin record page
1. `/resolve-feature`
2. `/resolve-record-workspace`
3. `/resolve-data-table` when needed
4. `/resolve-security-review`
5. `/resolve-accessibility`
6. `/resolve-release`

### New connector
1. `/resolve-feature`
2. `/resolve-connector`
3. `/resolve-security-review`
4. `/self-host-check`
5. `/resolve-release`

### Portal mobile flow
1. `/resolve-feature`
2. `/resolve-ui`
3. `/resolve-pwa`
4. `/resolve-accessibility`
5. `/resolve-release`

### Shell/Core UI
1. `/resolve-shell`
2. `/resolve-ui`
3. `/resolve-pwa`
4. `/resolve-accessibility`
5. `/self-host-check`
6. `/resolve-release`

## Skill creation order
Create first:
1. resolve-feature
2. resolve-ui
3. resolve-shell
4. resolve-form
5. resolve-data-table
6. resolve-security-review
7. resolve-pwa
8. resolve-release
9. self-host-check

Add domain-specific skills when their first relevant build slice approaches.
