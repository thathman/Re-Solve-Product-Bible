# Re:Solve Lovable Build Slice Protocol

## Purpose
The Product Bible may describe the entire operating system. Lovable must receive only the smallest coherent slice needed for the current build step.

This protocol prevents broad prompts, premature implementation, architectural drift, and half-finished feature breadth.

## Definition of a build slice
A build slice is the smallest independently reviewable unit that completes one meaningful user flow or one bounded platform capability.

A slice may include multiple files/components when required to complete that flow, but it must not become a disguised module rewrite.

## Slice rules
Every slice must have:
- one objective
- one primary actor or tightly related actor set
- one bounded route/surface or platform capability
- explicit in-scope work
- explicit out-of-scope work
- source Product Bible references
- data requirements
- permission requirements
- states
- acceptance criteria
- responsive/PWA expectations
- completion evidence

## Forbidden prompt style
Do not send prompts such as:
- "Build the CRM"
- "Build billing"
- "Implement the client portal"
- "Add the settings page"
- "Create the full dashboard and all modules"

These prompts are too broad.

## Preferred prompt style
Examples:
- Build the Admin application shell only.
- Build the Organisations list only, including filters, saved views, empty/loading/error states, and responsive behavior. Do not build Organisation 360 yet.
- Build Organisation 360 Overview tab only. Do not build Billing, Support, Vault, or plugin tabs yet; show future tabs as disabled only if the spec explicitly requires it.
- Build notification preference matrix only; do not implement email/WhatsApp delivery yet.

## Standard slice template

### Slice ID
Use a stable identifier, e.g. `FOUND-001`, `ORG-002`, `PROP-004`.

### Objective
One sentence describing what becomes usable after the slice.

### Product Bible sources
List exact spec files/sections Lovable should follow.

### Actor and goal
Use Flow-by-Flow framing:
`<actor> can <measurable goal> without <current friction>`.

### In scope
Exact functionality to implement.

### Out of scope
Explicit adjacent features not to implement.

### Existing foundation to reuse
List existing components, patterns, schemas, services, routes, and skills to reuse.

### Data requirements
Specify realistic demo data needed for this slice only.

### Permissions
List capabilities and denial cases.

### States
At minimum consider:
- default
- loading
- skeleton
- empty
- first-use
- success
- error
- partial data
- permission denied
- read-only/disabled
- mobile
- offline/online-only where relevant

### Responsive/PWA
Define phone/tablet/desktop behavior and safe offline assumptions.

### Accessibility
Define keyboard/focus/semantic/touch requirements.

### API/service boundaries
State whether this slice creates or uses data/service/API abstractions.

### Notifications/automation
Only include if the slice creates or consumes them.

### Plugin/connector extension points
Only include where required by the source spec.

### Acceptance criteria
Observable outcomes.

### Verification
Specify what Lovable should inspect/test before reporting completion.

### Completion report
Lovable must return:
- what was built
- files/surfaces materially changed
- data/schema changes
- tests/checks performed
- known limitations
- out-of-scope items deliberately left untouched
- any conflict found with Product Bible

## Slice sizing guidance
A slice is probably too large if it:
- creates more than one major record workspace
- implements both list and full multi-tab record detail with several domains
- introduces multiple unrelated data models
- implements more than one external connector
- combines architecture foundation and a business module
- requires a long prompt containing many future features

A slice may be too small if it:
- produces no traversable user outcome
- creates only decorative components without a real flow
- splits tightly coupled behavior so the intermediate build is broken

## Build sequence policy
Prefer vertical progress:
1. shared foundation
2. one visible flow
3. complete states
4. review
5. next adjacent flow

Do not horizontally scaffold dozens of empty pages before proving the shell and one or two core workflows.

## Review gate
No next slice until the current slice is reviewed against:
- Product Bible
- design system
- permission model
- state completeness
- responsive/PWA behavior
- accessibility
- portability

## Spec drift
If implementation reveals a genuine product ambiguity:
- do not silently decide in code
- record the ambiguity
- update Product Bible if needed
- then continue

## Prototype gate
Use the Flow Prototype skill before implementation when a slice includes a novel or high-impact interaction such as:
- complex dashboard composition
- advanced table interactions
- multi-step onboarding
- approval workflows
- Vault reveal/share flows
- plugin installation
- automation builder
- connector setup
- mobile navigation changes

## Build-slice numbering
Suggested prefixes:
- `FOUND` foundation
- `AUTH` identity/access
- `NAV` shell/navigation
- `DASH` dashboard
- `ORG` organisations
- `CONTACT` contacts
- `PROP` properties
- `PROJ` projects
- `SALE` sales
- `BILL` billing
- `SUP` support
- `VAULT` secure vault
- `FILE` files
- `KB` knowledge
- `NOTIF` notifications
- `AUTO` automations
- `PLUGIN` plugins
- `CONN` connectors
- `API` API/webhooks
- `MCP` MCP
- `AI` Re:Solve AI
- `PORTAL` client portal
- `SYS` system operations
