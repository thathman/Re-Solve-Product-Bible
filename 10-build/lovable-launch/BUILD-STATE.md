# Re:Solve Lovable Build State

Keep this file updated after each supervised build review so the next Product Bible prompt is based on actual application state rather than assumptions.

## Current stage
**FOUND-001A ACCEPTED — FOUND-001B ACCEPTED/CLOSED — FOUND-001C1-C5C ACCEPTED/FROZEN — SECURITY GOVERNANCE REMEDIATION REQUIRED BEFORE C5D**

## Canonical repositories
- Product Bible: `thathman/Re-Solve-Product-Bible` — public, specification/planning only.
- Current Lovable app: `thathman/re-solve-c560d62c` — private, `main`.
- Legacy/reference app: `thathman/Re-Solve` — untouched pending explicit post-FOUND-001 owner approval.
- Canonical-name transition performed: `NO`.

## Lovable project
- Project Knowledge installed: YES.
- Canonical workspace Skills installed: YES — 30 Re:Solve skills + `self-host-check`.
- Platform default skill active: `design-taste-frontend`.

## Backend state
- Lovable Cloud enabled for development.
- Custom database tables: none.
- RLS policies: none.
- Migrations: not initialized.
- Demo seed/reset: not initialized.
- Auth/domain implementation: not yet built.

Never store credentials/secrets in this file.

## Accepted foundation

### FOUND-001A — Stack & Repository Foundation
**ACCEPTED**
TanStack Start v1 + React 19.2 + Vite 8.2 + TypeScript 5.8 + Bun 1.3.3 + Tailwind 4.2.1. Radix-based shadcn source setup preserved.

### FOUND-001B — UI Stack & Design Tokens
**ACCEPTED + CLOSED**
Re:Solve semantic OKLCH tokens, light/dark/system theming, typography, density/layout/elevation/focus/safe-area/motion contracts and shadcn compatibility mappings accepted.

Component Gallery:
- source: `src/routes/__dev/ui.tsx`;
- browser route: `/ui`;
- production guard: `beforeLoad` + `import.meta.env.PROD` redirect to `/`.

### FOUND-001C1 — Core UI Primitive Foundation
**ACCEPTED / CANONICAL / FROZEN**
Button, IconButton, Badge, StatusBadge, ResolveAvatar, Tooltip, Separator, Skeleton, Metric, MetricDelta.

### FOUND-001C2 — Forms & Controls
**ACCEPTED / CANONICAL / FROZEN**
Input, Textarea, Checkbox, RadioGroup, Switch, Select, FormField, FieldGroup.

### FOUND-001C3 — Interaction & Overlay Pack
**ACCEPTED / CANONICAL / FROZEN**
Dialog, AlertDialog, Sheet/SheetBody, Drawer/DrawerBody, Popover, HoverCard, DropdownMenu, ContextMenu, Accordion, Collapsible, Tabs, ScrollArea/ScrollBar.

### FOUND-001C4 — Utility, Feedback & Composition Pack
**ACCEPTED / CANONICAL / FROZEN**
Alert, Empty, StatePanel, Spinner, Progress, typed Sonner Toast boundary, Item family, ButtonGroup family, InputGroup family, Kbd, Toggle/ToggleGroup and Breadcrumb.

Known non-blocking limitation:
- Item public forwarded ref remains div-biased when `asChild` renders another semantic element.

### FOUND-001C5A — Advanced Input Primitives I
**ACCEPTED / CANONICAL / FROZEN**
Command/CommandDialog, Combobox, NativeSelect family, InputOTP family and Slider are canonical.

### FOUND-001C5B — Calendar, Date Selection, Pagination & Resizable
**ACCEPTED / CANONICAL / FROZEN**
Calendar, DatePicker, DateRangePicker, Pagination family and ResizablePanelGroup/ResizablePanel/ResizableHandle are canonical.

### FOUND-001C5C — Display Primitives
**ACCEPTED / CANONICAL / FROZEN**
Card family, semantic Table family and AspectRatio are canonical.

