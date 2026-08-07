# FOUND-001 Review — Re:Solve Foundation

Run this after Lovable completes FOUND-001 and before authoring any business-domain slice.

Grade each section **PASS**, **CONDITIONAL**, or **FAIL**. Any critical FAIL blocks the next slice.

## 1. Scope discipline
- [ ] No Dashboard business content beyond explicit NotBuilt/demo shell state.
- [ ] No CRM/Organisation/Contact business CRUD.
- [ ] No Properties/Projects/Sales/Billing/Support/Vault/Automation implementation.
- [ ] No real provider integration.
- [ ] No full future schema scaffolding.
- [ ] No HR, Timesheets/Time Tracking or Client Service Consumption.

## 2. Repository and architecture
- [ ] Lovable-created GitHub repository is connected and syncing.
- [ ] Root `AGENTS.md` exists and matches durable Re:Solve rules.
- [ ] Source structure has clear app shell/Core UI/auth/services/data boundaries.
- [ ] Business/provider logic is not embedded indiscriminately in presentational components.
- [ ] Supabase/provider-specific use is reasonably centralized.
- [ ] migrations/config/environment handling is explicit.
- [ ] no Lovable-only product-critical runtime assumption was introduced.

## 3. Core UI Component Framework
- [ ] Design tokens are coherent and source-controlled.
- [ ] shadcn/ui materially influences implementation.
- [ ] Untitled UI React materially influences application composition/polish.
- [ ] Tremor materially influences appropriate metric/data patterns or the framework clearly prepares for it without adding decorative charts.
- [ ] React Aria/Base UI/Radix primitives are used where they materially improve accessibility/behavior.
- [ ] final UI looks like one Re:Solve system rather than stitched libraries.
- [ ] reusable Core components are used instead of page-specific duplicates.

## 4. Component Gallery
- [ ] Gallery exists and is clearly development-only.
- [ ] typography/tokens shown.
- [ ] buttons/inputs/form basics shown.
- [ ] Avatar/AccountMenu shown.
- [ ] Sidebar states shown.
- [ ] TopBar shown.
- [ ] NotificationTrigger/Tray shown with realistic states.
- [ ] Àríyá trigger/panel shown.
- [ ] Search/Command + Quick Create shown.
- [ ] overlay/menu primitives shown.
- [ ] loading/skeleton/empty/error/permission/offline/not-built/connection states shown.
- [ ] representative long-label/high-count/narrow-width cases shown.

## 5. Admin Sidebar/navigation
- [ ] Root labels are obvious to a first-time operator.
- [ ] hierarchy is shallow.
- [ ] strong active route/section state.
- [ ] expanded mode is the clear default learning state.
- [ ] collapsed mode remains discoverable and accessible.
- [ ] no Odoo-style app grid/module launcher.
- [ ] no Twenty-style object/module switcher as primary navigation.
- [ ] no icon-only root navigation.
- [ ] no giant nested accordion tree.
- [ ] child destinations are represented as area-level navigation/not-built routes rather than permanent root clutter.
- [ ] plugin extension space cannot trivially overwhelm root nav.

## 6. TopBar/global chrome
- [ ] current page/context is obvious.
- [ ] Search/Command is visible without knowing a keyboard shortcut.
- [ ] Quick Create has a clear canonical entry.
- [ ] Àríyá has a stable, distinctive but restrained entry.
- [ ] Notification unread state is visible without shouting.
- [ ] Account/Avatar is unmistakably interactive.
- [ ] connection/degraded status appears only when useful.
- [ ] top bar is not decorative empty space or random shortcut clutter.

## 7. ResolveAvatar / AccountMenu
- [ ] image + initials fallback.
- [ ] accessible identity label.
- [ ] identity/role/context summary.
- [ ] Profile.
- [ ] Preferences/Appearance.
- [ ] Notification preferences entry.
- [ ] Security/Sessions entry.
- [ ] Admin/Portal switching only when authorized.
- [ ] Sign out.
- [ ] not merely `Profile / Log out`.

## 8. Notification foundation
- [ ] canonical trigger/tray/item components.
- [ ] unread/read states.
- [ ] restrained priority treatment not color-only.
- [ ] grouping/context.
- [ ] primary deep-link/action pattern.
- [ ] read/unread and relevant snooze/archive demonstration.
- [ ] link to future full Notification Center.
- [ ] no sensitive demo content.

