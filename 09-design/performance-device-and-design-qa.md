# Performance, Device and Design QA Standards

## Purpose
`Responsive`, `fast` and `polished` need measurable review expectations. Re:Solve should not accept technically functional slices that feel slow, break at common widths or drift visually.

## Device classes
Every major UI slice should be reviewed at representative widths including:
- compact phone around 360px
- common phone around 390–430px
- tablet portrait around 768px
- tablet/compact laptop around 1024px
- common laptop around 1366px
- desktop around 1440–1600px
- wide desktop around 1920px+

Exact CSS breakpoints remain implementation decisions. These are review scenarios, not a promise to hard-code these widths.

## Browser baseline
Target current stable evergreen browsers appropriate to the deployment, including Chromium-based browsers and Safari/WebKit where practical for Portal/PWA use. Browser-specific limitations must be documented rather than silently ignored.

## Interaction performance
Operational expectations:
- shell/navigation interactions should feel immediate;
- command palette should open instantly after local trigger;
- typing/filter controls should not visibly lag on ordinary datasets;
- long lists should use pagination/virtualization as needed;
- background refetch should not blank usable content;
- optimistic updates are used only when rollback/failure behavior is safe;
- expensive charts/editors/canvases should be lazy-loaded where appropriate.

FOUND-001 should establish measurement tooling available in the chosen Lovable stack rather than premature rigid production SLAs.

## Network/degraded behavior
Review:
- fast connection
- slow connection
- intermittent connection
- offline PWA shell
- stale cached state
- provider/connector unavailable

Do not display empty/zero data when the truth is `unable to load` or `stale`.

## Content stress tests
Components should be reviewed with:
- long organisation/property names
- long email addresses
- many nav entries within approved limits
- high notification counts
- empty avatar image
- large amounts/currencies
- multiple status labels
- long translated/localized text readiness
- dense tables

## Design QA gate
A slice is not complete after functional testing alone.

Required completion sequence where applicable:
1. functional acceptance
2. permission/security review
3. responsive/PWA review
4. accessibility review
5. Core UI consistency review
6. visual hierarchy/polish review
7. interaction/state review
8. performance/degraded-state review

## Core UI consistency review
Check:
- correct canonical component used
- spacing/radius/typography tokens
- no page-specific duplicate component
- shadcn/Untitled/Tremor influence normalized into Re:Solve language
- sidebar/topbar/avatar/notifications unaffected by feature drift
- plugin/connector contribution uses approved slots

## Visual regression
Use the Component Gallery and available screenshot/visual regression tooling where practical. Major shell/Core UI changes should be reviewed across representative variants.

## Acceptance criteria
- phone/tablet/laptop/desktop are intentionally composed
- shell does not visibly lag in normal use
- stale/error/offline are truthful states
- visual QA is a release gate
- Core UI drift is caught before feature completion