Accepted C5C contracts:
- Card variants: default, raised, subtle and semantic interactive/asChild;
- only interactive Card receives hover/focus affordance;
- interactive Card uses frozen Re:Solve focus-variable contract;
- simple Table uses native HTML table semantics and bounded horizontal scrolling;
- static TableRow has no default hover affordance;
- selected-row visual state remains available without introducing DataTable behavior;
- currency display uses symbols such as `$1,250.00` in normal UI;
- AspectRatio is a thin Core wrapper over pre-existing `@radix-ui/react-aspect-ratio`;
- Display Primitives gallery evidence is accepted;
- no C5C dependency added.

Lovable reported frozen install, build, lint and `tsc --noEmit` passing. GitHub source review verified the resulting contracts; GitHub review does not independently execute Bun.

## Currency display convention
**CANONICAL**
- Internal/data/API currency identity remains explicit via ISO codes.
- Normal user-facing UI uses locale-appropriate currency symbols where unambiguous.
- No universal default currency.

## Security governance state
**REMEDIATION REQUIRED BEFORE C5D**

### Security-memory drift
Lovable surfaced an empty security-memory template after C5C rather than the previously approved Re:Solve-specific rules. Treat the empty template as non-canonical. Before C5D, replace it with an accurate concise scanner-oriented Re:Solve security memory that covers the actual foundation and future access-control rules without claiming unimplemented auth/RLS systems already exist.

### Dependency scan — 2026-08-08
User-provided dependency scan reports one High vulnerability finding associated with `@tanstack/react-start` through transitive `js-yaml`:
- advisory: GHSA-5p4m-2wfm-xmqj;
- affected js-yaml: >=4.0.0,<4.3.1 (and legacy 3.x before 3.15.1);
- patched js-yaml 4.x: 4.3.1;
- impact: algorithmic-complexity CPU denial of service when parsing attacker-controlled YAML.

Do not blindly add an override. First identify the exact installed `js-yaml` version and dependency chain with Bun, determine whether a safe compatible transitive update/lock refresh resolves it, and prefer an upstream-compatible package update over forced overrides. If no clean compatible resolution exists, document exposure and mitigation and stop for supervisor review.

### AspectRatio provenance accuracy
`package.json` declares `@radix-ui/react-aspect-ratio` as `^1.1.8`; the 2026-08-08 scanner reports resolved version 1.1.15. Provenance should distinguish declared range from resolved version instead of treating 1.1.8 as the installed resolved version.

## Security memory baseline
The old 13-rule prose should not be blindly pasted into the new scanner template. Use the scanner's three sections:
- Security Memory: concise description of Re:Solve and its server-authoritative access-control model;
- What should never happen within apps business logic: invariant security failures the scanner should flag;
- What to not create vulnerabilities for: accepted-risk exceptions only; currently none unless explicitly approved by the owner/supervisor.

No actual credentials/secrets belong in security memory.

## Current architecture facts
- TanStack Start v1 + Vite 8.2 + React 19.2.
- Bun 1.3.3 canonical package manager.
- Tailwind 4.2.1.
- shadcn source setup `new-york`; do not rerun init.
- primitive base: individual Radix packages + source-owned shadcn.
- Calendar/date foundation: react-day-picker 9.14.0 + date-fns 4.1.0.
- Resizable foundation: react-resizable-panels 4.6.5.
- Testing stack not canonical/configured.
- Auth, database/RLS, PWA and domain implementation remain later work.

## UI source direction
- Re:Solve Core is the public UI boundary.
- Keep the established Radix foundation; no wholesale Base UI/React Aria migration.
- shadcn-vue remains visual/composition reference only; never runtime Vue code.
- Untitled UI and Tremor remain selective source/reference systems.

## Planned later work
- FOUND-001C5D: DataTable foundation, after security remediation gate passes.
- Further Core-gap audit only after DataTable.
- Admin shell, Portal shell, identity/auth/permissions, PWA/accessibility/CI/security hardening and integrated review remain later FOUND-001 work.

## Next action
Execute the supervisor-provided security-memory + dependency-advisory remediation gate. Re-review before C5D. Do not begin DataTable yet.