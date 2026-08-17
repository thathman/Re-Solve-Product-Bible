# Phase 4 — Admin & Client Portal Experience Reset

Prefix: `UXR`
Canonical scope: `UXR-001...126`

## Purpose
Establish the clean Admin and Client Portal product shell before delivery-domain expansion. Replace presentation/navigation/workspace contracts while preserving Phase 3 database truth, RLS, permissions, tenant isolation, commercial authority and existing working domain behavior.

## Dependencies
- Phase 3B Commercial Completion closed and promoted to `main`.
- Production baseline is the v1.26 line.
- Existing Admin/Portal route guards and Supabase RLS remain authoritative.
- Existing Action Registry, Activity, Audit, Attention and commercial primitives are preserved.

## Explicitly out of scope
- Broad new domain engines.
- Projects/Tasks/Forms delivery depth; owned by Phase 5.
- HR/payroll/recruitment/leave/attendance/performance/timesheets/work timers.
- Full accounting/general ledger, inventory, manufacturing, POS.
- CMS/public-content functionality.
- Duplicate native live chat.

## Data and migration risk
Prefer presentation/configuration changes. Do not introduce speculative schema merely for UI convenience. Any configuration persistence must preserve RLS/tenant boundaries and must not become an authorization substitute.

## External dependencies
No provider integration is required to complete the experience contract. Existing Chatwoot/Ariya/OpenShip/Supabase boundaries are preserved.

## Browser acceptance
One consolidated Admin + Portal desktop/mobile acceptance is reserved for `UXR-125`. Internal slices do not claim browser closure.

## Atomic ledger

### A. Entry audit & canonical UX contract
- ⬜ UXR-001 Verify current `main`, v1.26 production SHA, CI and OpenShip baseline.
- ⬜ UXR-002 Inventory current Admin routes, shell, navigation and workspace primitives.
- ⬜ UXR-003 Inventory current Portal routes, shell, navigation and homepage primitives.
- ⬜ UXR-004 Audit PR #27 against current `main`; preserve only changes still correct after Phase 3.
- ⬜ UXR-005 Reconcile Phase 3 residual UX findings into Phase 4 ownership.
- ⬜ UXR-006 Review open Product Oversight items that belong to presentation/experience.
- ⬜ UXR-007 Lock Phase 4 rule: no authorization/data-truth weakening for UI convenience.
- ⬜ UXR-008 Lock Phase 4 rule: no broad new domain engines or speculative schema.
- ⬜ UXR-009 Record Admin and Portal experience contracts in the canonical Product Bible.
- ⬜ UXR-010 Create clean Phase 4 branch from current `main` and open the phase PR.

### B. Admin information architecture
- ⬜ UXR-011 Establish canonical Admin top-level order: Home, Tasks, Clients, CRM, Sales, Delivery, Support, Billing, Forms, Calendar, Information, Reports, Automations, Settings.
- ⬜ UXR-012 Preserve route compatibility for existing working URLs while IA changes.
- ⬜ UXR-013 Ensure Home routes to the real Admin operational workspace.
- ⬜ UXR-014 Represent Tasks in navigation without prematurely building the Phase 5 Tasks engine.
- ⬜ UXR-015 Consolidate Client-facing organisation/contact/property entry points under Clients.
- ⬜ UXR-016 Consolidate Lead/Opportunity commercial acquisition surfaces under CRM.
- ⬜ UXR-017 Consolidate Proposal/Contract/Recurring commercial surfaces under Sales.
- ⬜ UXR-018 Establish Delivery navigation contract without prematurely rebuilding Projects.
- ⬜ UXR-019 Preserve Support as a first-class operational area.
- ⬜ UXR-020 Consolidate Invoice/Payment/Adjustment surfaces under Billing.
- ⬜ UXR-021 Reserve Forms navigation cleanly for the Phase 5 engine without dead misleading UX.
- ⬜ UXR-022 Establish Calendar navigation contract without speculative calendar authority.
- ⬜ UXR-023 Define Information grouping for Files/Knowledge/Vault as those domains mature.
- ⬜ UXR-024 Preserve Reports and Automations as coherent future-facing areas without fake data.
- ⬜ UXR-025 Consolidate configuration under Settings and remove duplicate account/settings entry points.
- ⬜ UXR-026 Remove dead, duplicate, misleading and unreachable Admin nav paths.

