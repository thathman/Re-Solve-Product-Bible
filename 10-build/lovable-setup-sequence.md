# Re:Solve Lovable Setup Sequence

## Purpose
This sequence prepares Lovable for Re:Solve without asking it to build the operating system all at once.

## Step 1 — Connect source control
Connect Lovable to the Re:Solve application repository.

Rules:
- GitHub remains the source-controlled record of exported application code.
- Do not rewrite the full product immediately.
- Inspect the existing Re-Solve repository as behavior/reference material.
- Prefer Lovable-compatible architecture for new work.

## Step 2 — Add persistent Knowledge
Add the contents/rules from `10-build/lovable-knowledge.md` to Lovable Workspace/Project Knowledge in a concise persistent form.

Knowledge should include only durable rules, not every feature specification.

## Step 3 — Establish design foundation
Before business pages:
- initialize the preferred Lovable React application structure
- establish Tailwind/design tokens
- establish shadcn/ui or equivalent accessible primitive layer
- define typography, spacing, radii, shadows, surfaces, status colors, focus states, and responsive breakpoints
- install specialist libraries only when justified by an actual slice

Do not install a large dependency catalogue preemptively.

## Step 4 — Create initial custom skills
Create first:
1. airix-feature
2. airix-ui
3. airix-form
4. airix-data-table
5. airix-security-review
6. airix-pwa
7. airix-release
8. self-host-check

Use Lovable's skill-creation capability where available.
Descriptions must be specific enough for reliable auto-selection.

## Step 5 — Connect Supabase
Use Supabase for development data/auth/storage where useful.

Initial expectations:
- canonical user/profile/membership foundation
- clean migrations/schema history
- realistic demo data
- safe storage buckets/policies
- explicit permission model

Do not create the full future schema in one pass.
Only create data models required by the current slice plus truly foundational identity/platform tables.

## Step 6 — Establish application shells
Create only the shared app foundation:
- global providers
- Admin shell route/layout
- Client Portal shell route/layout
- authenticated route gates
- role/membership resolution
- design-system primitives
- error boundary
- loading patterns
- global responsive behavior
- PWA base

Do not build business modules yet.

## Step 7 — PWA base
From the start establish:
- web app manifest
- installability
- app icons/placeholders
- service-worker strategy
- update lifecycle placeholder
- safe offline shell
- push-ready architecture
- no Vault/secret caching

Full push delivery can wait for Notifications slices.

## Step 8 — Developer quality baseline
Configure the quality tools that fit the generated stack:
- strict TypeScript
- linting/formatting
- unit/component tests
- Playwright or equivalent flow tests
- accessibility checks where practical

Avoid test-suite ceremony without behavior coverage.

## Step 9 — First demo universe
Seed only the subset needed to render the shell and identity states:
- Airix Media internal organisation
- a few staff identities/roles
- Kampala University client organisation
- a few client users and memberships

Do not seed every project/invoice/property until those slices arrive.

## Step 10 — Review foundation
Before building the first business list:
- inspect generated architecture
- inspect routing
- inspect auth
- inspect responsive behavior
- inspect component consistency
- inspect dependency choices
- run `/self-host-check`
- verify no future modules were prematurely implemented

## Step 11 — Begin bounded slices
Recommended sequence after the foundation:
1. `FOUND-001` application/design foundation
2. `FOUND-002` identity, memberships, permission gates
3. `NAV-001` Admin shell navigation
4. `PORTAL-001` Client Portal shell navigation
5. `DASH-001` Admin Dashboard structural prototype
6. `ORG-001` Organisations list
7. `ORG-002` Organisation 360 Overview
8. `CONTACT-001` Contacts list
9. `PROP-001` Properties list/tree
10. `PROP-002` Property 360 Overview

Later slices proceed from the Product Bible rather than from this list alone.

## Rule for every setup/build conversation
Lovable should be told:
- the exact current slice
- exact Product Bible references
- what must not be built
- what existing patterns to reuse
- acceptance criteria

Do not paste the entire Product Bible into a build prompt.
