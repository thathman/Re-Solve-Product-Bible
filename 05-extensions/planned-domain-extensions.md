# Planned Optional Domain Extensions

## Purpose
Re:Solve is intentionally broad in architecture but should not force every specialist domain into core. This document records capabilities that may eventually be delivered as first-party/private Plugins or future product expansions so current architecture preserves extension points without prematurely implementing them.

These are roadmap/spec acknowledgements, not current-run scope unless another canonical phase explicitly absorbs them.

## Advanced Accounting
Potential chart of accounts, journals/ledger, statutory reports, bank-feed depth and jurisdiction extensions. Core Billing remains operational receivables/payments/credits/statements and does not depend on full accounting.

## Procurement & Vendor Operations
Potential suppliers/vendors, purchase requests/orders, vendor bills, approvals, recurring vendor commitments, receiving/evidence and cost allocation. Core Spend/Expenses remains lightweight. No payroll/HR implication.

## Hosting Operations
Potential hosting accounts/plans, servers/resources, provisioning, backup/restore operations, capacity/provider metrics, maintenance, renewal/provider cost, Property Health signals and controlled Actions. Infrastructure usage is not Client Service Consumption.

## OJS / Journal Operations
Potential OJS installation/journal/version/update posture, scheduler/jobs, publishing workflows, approved editorial metadata, maintenance and reporting with strict confidentiality.

## WordPress / Website Operations
Potential WordPress inventory, plugins/themes, updates/health, backups, maintenance operations, reports and security Actions.

## WooCommerce / Commerce Operations
Potential orders, fulfilment/delivery, catalogue/customer mapping, refunds/commerce operations, store health and reporting. Provider commerce payment state does not automatically replace Re:Solve Billing truth.

## SEO / Growth Operations
Potential SEO audits, keyword/page tracking, technical checks, recommendations and client reports through specialist connectors.

## Marketing / Campaign Operations
Sophisticated newsletters/campaigns/segments/deliverability remain specialist-system territory. A future Re:Solve Marketing Plugin may provide planning/context/approval/provider launch/result references without rebuilding a bulk email marketing engine.

## Asset / Inventory Operations
Potential non-Property physical/business asset tracking. Property remains the native digital/operational asset model.

## Structured / E-Invoice Formats
Country/industry-specific invoice schemas, XML/JSON/e-invoice export, fiscal integrations and compliance validation through Plugins/Connectors while Billing/Document Studio remain provider-neutral.

## Advanced Reporting / BI
Potential custom datasets, scheduled reporting packs, warehouse/BI connectors and richer visualization. No unrestricted SQL for ordinary users/agents.

## Data Import Packs
Specialized migration packages for Perfex, HubSpot, EspoCRM, ERPNext, Odoo and other legacy systems may register importers/transformations/reconciliation checks using core Import/Data Quality.

## Distant Future — Headless CMS / Public Content Platform
A future Re:Solve expansion may provide a structured headless CMS for external public frontends, including Pages/Collections, reusable blocks, navigation, media, SEO metadata, redirects, draft/version/preview, scheduled publishing, approval and a read-only public content API/webhooks.

**This CMS is explicitly not part of the current development run.**

Current-run rules:
- no CMS schemas/migrations;
- no CMS Admin/Portal routes;
- no page builder;
- no public content API work;
- no CMS phase dependency;
- no attempt to migrate the separate Airix frontend into Re:Solve.

The architecture should merely avoid choices that make a later headless-CMS/plugin expansion impossible.

## Airix Food Operations
A future first-party Plugin may add food-order/event/fulfilment domains while reusing Re:Solve identity, clients, Billing, Notifications, Documents, Connectors, API/MCP and Core UI where appropriate.

## Extension UX rules
Every planned extension must use Core UI, respect simple navigation, prefer contextual tabs/views/actions over root-nav sprawl, use canonical Principal/permission/Action/Audit contracts, integrate Attention/Notifications, declare data provenance and remain responsive/PWA/accessibility compatible.

## Explicit exclusions
Even as optional extensions, the current product direction does not plan HR/payroll/recruitment/leave/attendance/performance review, Timesheets/Time Tracking/work timers, or Client Service Consumption/remaining-hours/credit metering. Adding one requires a new explicit owner product decision.
