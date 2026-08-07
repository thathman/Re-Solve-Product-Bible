# Re:Solve Plugin Platform

## Purpose

Plugins extend Re:Solve with business capabilities that are not universally required by core. The plugin platform must allow Re:Solve to remain opinionated and coherent while supporting first-party, private, client-specific, and future third-party extensions.

A plugin adds product behavior. A connector integrates an external system. A plugin may depend on one or more connectors, but the two concepts must remain distinct.

## Core goals

- extend business capability without forking core
- preserve one coherent Admin and Client Portal experience
- support lifecycle management, compatibility checks, permissions, migrations, health, and audit
- expose stable extension points for UI, data, workflows, notifications, API, MCP, search, reports, and automation
- keep plugins portable with the final self-hosted application
- allow plugins to be authored incrementally in Lovable without coupling them to Lovable runtime services

## Non-goals

- arbitrary unrestricted code execution without platform contracts
- letting every feature become a plugin
- allowing plugins to bypass core permission, audit, notification, Vault, or connector policies
- promising a public marketplace in v1

## What remains core

Core owns identity, users, organisations, contacts, memberships, permissions, properties, projects, files, notifications, audit, settings, events, automation primitives, plugin management, connector management, API foundations, and MCP foundations.

Core business domains may also include CRM, billing, and knowledge where they are required across the operating model.

## Suitable plugin examples

- OJS Publishing
- Journal Operations
- Hosting Operations
- SEO Toolkit
- WooCommerce Operations
- Advanced Accounting
- Asset Management
- Advanced Reporting
- Data Import Packs

## Plugin package contract

Every plugin declares a manifest with at least:

- id
- name
- description
- version
- vendor
- core compatibility range
- dependencies
- requested permissions
- navigation contributions
- UI extension points
- API contributions
- MCP contributions
- event subscriptions
- automation triggers/actions
- scheduled jobs
- migrations
- settings schema
- health checks
- uninstall policy

Conceptual manifest:

```json
{
  "id": "resolve-ojs",
  "name": "Re:Solve OJS",
  "version": "1.0.0",
  "requiresCore": ">=1.0.0",
  "permissions": ["properties.read", "ojs.read", "ojs.manage"],
  "navigation": ["journals"],
  "migrations": true,
  "serverEntry": "./server/index",
  "uiEntry": "./ui/index"
}
```

Exact implementation format is not locked by this product spec; capability semantics are.

## Lifecycle

Supported lifecycle states:

- available
- installed
- enabled
- disabled
- update available
- upgrading
- error
- incompatible
- rollback available
- uninstalling
- removed

Supported operations:

- install
- inspect requested permissions
- configure
- enable
- disable
- update
- rollback
- repair
- export diagnostic bundle
- uninstall

Uninstall must declare whether plugin-owned records are retained, archived, exported, or deleted. Destructive removal requires explicit confirmation and audit.

## Admin experience

### Installed

Show:
- plugin name and icon
- vendor
- version
- status
- core compatibility
- health
- permissions summary
- update state
- last migration
- last error
- configure action
- enable/disable action
- diagnostics

### Available

Initially this can represent bundled first-party packages and explicitly configured private sources. Future registry/marketplace support must not require a redesign of the package model.

### Updates

Show changelog, compatibility, required migrations, permission changes, and rollback availability before upgrade.

### Development

For trusted development environments, allow local/private plugin packages to be registered for testing. Production policy may disable development-source installation.

## UI extension points

Core pages expose named slots rather than inviting plugin forks.

Examples:

### Organisation 360
- overview widgets
- secondary tabs
- contextual actions

### Property 360
- summary widgets
- tabs
- status indicators
- actions

### Project 360
- tabs
- widgets
- actions
- reports

### Dashboard
- optional widgets
- attention providers

### Client Portal
- navigation entries where permitted
- property/project tabs
- portal widgets

Plugins must use approved Re:Solve design primitives and responsive contracts.

## Permissions

Plugins request explicit platform permissions such as:

- organisations.read
- contacts.read
- properties.read
- properties.manage
- projects.read
- billing.read
- notifications.create
- vault.metadata.read
- api.tools.register

Install/upgrade UI must show requested capabilities and highlight newly added permissions.

A plugin must not gain unrestricted access merely because it is installed.

## Data ownership

Plugins may define namespaced data structures and declared migrations.

Rules:
- plugin tables/collections must be namespaced
- core schema mutation must occur only through approved extension mechanisms
- cross-domain links use stable core identifiers
- plugin migrations are versioned
- failed migrations place the plugin into a recoverable error state
- disabling a plugin does not silently delete data

## Events and hooks

Plugins subscribe to the shared event bus rather than patching core modules.

Examples:
- organisation.created
- property.created
- property.updated
- project.created
- project.completed
- invoice.created
- invoice.paid
- approval.requested
- approval.completed
- credential.revealed
- connector.health_changed

Plugins may also publish namespaced events.

## Jobs

Plugins register jobs with the central job runtime. They must not create unmanaged cron processes.

Jobs declare:
- schedule/event trigger
- concurrency
- timeout
- retry policy
- idempotency behavior
- health/metrics

## Notifications

Plugins may register notification event types, templates, default delivery policies, and preference controls. All actual delivery goes through the core Notification Platform.

## API and MCP

Plugins may register API resources/actions and MCP tools through core registries.

Rules:
- inherit core authentication and permission systems
- declare scopes
- use platform audit
- never expose unrestricted storage/database access
- dangerous actions may require confirmation or approval

## Security

Minimum controls:
- declared permissions
- namespaced routes and data
- migration validation
- secret access only through approved Vault/connector interfaces
- no raw secret display in logs
- dependency and compatibility checks
- enable/disable kill switch
- audit trail

Full sandboxing is not required for v1, but the architecture must not normalize unrestricted access.

## Health

Each plugin can report:
- healthy
- degraded
- misconfigured
- incompatible
- migration required
- failed

Health detail belongs in Plugins, System Health, and diagnostics.

## Notifications and audit events

Audit:
- installed
- enabled
- disabled
- configured
- upgraded
- rollback
- permission changed
- migration run
- uninstall requested/completed

Important failure states may create notifications for administrators.

## PWA/mobile

Plugin UI must support the same responsive and accessibility standards as core. Unsupported desktop-only plugin functionality must present an explicit mobile limitation rather than broken layout.

## Acceptance criteria

- plugin can be installed, configured, enabled, disabled, updated, rolled back, and removed through declared lifecycle
- newly requested permissions are visible before activation
- disabling plugin removes its UI/actions without corrupting core records
- plugin data remains namespaced and recoverable
- plugin failures are visible in health and logs
- plugin notifications use core notification delivery
- plugin APIs/MCP tools obey platform permissions and audit
- portal contributions remain permission- and organisation-scoped

## Lovable build slices

1. Plugin registry records + Installed list UI
2. Plugin detail/configuration/health UI
3. lifecycle enable/disable and compatibility model
4. named UI extension-slot registry
5. event/job/notification contribution contracts
6. migration/update/rollback model
7. private-source/development installation support