## 9. Àríyá foundation
- [ ] user-facing spelling/name is **Àríyá**.
- [ ] not a generic floating purple sparkle bubble.
- [ ] global entry in TopBar/Command system.
- [ ] panel/workspace foundation feels native to Re:Solve.
- [ ] mock evidence/source/freshness presentation establishes future contract where demonstrated.
- [ ] no real provider/tool implementation was prematurely added.
- [ ] Chatwoot Captain separation remains explicit.

## 10. Client Portal shell
- [ ] visually related to Admin but calmer/less dense.
- [ ] simple goal-oriented destinations.
- [ ] mobile-first navigation is intentional.
- [ ] Account/Notifications/support entry are easy to reach.
- [ ] Vault is not advertised to users with no access.
- [ ] no Admin-only technical/platform language leaks into client navigation.
- [ ] client-safe NotBuilt/permission/error states.

## 11. Identity/permission foundation
- [ ] Workspace is distinct from Operating Entity.
- [ ] Airix Media is Operating Entity, not client Organisation.
- [ ] User is human identity; Principal abstraction is represented cleanly where needed.
- [ ] Membership/role/capability context is sufficient for shell routing.
- [ ] staff enters Admin.
- [ ] client enters Portal.
- [ ] direct Admin URL access by client is denied server-side/equivalent backend guard.
- [ ] at least one negative authorization path is tested/verifiable.

## 12. Responsive/device QA
Review at representative small phone, large phone, tablet, laptop and desktop widths.
- [ ] no unexplained page-level horizontal overflow.
- [ ] Admin mobile navigation is recomposed, not squeezed Sidebar.
- [ ] Portal mobile shell is genuinely usable.
- [ ] Search/Notifications/Account remain reachable.
- [ ] Àríyá does not cover critical actions.
- [ ] overlays respect small screens/safe areas/on-screen keyboard.
- [ ] long labels/large unread counts do not break chrome.

## 13. PWA/offline
- [ ] manifest/installability foundation.
- [ ] source-controlled service-worker strategy.
- [ ] offline shell/fallback.
- [ ] stale/offline indication.
- [ ] app update lifecycle does not threaten unsaved work.
- [ ] cache policy distinguishes sensitive data.
- [ ] no Vault/secret data is intentionally cached.

## 14. Accessibility
- [ ] semantic landmarks/headings.
- [ ] keyboard access to Sidebar/TopBar/menus/overlays.
- [ ] visible focus.
- [ ] dialog/drawer/popover focus restore.
- [ ] accessible names for icon buttons/avatar/notifications/Àríyá.
- [ ] status/priority is not color-only.
- [ ] contrast is acceptable.
- [ ] touch targets are usable.
- [ ] reduced motion is respected.

## 15. Quality/tests
- [ ] strict TypeScript/config equivalent.
- [ ] lint/format checks.
- [ ] component/unit tests for meaningful foundation behavior.
- [ ] browser/flow test for Admin/Portal access where practical.
- [ ] no meaningful console/runtime errors in core routes.
- [ ] no dead placeholder components/libraries added "for later".

## 16. Portability
- [ ] `self-host-check` run.
- [ ] no product-critical Lovable runtime dependency.
- [ ] source can plausibly build outside Lovable.
- [ ] provider/auth/storage boundaries are not scattered.
- [ ] PWA/UI/config are ordinary source files.
- [ ] no premature Docker/Kubernetes/production-hosting work.

## 17. Visual quality gate
Use `/resolve-design-review` and answer:
- Does this look intentionally Re:Solve, or like a default generated admin template?
- Are Sidebar/TopBar/Avatar/Notifications/Àríyá visually strong enough to be reused for years?
- Is hierarchy obvious without excessive cards/badges?
- Is operational density calm rather than cramped?
- Does the Portal feel trustworthy and simpler than Admin?
- Is there any raw-library styling that needs normalization before business modules begin?

## Final decision
### PASS
FOUND-001 is accepted. Repository transition may be considered, then author the next bounded slice from actual implementation.

### CONDITIONAL
Only small non-architectural polish remains. Record exact items and complete them before the first dependent domain slice.

### FAIL
Do not build business modules. Fix foundation first.

## Required review record
Capture:
- Lovable project name;
- GitHub repository name/default branch;
- application stack/dependencies;
- Supabase/backend state;
- review date;
- results per section;
- screenshots/links if useful;
- blockers/waivers;
- Product Bible changes needed;
- final PASS/CONDITIONAL/FAIL decision.