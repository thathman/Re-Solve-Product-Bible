# Re:Solve Lovable Skills

## Purpose
Re:Solve should use reusable Lovable skills so recurring engineering and design tasks are handled consistently rather than re-explained in every prompt.

The skill set should be small enough to remain discoverable, but specific enough that Lovable can auto-select the right skill from its description.

## Skill authoring rules
Each skill should:
- have a narrow trigger description
- state what context to read first
- reference Product Bible rules rather than duplicating them excessively
- produce bounded output
- include completion checks
- avoid silently implementing unrelated future work

## Required skills

### `/airix-feature`
Use when implementing one bounded Re:Solve feature slice from the Product Bible.

Responsibilities:
- read the applicable spec
- restate in-scope and out-of-scope work
- identify affected flows
- identify permissions and states
- implement only the requested slice
- use existing design-system primitives
- include realistic demo data if needed
- verify responsive/mobile behavior
- verify loading/empty/error/permission states
- verify API/service boundaries
- report what was intentionally not built

### `/airix-ui`
Use when creating or refining Re:Solve pages, record workspaces, navigation, panels, dashboards, or portal experiences.

Responsibilities:
- follow the design direction and design system
- avoid generic admin templates
- preserve hierarchy and operational density
- use shadcn/Radix primitives by default
- choose stronger specialist components only when they materially improve UX
- verify desktop/tablet/mobile composition
- verify keyboard and touch behavior
- verify accessibility and reduced motion

### `/airix-form`
Use for create/edit/configuration forms.

Responsibilities:
- derive fields from the spec
- define labels/help text/defaults
- validation
- async validation where needed
- sensitive-field treatment
- unsaved changes
- error summaries
- success feedback
- mobile layout
- keyboard/focus order
- destructive action separation

### `/airix-data-table`
Use for operational lists and data-heavy views.

Responsibilities:
- columns
- sorting
- filtering
- search
- pagination/virtualisation where appropriate
- saved views
- bulk actions
- row actions
- selection behavior
- permission-sensitive columns/actions
- empty/loading/error states
- mobile alternate presentation
- accessibility

### `/airix-record-workspace`
Use for Organisation 360, Contact 360, Property 360, Project 360, invoice workspaces, and other first-class record pages.

Responsibilities:
- record header
- summary/status
- contextual actions
- tabs/sections
- related records
- timeline/activity
- files
- notifications
- extension slots
- mobile adaptation
- permission-aware visibility

### `/airix-dashboard`
Use for Admin Dashboard, Portal Home, reporting overviews, and other summary surfaces.

Responsibilities:
- begin from decisions/actions, not cards
- distinguish attention from information
- define source and freshness for every metric
- avoid redundant charts
- support personalization only where useful
- maintain strong small-screen hierarchy

### `/airix-notifications`
Use whenever a feature creates, changes, consumes, or configures notifications.

Responsibilities:
- event taxonomy
- recipients
- priority
- channels
- mandatory/configurable policy
- grouping/deduplication
- deep link
- delivery state
- escalation
- digest behavior
- push/PWA behavior

### `/airix-security-review`
Use before completing auth, permission, Vault, API, MCP, plugin, connector, financial, or destructive-action work.

Responsibilities:
- authorization paths
- cross-organisation isolation
- cross-property isolation
- sensitive field exposure
- audit events
- secrets handling
- rate limits
- replay/idempotency concerns
- step-up requirements
- unsafe client-side trust
- offline cache concerns

### `/airix-plugin`
Use when designing or implementing a Re:Solve plugin.

Responsibilities:
- manifest
- compatibility
- permissions
- settings
- migrations
- routes
- UI extension slots
- events
- jobs
- notifications
- API/MCP contributions
- health
- install/update/rollback/uninstall behavior

### `/airix-connector`
Use when creating or modifying an external-system connector.

Responsibilities:
- connector contract
- instance model
- authentication reference
- mappings
- health checks
- rate limits
- webhooks
- idempotency
- retries
- dead-letter handling
- logs
- capability exposure
- security boundaries

### `/airix-automation`
Use when designing or implementing workflow automation.

Responsibilities:
- trigger
- conditions
- actions
- branches
- delays
- approval gates
- retry/failure behavior
- run history
- idempotency
- permissions
- connector/plugin actions

### `/airix-api`
Use for public/internal API work.

Responsibilities:
- versioned resource/action design
- auth/scopes
- permission parity with UI
- pagination/filtering/sorting
- idempotency
- errors
- audit
- rate limits
- OpenAPI coverage
- webhook implications

### `/airix-mcp`
Use for MCP server, tools, resources, prompts, or AI-client integrations.

Responsibilities:
- tool/resource definition
- read/write risk class
- scope
- caller permission inheritance
- field redaction
- confirmation requirements
- audit
- rate limits
- no arbitrary SQL
- no unrestricted Vault access

### `/airix-pwa`
Use when a slice affects installability, mobile behavior, offline behavior, push, caching, or service-worker lifecycle.

Responsibilities:
- installability
- responsive layout
- safe caching class
- online-only operations
- push/deep-link behavior
- update lifecycle
- offline fallback
- safe-area/touch behavior
- secret-cache prohibition

### `/airix-accessibility`
Use for accessibility reviews or before completing major UI slices.

Responsibilities:
- semantic structure
- labels
- focus order
- keyboard access
- screen-reader states
- contrast
- reduced motion
- error announcements
- touch targets
- tables and dialogs

### `/airix-debug`
Use for regressions and broken flows.

Responsibilities:
- reproduce the complete affected flow
- locate boundary of failure
- inspect recent changes
- fix root cause rather than cosmetic symptom
- add regression coverage
- verify adjacent states

### `/airix-release`
Use before declaring a build slice complete.

Responsibilities:
- acceptance criteria check
- type/lint/test/build checks where available
- permission/security checks
- responsive/PWA check
- known limitations
- migration/data impact
- documentation/spec drift

### `/self-host-check`
Use when architecture or dependencies may threaten portability.

Responsibilities:
- identify Lovable-only runtime assumptions
- identify provider lock-in
- identify Cloudflare-specific APIs if any
- identify direct Supabase coupling that should be abstracted
- ensure environment-driven configuration
- ensure generated app remains exportable/self-hostable
- do not force premature production infrastructure work

## Built-in Lovable skills to use
Where available, Re:Solve should make active use of Lovable's own design and review capabilities, including equivalents of:
- skill creator
- redesign/design critique
- accessibility review
- SEO review where public surfaces need it

Custom skills should complement rather than duplicate built-in capabilities.

## Skill sequencing examples

### New Admin record page
1. `/airix-feature`
2. `/airix-record-workspace`
3. `/airix-data-table` if list view is part of slice
4. `/airix-security-review`
5. `/airix-accessibility`
6. `/airix-release`

### New connector
1. `/airix-feature`
2. `/airix-connector`
3. `/airix-security-review`
4. `/self-host-check`
5. `/airix-release`

### Portal mobile flow
1. `/airix-feature`
2. `/airix-ui`
3. `/airix-pwa`
4. `/airix-accessibility`
5. `/airix-release`

## Skill creation order
Create these first:
1. airix-feature
2. airix-ui
3. airix-form
4. airix-data-table
5. airix-security-review
6. airix-pwa
7. airix-release
8. self-host-check

Then add domain-specific skills as their first relevant build slice approaches.
