# Planned Optional Domain Extensions

## Purpose
Re:Solve is intentionally broad in architecture but should not force every specialist domain into core. This document records capabilities we expect may eventually be delivered as first-party/private Plugins so current architecture preserves the right extension points without prematurely implementing them.

These are roadmap/spec acknowledgements, not FOUND-001 scope.

## Advanced Accounting
Potential scope:
- chart of accounts;
- journals/ledger;
- vendor/customer accounting;
- statutory reports;
- bank feeds/reconciliation depth;
- jurisdiction extensions.

Core Billing remains operational receivables/payments/credits/statements and does not depend on a full accounting ledger.

## Procurement & Vendor Operations
Potential scope:
- supplier/vendor Organisations;
- purchase requests;
- purchase orders;
- vendor bills;
- approvals;
- recurring vendor commitments;
- receiving/evidence;
- cost allocation to Organisation/Property/Project/Service;
- procurement reporting.

Core Operational Spend/Expenses provides lightweight cost visibility until this depth is needed.

No payroll/employee expense/HR workflow is implied.

## Hosting Operations
Potential scope:
- hosting accounts/plans;
- servers/resources;
- provisioning;
- backup/restore operations;
- usage/capacity from hosting providers;
- maintenance;
- renewal/provider cost;
- Property Posture signals;
- controlled Actions.

Hosting operational metrics are infrastructure/provider data, not Client Service Consumption.

## OJS / Journal Operations
Potential scope:
- OJS installation management;
- journals/publications;
- version/update posture;
- scheduler/jobs;
- publishing workflows;
- approved submission/editorial metadata;
- release/update/maintenance operations;
- journal-specific reporting.

Privacy/blind-review/editorial confidentiality remain strict.

## WordPress / Website Operations
Potential scope:
- WordPress inventory;
- plugins/themes;
- update/health posture;
- backups;
- content/maintenance operations;
- website reports;
- security/maintenance Actions.

## WooCommerce / Commerce Operations
Potential scope:
- orders;
- fulfilment/delivery;
- catalogue/product context;
- customer mappings;
- refunds/commerce operations;
- store health;
- reporting.

Provider/commerce payment state does not automatically replace Re:Solve Billing truth.

## SEO / Growth Operations
Potential scope:
- SEO audits;
- keyword/page tracking;
- technical checks;
- recommendations;
- client reports;
- campaign/project integration.

Specialist search/analytics providers integrate through Connectors.

## Marketing / Campaign Operations
Sophisticated newsletters, automations, campaigns, segments and deliverability should normally remain specialist-system territory such as Brevo or future providers.

A Re:Solve Marketing Plugin could provide:
- campaign planning/context;
- audience/segment references;
- approval;
- launch through Marketing Connector;
- provider result/report references;
- client/project relationship.

Re:Solve should not casually become a bulk email marketing engine.

## Asset / Inventory Operations
Potential client/internal asset tracking where a deployment needs non-Property physical/business assets.

Property remains the native digital/operational asset model and should not be diluted to accommodate every physical inventory use case.

## Structured/E-Invoice Document Formats
Country/industry-specific invoice schemas, XML/JSON/e-invoice export, fiscal integrations and compliance validation can be supplied by jurisdiction/provider Plugins/Connectors while Billing and Document Studio remain provider-neutral.

## Advanced Reporting / BI
Potential custom datasets, scheduled reporting packs, warehouse/BI connectors and richer visualization beyond core Reports.

No unrestricted SQL is exposed to ordinary users/agents.

## Data Import Packs
Specialized migration packages for Perfex, HubSpot, EspoCRM, ERPNext, Odoo or other legacy systems may register importers, transformations and reconciliation checks using the core Import/Data Quality platform.

## Airix Food Operations
A future first-party Plugin may add food-order/event/fulfilment operational domains while reusing Re:Solve identity, clients, Billing, Notifications, Documents, Connectors, API/MCP and Core UI where appropriate.

## Extension UX rules
Every planned domain extension must:
- use Core UI Component Framework;
- respect simple navigation governance;
- prefer tabs/views/contextual Actions over adding root navigation;
- use canonical Principal/permission/Action/Audit contracts;
- integrate Attention/Notifications rather than inventing parallel inboxes;
- declare data provenance/Connector truth;
- remain responsive/PWA/accessibility compatible.

## Explicit exclusions
Even as optional extensions, the current Re:Solve product direction does **not** plan:
- HR/payroll/recruitment/leave/attendance/employee performance;
- Timesheets/Time Tracking;
- Client Service Consumption / remaining-hours/credits metering.

Adding one of those would require a new explicit product decision rather than being treated as an assumed future extension.
