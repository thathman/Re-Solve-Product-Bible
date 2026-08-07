# Re:Solve Lovable Skills

## Purpose
Re:Solve uses source-controlled Lovable workspace skills so recurring engineering, design, security, platform and review work is handled consistently. Skill naming belongs to the reusable Re:Solve product, not the Airix Media deployment.

All former `airix-*` skill names are deprecated. Canonical custom skill namespace is `resolve-*`, with `self-host-check` retained as a generic portability review.

## Lovable behavior
Lovable workspace skills are loaded on demand when their descriptions match or can be invoked directly with `/skill-name`. Descriptions therefore start with `Use when...` and are intentionally narrow enough to avoid accidental triggering.

The Product Bible owns the canonical skill contents. Lovable must import them without rewriting or summarizing them.

## Skill authoring rules
Every skill must:
- use lowercase/hyphenated permanent names;
- have a clear `Use when...` trigger description;
- read applicable Product Bible sources first;
- produce bounded work/output;
- preserve the Core UI Framework and canonical terminology;
- include completion checks;
- avoid silently implementing unrelated future work;
- enforce explicit exclusions: no HR, payroll, recruitment, leave/attendance, performance management, timesheets/time tracking, or Client Service Consumption.

## Complete initial catalogue

### Build and UI
- `/resolve-feature` — bounded feature-slice implementation and scope discipline.
- `/resolve-ui` — Core UI Framework implementation/refinement.
- `/resolve-shell` — Sidebar, TopBar, Avatar/Account, Notifications, Search/Command, Quick Create, Àríyá and global chrome.
- `/resolve-navigation` — simple route/navigation hierarchy and mobile navigation governance.
- `/resolve-form` — forms, validation, sensitive fields and error/focus behavior.
- `/resolve-data-table` — operational lists, filters, saved views, bulk actions and mobile alternatives.
- `/resolve-record-workspace` — first-class 360/detail record workspaces.
- `/resolve-dashboard` — Attention-led dashboards/overview surfaces and meaningful Tremor-style analytics.
- `/resolve-responsive` — phone/tablet/laptop/desktop recomposition.
- `/resolve-portal` — client-safe Portal projections and client-first UX.

### Design and quality
- `/resolve-accessibility` — WCAG 2.2 AA and interaction accessibility review.
- `/resolve-design-review` — visual hierarchy, Core UI consistency, library influence and non-generic design review.
- `/resolve-security-review` — authorization, sensitive data, Vault, financial and integration security review.
- `/resolve-pwa` — installability, service worker, offline/cache, push and PWA-specific behavior.
- `/resolve-debug` — root-cause debugging and regression verification.
- `/resolve-release` — final slice go/no-go review.
- `/self-host-check` — architecture portability/self-hostability review.

### Platform primitives
- `/resolve-notifications` — notification events, recipient/channel/delivery behavior and notification UI contracts.
- `/resolve-attention` — current unresolved Attention Item creation, dedupe, resolve and presentation.
- `/resolve-action-registry` — reusable business Action contracts and risk/permission behavior.
- `/resolve-settings` — configuration ownership, scopes, defaults, forms, diagnostics and audit.
- `/resolve-data-migration` — imports, exports, legacy migration, dedupe/merge/reassignment and schema/data migrations.

### Extensions and machine interfaces
- `/resolve-plugin` — plugin manifest/lifecycle/data/UI/events/jobs/API/MCP.
- `/resolve-connector` — external integration instances, mapping, sync authority, health and event reliability.
- `/resolve-automation` — triggers/conditions/actions/approvals/runs/retries.
- `/resolve-api` — REST/API resources/actions, scopes, OpenAPI and webhooks.
- `/resolve-mcp` — curated MCP tools/resources, risk, redaction and audit.

### High-value specialist domains
- `/resolve-monitoring` — native Monitoring, Workers/Probes, Property Posture, Incidents and Renewal signals.
- `/resolve-document` — Document Studio, proposals, estimates, contracts, generated financial documents and immutable Final Snapshots.
- `/resolve-ai` — Àríyá provider/tools/actions/experience and Chatwoot Captain separation.
- `/resolve-vault` — Secure Vault reveal/download/share/request/rotation and protected-content boundaries.

## Skills required before FOUND-001
Import and enable at minimum:
1. resolve-feature
2. resolve-ui
3. resolve-shell
4. resolve-navigation
5. resolve-responsive
6. resolve-accessibility
7. resolve-design-review
8. resolve-security-review
9. resolve-pwa
10. resolve-release
11. self-host-check

The remaining skills should also be imported before broad feature development so the workspace is ready for later slices. They do not increase prompt context unless Lovable selects them for a matching task.

## Recommended FOUND-001 invocation
The foundation prompt should explicitly invoke:
`/resolve-feature /resolve-shell /resolve-ui /resolve-navigation /resolve-responsive /resolve-pwa /resolve-accessibility /self-host-check /resolve-release`

Use `/resolve-design-review` after the first visual implementation pass or as part of the final foundation review.

## Sequencing examples

### Record page
`resolve-feature → resolve-record-workspace → resolve-data-table/form as needed → resolve-responsive → resolve-security-review → resolve-accessibility → resolve-design-review → resolve-release`

### Connector
`resolve-feature → resolve-connector → resolve-action-registry when writes exist → resolve-security-review → self-host-check → resolve-release`

### Portal flow
`resolve-feature → resolve-portal → resolve-ui → resolve-responsive → resolve-pwa → resolve-accessibility → resolve-security-review → resolve-release`

### Shell/Core UI
`resolve-feature → resolve-shell → resolve-navigation → resolve-ui → resolve-responsive → resolve-pwa → resolve-accessibility → resolve-design-review → self-host-check → resolve-release`

### Monitoring
`resolve-feature → resolve-monitoring → resolve-attention → resolve-notifications → resolve-security-review → resolve-release`

### Document workflow
`resolve-feature → resolve-document → resolve-form/record-workspace as needed → resolve-action-registry → resolve-security-review → resolve-accessibility → resolve-release`

## Built-in Lovable skills
Use Lovable's maintained accessibility/redesign/other built-in skills when they add value, but Re:Solve custom skills and Product Bible rules remain authoritative for Re:Solve-specific behavior.

## Governance
When a recurring pattern repeatedly needs ad-hoc instructions, consider a new skill. Do not create overlapping skills merely to encode one page's details. Update source-controlled `SKILL.md` first, then refresh the Lovable workspace version.