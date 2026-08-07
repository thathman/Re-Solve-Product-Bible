# Platform — PWA & Responsive Experience

## Purpose
Make Re:Solve installable, responsive and operationally useful across desktop, tablet and phone from the beginning rather than retrofitting mobile behavior after desktop implementation.

## Principles
- responsive behavior is specified per surface
- Portal must be exceptionally strong on mobile
- Admin must remain genuinely usable on phone for common operational tasks
- desktop may remain preferred for high-density configuration/report building
- offline behavior must be explicit; never imply freshness that is not known
- sensitive data has stricter cache rules than normal content

## Installability
Provide a standards-compliant web app manifest, app icons, theme/background metadata, standalone display behavior and install guidance where supported. Installation is optional; the browser experience remains complete.

## Navigation
### Client Portal mobile
Prefer a compact mobile navigation pattern such as bottom navigation for highest-frequency areas plus a More menu for secondary areas. Critical actions and notifications remain reachable with one hand.

### Admin mobile
Use a responsive drawer/sheet navigation, global search/command entry and compact context header. Do not attempt to display the full desktop sidebar permanently.

## Responsive data patterns
- tables become prioritized columns, horizontal scroll only where unavoidable, or card/list views
- dense record workspaces collapse side panels into drawers/accordions
- tabs may become scrollable tab bars or section menus
- charts resize and retain accessible data alternatives
- forms become single-column when needed
- sticky actions respect viewport/safe areas and on-screen keyboards

## Offline model
Define data classes:
1. public/static shell — cacheable
2. ordinary user data — optionally safe for short-lived read cache
3. confidential business files — restrictive cache policy
4. Vault secrets — never persisted offline
5. mutations — online by default; only explicitly safe actions may be queued

When cached data is shown, display last refreshed time and offline/stale state.

## Service worker
Use a maintained PWA approach compatible with the chosen Lovable-generated stack. Strategies may include precache for shell/static assets, network-first for frequently changing authenticated data, and explicit exclusions for secrets/high-risk endpoints.

## Push notifications
Support web push where platform/browser permits. Push content should be privacy-conscious: enough context to act, not unnecessary sensitive detail on a lock screen. Clicking opens the intended deep link after authentication/authorization.

## Update lifecycle
Detect new application versions and provide a controlled refresh/update experience. Avoid silently replacing active forms or losing unsaved work.

## Connectivity and recovery
Handle intermittent networks, request retries, duplicate submissions and stale sessions gracefully. Long forms should preserve safe drafts. Uploads show resumable/retry behavior where feasible.

## Device capabilities
Where useful and permission-safe, allow camera capture, file picker, share sheet, copy-to-clipboard and biometrics/passkey flows supported by the browser/platform.

## Accessibility
Touch targets, keyboard navigation, focus order, screen-reader landmarks, orientation changes, zoom, reduced motion, contrast and text resizing are mandatory. Target WCAG 2.2 AA.

## Testing matrix
At minimum cover representative small phone, large phone, tablet, laptop and wide desktop widths; portrait/landscape where relevant; installed/standalone mode; offline/intermittent network; reduced motion; keyboard-only; and major supported browsers.

## Acceptance criteria
- no core Portal flow requires desktop
- common Admin flows such as notification review, incident acknowledgement, task update, client lookup and approval work on phone
- no secret is written to offline cache
- queued/retried mutations are idempotent or clearly guarded
- update prompts preserve unsaved work
- layouts have no unexplained overflow at supported widths

## Lovable build slices
PWA is not a late standalone build slice. Every feature slice includes responsive/PWA acceptance. Foundation work establishes manifest, service-worker strategy, responsive shell, offline state primitives, push capability abstraction and test breakpoints.