### C. Admin shell / global chrome
- ⬜ UXR-027 Redesign Admin sidebar proportions, rhythm and visual hierarchy.
- ⬜ UXR-028 Implement clear expanded/collapsed sidebar states.
- ⬜ UXR-029 Implement reliable active-route and child-route indication.
- ⬜ UXR-030 Move global search/command entry to the top bar.
- ⬜ UXR-031 Keep exactly one account control.
- ⬜ UXR-032 Preserve theme/appearance control without shell clutter.
- ⬜ UXR-033 Make global actions discoverable without turning the top bar into a toolbar dump.
- ⬜ UXR-034 Keep Àríyá persistent bottom-right and non-draggable.
- ⬜ UXR-035 Preserve skip-to-content and keyboard shell navigation.
- ⬜ UXR-036 Standardize shell width, gutters and content max-width.
- ⬜ UXR-037 Standardize page-header title/description/action hierarchy.
- ⬜ UXR-038 Preserve breadcrumbs only where they materially improve record orientation.
- ⬜ UXR-039 Ensure Admin pending/loading state appears immediately during cold navigation.
- ⬜ UXR-040 Add graceful shell-level error presentation.
- ⬜ UXR-041 Add graceful not-found/invalid-route experience instead of blank screen.
- ⬜ UXR-042 Verify shell chrome does not obscure content on desktop or mobile.

### D. Admin Home / operational briefing
- ⬜ UXR-043 Redesign Admin Home as an operational briefing, not a card gallery.
- ⬜ UXR-044 Keep only 3–6 useful top-level metrics at a time.
- ⬜ UXR-045 Ensure every metric is database-backed or truthfully derived.
- ⬜ UXR-046 Keep unlike currencies separate in Home financial summaries.
- ⬜ UXR-047 Surface real Attention items as the primary “what needs me” area.
- ⬜ UXR-048 Surface real assigned/open work without inventing workload state.
- ⬜ UXR-049 Surface useful delivery/commercial targets only when backed by real records.
- ⬜ UXR-050 Surface recent Activity with meaningful chronology and context.
- ⬜ UXR-051 Remove decorative filler metrics/cards.
- ⬜ UXR-052 Make high-impact Home actions route through existing guarded actions.
- ⬜ UXR-053 Provide truthful empty states when briefing data is absent.
- ⬜ UXR-054 Ensure Home remains useful at narrow/mobile widths.
- ⬜ UXR-055 Preserve commercial Attention truth established in Phase 3.

### E. List and record workspace contract
- ⬜ UXR-056 Define one canonical list-page hierarchy.
- ⬜ UXR-057 Define one canonical record-page hierarchy.
- ⬜ UXR-058 Standardize record identity/header/state/action presentation.
- ⬜ UXR-059 Standardize summary → tabs → state/activity → related data → contextual rail.
- ⬜ UXR-060 Standardize search/filter/sort/view controls on list pages.
- ⬜ UXR-061 Standardize bulk-action placement without building Phase 9 bulk-action authority.
- ⬜ UXR-062 Standardize tables for density, overflow and row actions.
- ⬜ UXR-063 Standardize truthful empty/loading/error states.
- ⬜ UXR-064 Standardize status/badge presentation and human-readable labels.
- ⬜ UXR-065 Apply workspace contract to Clients.
- ⬜ UXR-066 Apply workspace contract to CRM.
- ⬜ UXR-067 Apply workspace contract to Sales.
- ⬜ UXR-068 Apply workspace contract to Billing.
- ⬜ UXR-069 Apply workspace contract to Support.
- ⬜ UXR-070 Apply workspace contract to Properties/current Delivery surfaces without rebuilding their engines.
- ⬜ UXR-071 Verify record actions remain permission-aware/server-authoritative.
- ⬜ UXR-072 Verify workspace layouts remain usable without a right rail when no real contextual content exists.

### F. Persistent/contextual Àríyá
- ⬜ UXR-073 Define one persistent Àríyá shell entry point across Admin.
- ⬜ UXR-074 Pass current route/workspace context into Àríyá presentation.
- ⬜ UXR-075 Pass current record identity/context only when authorized.
- ⬜ UXR-076 Distinguish Ask/Draft/Act/Watch/Investigate/Recommend affordances without pretending unsupported actions exist.
- ⬜ UXR-077 Preserve Action Registry/permission checks for all executable actions.
- ⬜ UXR-078 Preserve confirmation/risk boundaries for high-impact actions.
- ⬜ UXR-079 Implement accessible open/close/focus behavior.
- ⬜ UXR-080 Ensure Àríyá does not cover important mobile controls/content.
- ⬜ UXR-081 Keep Support/Chatwoot conceptually separate from Àríyá intelligence.

