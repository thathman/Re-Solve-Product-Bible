---
name: resolve-plugin
description: Use when designing, implementing, reviewing, installing, upgrading, disabling, or uninstalling a Re:Solve plugin that adds business capability inside the product.
---

# Re:Solve Plugin

Read `05-extensions/plugins.md`, Action Registry, Automations, API/MCP, Core UI Framework, security and the plugin's domain spec.

## Boundary
Plugin = product/business capability extension.
Connector = integration with an external system.
A plugin may register connector implementations but the concepts remain distinct.

## Manifest
Define stable id, name, version, vendor, compatible core range, dependencies, requested capabilities, settings schema, UI extension slots/navigation contribution, data/migrations, events, jobs, actions, notifications, API resources, MCP tools, health and uninstall policy.

## Permissions
Request the narrowest capabilities required. Installation/update UI must surface permission additions. Installed does not mean omnipotent.

## Data
Use namespaced plugin-owned tables/collections and versioned migrations. Cross-domain links use stable core ids. Disabling must not delete data. Uninstall must explicitly preserve/archive/export/delete plugin data according to policy.

## UI
Consume Re:Solve Core UI components/tokens and named extension slots. Do not introduce a second design system or uncontrolled root navigation.

## Runtime
Register events/jobs/notifications/actions through central platform registries. Do not create hidden cron/background mechanisms or private notification transports.

## API/MCP
Plugin contributions inherit core auth, scopes, rate limits, audit, risk classification and documentation conventions.

## Health/lifecycle
Cover available, installed, enabled, disabled, updating, incompatible, degraded/error, rollback and removed states. Expose recoverable diagnostics without secrets.

## Security
No raw Vault/provider credential access outside approved interfaces. Validate migrations, redact logs, audit lifecycle/config changes and support a kill switch.

## Completion
Verify compatibility failure is safe, permission changes are visible, disable removes active contributions cleanly, data remains recoverable, UI remains coherent, and uninstall consequences are explicit.