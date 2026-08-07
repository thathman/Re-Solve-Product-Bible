# Re:Solve Plugin Platform

## Purpose
Plugins extend Re:Solve with business/product capability that is not universally core, while preserving one coherent application and avoiding forks.

A Plugin adds capability. A Connector integrates an external system. A provider package may be distributed as a Plugin that registers one or more Connector implementations, but business domains still depend on provider-neutral Connector contracts.

## Goals
- extend capability without forking core;
- preserve coherent Admin/Portal UX;
- support compatibility, lifecycle, permissions, migrations, settings, health and Audit;
- expose controlled UI, data, Event, Action, Automation, Notification, Search, Report, API and MCP extension points;
- remain portable/self-hostable;
- integrate with Core UI Framework and simple navigation rather than creating a separate app shell.

## Non-goals
- arbitrary unrestricted code/database access;
- making every core feature a Plugin;
- allowing bypass of Principal/permission, Vault/File, Notification, Attention, Action Registry, Connector or Audit contracts;
- allowing each Plugin to add an Odoo-like mini app launcher/navigation system;
- promising a public marketplace in v1.

## Core remains core
Core includes Workspace/Operating Entity/identity/access, Organisations/Contacts, Properties, Projects, Requests, CRM, Services, Billing, Files, Vault, Knowledge, Attention, Notifications, Actions, Automations, Monitoring/Posture/Renewals, Settings, Audit, Search, API/MCP and extension infrastructure.

Plugins should not reimplement these foundations.

## Suitable examples
- OJS / advanced Journal Operations;
- Hosting Operations;
- SEO Toolkit;
- WooCommerce Operations;
- Advanced Accounting;
- Procurement/Vendor Operations;
- Asset Management;
- Advanced Reporting;
- specialized Import Packs;
- Airix Food operational domain;
- provider packages that register Connectors.

Explicitly out of scope as core Plugin targets unless a future deliberate product decision changes it: HR, payroll, Timesheets and Client Service Consumption.

## Manifest contract
Every Plugin declares at least:
- id/name/description/vendor/version/license;
- core compatibility;
- dependencies;
- requested canonical permissions;
- settings schema;
- migrations/data ownership;
- navigation/record/UI extension contributions;
- Action definitions;
- Event subscriptions/publications;
- Automation triggers/actions;
- scheduled jobs;
- Notification/Attention providers;
- Search/Report contributions;
- API/MCP contributions;
- Connector implementations/dependencies where applicable;
- health/diagnostics;
- update/rollback/uninstall policy.

Exact package format remains technical planning.

## Provider package pattern
Example:
```text
Billing Core
  -> PaymentConnector capability
      -> Bachs Provider Plugin registers BachsPaymentConnector
      -> Paystack Provider Plugin registers PaystackPaymentConnector
```

This pattern may also apply to optional specialist provider implementations for other Connector Types. Installing a provider package does not make the provider name part of core domain data.

## Lifecycle
States may include available, installed, config_required, enabled, disabled, update_available, upgrading, error, incompatible, rollback_available, uninstalling and removed.

Operations include install, inspect permissions, configure, enable/disable, update, rollback, repair, diagnostics and uninstall.

Uninstall policy explicitly states retain/archive/export/delete behavior for Plugin-owned data. Destructive removal requires confirmation and Audit.

## Admin UX
### Installed
Show identity/vendor/version, compatibility, health, requested/effective permissions, update state, migrations, Connector registrations/dependencies, last failure, configure/enable/disable/diagnostics.

### Available/Sources
Initially bundled first-party and configured private sources. Future registry/marketplace can reuse the same package contract.

### Update review
Show changelog, compatibility, migrations, newly requested permissions, new Actions/Connector capabilities and rollback before activation.

## UI extension contract
Plugins use named slots and `09-design/core-ui-framework.md`.

Possible slots:
- Organisation/Property/Project/Request record tabs/widgets/actions;
- Dashboard secondary modules/Attention provider;
- Reports datasets/views;
- Settings sections;
- Client Portal entries/widgets;
- Search/Command Actions;
- Quick Create only when genuinely frequent.

### Navigation governance
Default answer is **not** `add a root Sidebar item`.

A Plugin must first determine whether capability belongs as:
- a tab/view under an existing major area;
- a record extension;
- a Settings subsection;
- a Search/Command action;
- a secondary Operations destination.

Any root navigation contribution uses approved slots, simple human labels and mobile rules. Plugins cannot introduce app grids, nested module launchers or unrelated shell chrome.

## Core UI
Plugin UI must consume approved Re:Solve tokens/components/composites. If a reusable pattern is missing, contribute it to the Core Framework rather than shipping a visually unrelated component system.

## Permissions / Principal
Plugin is a Principal when acting. Requested canonical capabilities are reviewed on install/upgrade and checked at execution.

Examples:
- `organisations.read`
- `properties.read`
- `projects.read`
- `billing.read`
- `vault.metadata.read`
- `notifications.create`
- `actions.register`

Installation does not grant unrestricted data access.

## Data ownership / migrations
- Plugin data structures namespaced;
- cross-domain links use stable core ids;
- core schema mutation only through approved mechanisms;
- migrations versioned/recoverable;
- failed migration yields diagnosable error state;
- disable does not delete data;
- imported/synced data retains provenance where relevant.

## Events / Actions / Jobs
Plugins subscribe/publish through shared Event runtime.

Plugin writes/actions register through Action Registry with permission/risk/confirmation/approval semantics.

Jobs use central job runtime with trigger/schedule, concurrency, timeout, retry, idempotency and health—no unmanaged cron processes.

## Attention / Notifications
Plugins may register namespaced Attention providers and Notification events/templates/default policies. Delivery remains core Notification Platform responsibility.

## Search / Reports
Plugin Search/Report contributions declare fields, sensitivity, permission, source/freshness and Core UI renderer. No unrestricted SQL.

## API / MCP / Àríyá
Plugin API/MCP tools inherit core auth/scope/Audit and registered Actions. Àríyá can use plugin-provided tools/actions only through approved registries.

No unrestricted storage/database/provider credentials.

## Security
Minimum:
- declared permissions;
- namespaced routes/data;
- migration validation;
- secret access only through approved Vault/Connector interfaces;
- no secret logs;
- dependency/compatibility checks;
- enable/disable kill switch;
- append-only Audit for consequential lifecycle/permission actions.

Full sandboxing may be deferred, but unrestricted access must never become the normalized extension contract.

## Health / diagnostics
States: healthy, degraded, misconfigured, incompatible, migration_required, failed.

Health appears in Plugins/System Health and can produce Attention for persistent actionable failure.

## Responsive/PWA/accessibility
Plugin surfaces meet the same responsive/PWA/WCAG/Core UI requirements as core. Desktop-only limitation, when truly unavoidable, is explicit—not broken layout.

## Acceptance criteria
- lifecycle is controlled/recoverable;
- newly requested permissions/actions/connectors visible before activation;
- disabling removes contributions without corrupting core;
- provider Plugins register Connectors without leaking provider assumptions into domains;
- navigation remains simple;
- Core UI coherence is enforced;
- Plugin Attention/Notifications use core systems;
- API/MCP/Àríyá obey scope and Audit;
- no HR/Timesheet/service-consumption assumptions enter core through a Plugin.