### G. Client Portal IA & shell reset
- ⬜ UXR-082 Establish deliberately small Portal navigation: Home, Projects, Billing, Support, Files, More.
- ⬜ UXR-083 Hide Portal destinations the principal lacks capability to view.
- ⬜ UXR-084 Preserve active-membership authority and suspended/revoked denial.
- ⬜ UXR-085 Redesign Portal shell around warm-paper/charcoal/terracotta language.
- ⬜ UXR-086 Preserve Space Grotesk and selective Instrument Serif use.
- ⬜ UXR-087 Remove Admin-style operational density from client-facing surfaces.
- ⬜ UXR-088 Standardize Portal page headers and action hierarchy.
- ⬜ UXR-089 Standardize Portal loading/empty/error states.
- ⬜ UXR-090 Keep client actions visually distinct from read-only information.
- ⬜ UXR-091 Preserve one clear account/navigation control model.
- ⬜ UXR-092 Ensure Portal shell works at 390–500px without horizontal overflow.
- ⬜ UXR-093 Prevent floating Àríyá/chat controls from overlapping content.
- ⬜ UXR-094 Preserve tenant-safe direct-record navigation and 404 behavior.
- ⬜ UXR-095 Preserve secure guest flows as separate pre-membership experiences.

### H. Portal Home / Needs Your Attention
- ⬜ UXR-096 Rebuild Portal Home around “What needs my attention?”
- ⬜ UXR-097 Surface Proposal decisions from authoritative commercial Attention.
- ⬜ UXR-098 Surface Contracts requiring client action.
- ⬜ UXR-099 Surface outstanding Invoice/payment obligations without fake totals.
- ⬜ UXR-100 Reserve Form-completion attention for Phase 5 without fabricating Form records.
- ⬜ UXR-101 Surface useful active Project summary from existing truth without expanding the Project engine.
- ⬜ UXR-102 Surface Support/help entry points clearly.
- ⬜ UXR-103 Surface recent/shared Files only when real client-visible file data exists.
- ⬜ UXR-104 Provide clear truthful “nothing needs you” state.
- ⬜ UXR-105 Preserve server-authoritative `/attention` commercial truth from Phase 3.
- ⬜ UXR-106 Ensure Portal Home remains calm and useful instead of becoming a mini Admin dashboard.

### I. Preview as Client
- ⬜ UXR-107 Define read-only Preview-as-Client server context.
- ⬜ UXR-108 Add Staff entry point to preview an Organisation/Portal principal safely.
- ⬜ UXR-109 Render the exact client-visible shell/data subset permitted to that principal.
- ⬜ UXR-110 Show persistent “Viewing Portal as … — Read Only” banner.
- ⬜ UXR-111 Disable/remove Proposal acceptance, payment, Contract signing, Form submission and client-originated Support mutations.
- ⬜ UXR-112 Enforce read-only behavior server-side; do not rely only on disabled buttons.
- ⬜ UXR-113 Provide explicit exit back to Admin context.
- ⬜ UXR-114 Verify Preview never becomes unrestricted impersonation.

### J. Module visibility + Saved View foundations
- ⬜ UXR-115 Define module-visibility configuration model using existing real installation configuration where possible.
- ⬜ UXR-116 Hide disabled modules from navigation without deleting underlying business data.
- ⬜ UXR-117 Prevent module visibility from becoming an authorization substitute.
- ⬜ UXR-118 Define Saved View foundation for filters/sort/layout preferences without prematurely building Phase 9 universal governance.
- ⬜ UXR-119 Persist Staff view preferences safely and tenant/workspace appropriately.
- ⬜ UXR-120 Provide sane defaults/fallback when a saved view is missing or invalid.

### K. Consistency, accessibility, qualification & closure
- ⬜ UXR-121 Run design-system consistency sweep: spacing, typography, borders, radii, buttons, forms, tables, badges, dialogs and focus states.
- ⬜ UXR-122 Run desktop/mobile accessibility and overflow sweep across representative Admin + Portal routes.
- ⬜ UXR-123 Add/refresh regression tests for shell navigation, capability visibility, Preview read-only boundaries and saved/module preferences.
- ⬜ UXR-124 Run full Vitest → ESLint → TypeScript → production build → PWA/output qualification and reconcile Product Oversight.
- 🟦 UXR-125 Run one consolidated ChatGPT Work browser acceptance: Admin + Portal, desktop + mobile; fix every blocking finding and requalify the corrected exact SHA.
- ⬜ UXR-126 Merge exact green Phase 4 SHA to `main`, independently requalify `main`, deploy exact SHA through OpenShip, verify health, update Product Bible/ledger and close Phase 4.

## Completion definition
Phase 4 closes only when every blocking `UXR` item has evidence, authorization/data truth is unchanged, Admin and Portal browser acceptance is complete, all defers have an explicit later owner/reason, the exact release candidate passes the full quality gate, and the exact tested `main` SHA is healthy in production.
