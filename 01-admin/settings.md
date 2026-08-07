# Settings

## 1. Purpose

Settings is the control plane for Re:Solve. It must expose product configuration deliberately, with clear ownership, safe defaults, validation, auditability, diagnostics, and permission boundaries.

Settings must not become a miscellaneous dumping ground. Every setting belongs to a product domain, has an owner, and has defined consequences.

## 2. Goals

Settings must make it possible to configure and operate Re:Solve without editing source code or database records directly for ordinary administrative work.

It must support:

- workspace configuration;
- users, teams, roles, and permissions;
- client portal policies;
- CRM, properties, projects, sales, billing, support, notifications, communications, AI, vault, files, automation, plugins, connectors, API/MCP, security, and system operations;
- clear save/apply behavior;
- configuration health;
- test tools;
- audit trails;
- responsive access;
- plugin/connector extension sections;
- import/export where safe;
- reset/recovery where safe.

## 3. Information architecture

Top-level Settings groups:

1. General
2. People & Access
3. Client Portal
4. CRM
5. Properties
6. Projects
7. Sales
8. Billing
9. Support
10. Notifications
11. Communications
12. AI
13. Vault
14. Files
15. Automations
16. Plugins
17. Connectors
18. API & MCP
19. Security
20. System

On desktop, use persistent settings navigation with search. On mobile, use a settings index and drill-down pages rather than a permanently visible sidebar.

## 4. Settings search

Settings must support search across:

- section names;
- setting labels;
- descriptions;
- connector/plugin settings;
- security controls;
- feature keywords.

Search result should deep-link to the exact setting or section.

## 5. Shared setting behavior

Every setting should define:

- scope: workspace, team, role, user, client default, property type, connector instance, plugin;
- current value;
- inherited/default value where applicable;
- validation;
- permission required;
- whether change is immediate or requires confirmation/restart/reprocessing;
- whether change is audited;
- whether rollback is possible;
- whether it affects existing records or only new records;
- whether it may trigger notifications.

## 6. Save model

Use the save model best suited to the section:

- immediate save for low-risk toggles/preferences;
- explicit Save changes for grouped configuration;
- Review changes confirmation for high-impact settings;
- test-before-save where provider credentials are involved;
- step-up authentication for highly sensitive changes.

Unsaved changes must be visible and protected against accidental navigation where material.

## 7. Configuration health

Each major settings area should be able to expose:

- configured;
- partially configured;
- needs attention;
- disabled;
- error;
- healthy.

The Settings landing page should summarize areas needing action rather than showing generic cards for every section.

---

# A. General

## A1. Workspace

Fields/options:

- workspace display name;
- legal/business name;
- internal identifier/code;
- primary contact details;
- default business address;
- website/reference URL;
- default logo/mark;
- system display name where configurable;
- default record ownership behavior;
- default archive/delete behavior where appropriate.

## A2. Branding

- logo variants;
- favicon/app icon source;
- approved accent color;
- light/dark logo handling;
- client portal identity;
- authentication screen identity;
- email identity defaults;
- document identity defaults;
- accessibility contrast validation;
- preview across desktop/mobile/email/document contexts.

## A3. Locale

- default language;
- default country/region;
- date format;
- time format;
- first day of week;
- timezone;
- number formatting;
- address formatting;
- phone formatting assumptions.

## A4. Currency

- workspace base currency;
- enabled currencies;
- display precision;
- rounding policy;
- exchange-rate handling policy;
- invoice currency behavior;
- whether manual rates are permitted;
- accounting/reporting base currency behavior.

## A5. Defaults

Central default values that do not logically belong elsewhere, with links to domain-specific defaults rather than duplication.

---

# B. People & Access

## B1. Staff

- active staff;
- invited staff;
- suspended staff;
- role/team membership;
- last sign-in;
- MFA state;
- session/security summary;
- deactivate/reactivate;
- transfer ownership responsibilities before removal.

## B2. Teams

- create/edit/archive team;
- team lead;
- members;
- functional purpose;
- assignment eligibility;
- notification defaults;
- support/project/finance applicability.

## B3. Roles

Roles are named permission bundles.

- system roles;
- custom roles;
- clone role;
- compare roles;
- permission count;
- assigned users;
- risk warning for broad privileges.

## B4. Permissions

Capability-based permission matrix covering all first-class domains and sensitive actions.

Support:

- read;
- create;
- update;
- delete/archive;
- approve;
- export;
- manage settings;
- reveal sensitive values;
- share vault items;
- manage connectors/plugins;
- manage API/MCP;
- impersonation if ever supported, with strong audit.

## B5. Invitations

- invitation expiry;
- resend;
- revoke;
- allowed email/domain policy where useful;
- default role/team;
- onboarding requirements.

## B6. Sessions

- active sessions/devices;
- revoke one/all;
- force reauthentication;
- session timeout defaults;
- privileged-action step-up duration.

---

# C. Client Portal

## C1. Portal Defaults

- portal enabled;
- default welcome/help copy;
- default visible sections;
- client-safe terminology preferences;
- default home modules/widgets;
- support entry behavior;
- portal announcement/banner.

## C2. Client Roles

Initial role concepts may include:

- Organisation Owner;
- Organisation Admin;
- Billing Contact;
- Project Approver;
- Project Participant;
- Technical Contact;
- Vault Authorized;
- Read-only Stakeholder.

Roles remain configurable bundles over client-safe permissions.

## C3. Navigation

- workspace-level feature visibility defaults;
- entitlement-based visibility;
- plugin portal entries;
- ordering constraints;
- mobile priority navigation settings should be system-guided, not arbitrary.

## C4. Registration & Invitations

- self-registration enabled/disabled;
- invite-only mode;
- approved domain rules;
- invitation expiry;
- organisation admin invitation rights;
- approval requirement for new client users.

## C5. Branding

Controlled client-facing branding with accessibility guardrails.

---

# D. CRM

## D1. Lead Sources

- source list;
- active/archive;
- default source;
- reporting grouping.

## D2. Pipelines

- multiple pipelines;
- stages;
- probability/default weighting;
- stage colors using semantic constraints;
- required fields per stage;
- entry/exit automations;
- won/lost behavior.

## D3. Custom Fields

- supported record types;
- field types;
- validation;
- required/optional;
- client visibility;
- API exposure;
- plugin ownership;
- archive behavior.

## D4. Activity Types

- call;
- meeting;
- email;
- note;
- follow-up;
- custom types;
- outcome options;
- default reminder behavior.

---

# E. Properties

## E1. Property Types

Examples:

- website;
- journal;
- OJS installation;
- domain;
- server;
- hosting account;
- application;
- store;
- infrastructure asset;
- custom/plugin-defined type.

Each type may define allowed components, fields, health signals, icons, and plugin extensions.

## E2. Statuses

Operational/business statuses such as active, onboarding, maintenance, suspended, retired, archived.

## E3. Health Rules

- healthy/degraded/critical thresholds;
- stale health behavior;
- monitor weighting;
- incident creation rules;
- client-visible status mapping.

## E4. Maintenance

- maintenance windows;
- recurrence;
- client notifications;
- suppress/annotate monitor alerts;
- maintenance history.

## E5. Domains/Renewals

- expiry thresholds;
- auto-renew expectations;
- notification schedule;
- ownership/registrar defaults.

---

# F. Projects

## F1. Statuses

Configurable project statuses with canonical semantic categories.

## F2. Priorities

Workspace priority vocabulary.

## F3. Task Types

- task;
- client action;
- approval;
- review;
- technical action;
- plugin-defined types.

## F4. Templates

- project templates;
- milestone templates;
- task templates;
- role assignment defaults;
- client action defaults;
- notification/automation defaults.

## F5. Time Tracking

- enabled/disabled;
- billable defaults;
- rounding;
- timer/manual entry policy;
- approval requirements.

## F6. Approvals

- approval states;
- request changes behavior;
- quorum/multiple approvers where enabled;
- deadline/escalation defaults;
- client-safe wording.

---

# G. Sales

## G1. Services Catalogue

- service categories;
- active/archive;
- pricing models;
- default taxes;
- billing cadence;
- default project template;
- default support entitlement;
- property applicability.

## G2. Proposals

- numbering;
- validity period;
- templates;
- default terms;
- approval/signing behavior;
- accepted/declined expiry behavior.

## G3. Estimates/Quotes

- numbering;
- validity;
- conversion rules;
- approval;
- taxes/discount defaults.

## G4. Contracts

- numbering/reference;
- templates;
- signature connector;
- renewal reminders;
- deposit requirements;
- client visibility.

---

# H. Billing

## H1. Invoice Defaults

- numbering scheme;
- prefix;
- due terms;
- issue date behavior;
- line-item defaults;
- notes/terms;
- PDF/template selection.

## H2. Taxes

- tax definitions;
- rates;
- inclusive/exclusive;
- applicability;
- effective dates;
- client exemption handling;
- plugin-provided jurisdiction rules.

## H3. Payment Terms

- standard terms;
- grace periods;
- overdue thresholds;
- reminder schedule;
- late fee behavior if ever enabled.

## H4. Payment Providers

Do not hard-code providers into billing core. Settings surface installed payment plugins/connectors and their instances.

For each provider:

- enabled;
- environment/mode;
- supported currencies;
- payment methods;
- connection test;
- webhook health;
- settlement/reconciliation behavior;
- failure state.

## H5. Subscriptions / Recurring Services

- billing cadence;
- proration policy;
- trial defaults;
- pause/cancel timing;
- renewal generation;
- payment failure policy;
- grace policy.

## H6. Receipts/Credit Notes/Refunds

- numbering;
- generation policy;
- template;
- approval requirements;
- client notification defaults.

---

# I. Support

Chatwoot remains the managed client support engine.

## I1. Chatwoot

Settings should link to the Chatwoot connector instance and expose Re:Solve-specific support policy, not duplicate Chatwoot's entire administration UI.

Show:

- connection state;
- mapped account/inboxes;
- mapping health;
- sync status;
- supported capabilities;
- diagnostics;
- open connector configuration.

## I2. Support Plans / Entitlements

- plan name;
- response targets;
- supported channels;
- business hours;
- included properties/services;
- escalation policy;
- client-visible summary.

## I3. SLA

Re:Solve may retain commercial/operational SLA definitions that relate clients/properties/services to Chatwoot support, while conversation handling remains Chatwoot-owned.

## I4. Categories and Routing Context

Define Re:Solve-side support metadata used for mappings, reporting, and contextual handoff.

---

# J. Notifications

Settings must implement the platform spec in `03-platform/notifications.md`.

Sections:

- Channels;
- Delivery Rules;
- Event Policies;
- Templates;
- Digests;
- Quiet Hours;
- Mandatory Events;
- Retry & Failure;
- Retention;
- Test Center.

## J1. Test Center

Authorized admin can:

- send test in-app notification;
- send test push to own device;
- send test email;
- send test WhatsApp message to approved destination;
- preview templates with sample variables;
- inspect resulting delivery attempts.

---

# K. Communications

## K1. Email

- provider/connector;
- sender identities;
- default from/reply-to;
- domain verification status where available;
- test email;
- bounce/failure diagnostics;
- template relationship.

## K2. WhatsApp/Baileys

Purpose: Re:Solve-to-client operational communication.

Settings:

- connector status;
- linked number/session;
- connection/QR state where applicable;
- approved message categories;
- quiet-hour policy;
- client opt-in/eligibility fields where required;
- message retry;
- media/file policy;
- test message;
- session health;
- disconnect/reconnect;
- audit.

Do not present this as the client-customer support inbox; that remains Chatwoot.

## K3. SMS

Optional connector-based channel.

## K4. Sender Identities

Central view of communication identities and verification/health.

---

# L. AI

Re:Solve AI is independent from Chatwoot AI.

## L1. Provider

- provider/connector;
- endpoint if applicable;
- credential reference;
- health test;
- data policy summary.

## L2. Models

- default model;
- fast model;
- reasoning model;
- fallback model;
- enabled models;
- cost/context metadata where available.

## L3. Features

Feature-level enable/disable for:

- briefing;
- drafting;
- summaries;
- search;
- record insights;
- triage outside Chatwoot;
- reporting assistance;
- automation assistance;
- agentic actions where approved.

## L4. Tools

- registered tools;
- read/write classification;
- permission requirements;
- confirmation requirements;
- plugin-provided tools;
- connector-provided tools;
- audit state.

## L5. Usage & Limits

- usage summary;
- workspace/user limits;
- cost limits where measurable;
- feature limits;
- retention/logging.

## L6. Guardrails

- sensitive data policy;
- vault restrictions;
- write-action confirmation;
- client data isolation;
- external content/tool policy.

---

# M. Vault

## M1. Policies

- allowed item types;
- default classifications;
- retention;
- expiration;
- download policy;
- copy/reveal policy.

## M2. Step-up Authentication

- required actions;
- step-up methods;
- validity duration;
- reauthentication after risk events.

## M3. Access

- roles permitted to create/share/reveal;
- client access policy;
- temporary access;
- request/approval workflow;
- property/project-scoped access.

## M4. Categories

Credential, legal, commercial, infrastructure, financial, sensitive note, confidential file, and plugin-defined categories.

---

# N. Files

## N1. Storage Provider

Development may use Lovable/Supabase storage. Product architecture must remain provider-compatible.

Settings:

- provider;
- connection health;
- capacity/limits;
- allowed object sizes;
- signed URL behavior;
- public/private defaults.

## N2. Security

- allowed/blocked types;
- malware scanning integration where available;
- executable policy;
- confidential classification;
- download logging where appropriate.

## N3. Retention & Versions

- version retention;
- soft-delete duration;
- purge policy;
- orphan cleanup.

---

# O. Automations

## O1. Defaults

- enabled;
- maximum run duration;
- concurrency;
- default retry policy;
- recursion protection.

## O2. Schedules

- timezone behavior;
- schedule limits;
- missed-run behavior.

## O3. Failures

- retry defaults;
- alert thresholds;
- dead-letter behavior;
- owner/team notification.

## O4. AI Actions

Define whether AI-assisted automation building or AI-executed actions are permitted and under what confirmation/audit policies.

---

# P. Plugins

## P1. Installed

- name;
- version;
- publisher/source;
- status;
- compatibility;
- permissions;
- migrations;
- health;
- update state;
- configuration.

## P2. Sources

- official/bundled source;
- Git-based source where supported;
- uploaded package where supported later;
- trust policy.

## P3. Permissions

Show requested capabilities before enable/install.

## P4. Updates

- available update;
- compatibility;
- migration summary;
- backup requirement;
- rollback information.

## P5. Development

Developer mode, local plugin diagnostics, manifest validation, extension point registry.

---

# Q. Connectors

## Q1. Instances

Connector type may have many instances.

Each instance should expose:

- name;
- provider;
- environment;
- linked organisation/property if scoped;
- auth status;
- health;
- last success;
- last failure;
- rate-limit state if known;
- webhook state;
- version/capabilities.

## Q2. Authentication

Credentials are stored through the approved secret/vault mechanism, not exposed casually in Settings.

## Q3. Health

- connection test;
- last successful call;
- latency where useful;
- auth expiry;
- webhook freshness;
- provider status if known.

## Q4. Events / Failures

- recent connector events;
- failed webhook/event processing;
- retry/replay where permitted;
- correlation ID;
- masked payload diagnostics.

---

# R. API & MCP

## R1. REST/API

- API enabled;
- version information;
- documentation link;
- rate-limit defaults;
- CORS/origin policy where relevant.

## R2. API Tokens

- create;
- label;
- scopes;
- expiry;
- last used;
- allowed IPs optional;
- revoke;
- rotate;
- one-time secret reveal;
- audit.

## R3. Webhooks

- endpoint subscriptions;
- event types;
- secret/signature;
- delivery attempts;
- retries;
- disable;
- replay;
- test delivery.

## R4. MCP

- server enabled;
- endpoint/transport;
- client credentials;
- tool catalogue;
- tool scopes;
- read/write classification;
- confirmation policies;
- audit;
- client setup instructions for Claude, ChatGPT, Codex, OpenClaw/Hermes, and generic MCP clients.

## R5. AI Clients

Human-readable connection cards for supported external AI clients, generated from the current server configuration without leaking secrets.

---

# S. Security

## S1. Authentication

- password login;
- magic link;
- passkey support if introduced;
- OAuth providers;
- client/staff policy differences;
- self-registration rules.

## S2. MFA

- required roles;
- allowed methods;
- grace period;
- recovery codes;
- enforcement status.

## S3. Password Policy

Where password auth exists:

- minimum requirements;
- breached-password checks if supported;
- reset policy;
- lockout/rate limiting.

## S4. Sessions

- session duration;
- inactivity timeout;
- remember-device policy;
- step-up duration;
- revoke on sensitive changes.

## S5. Rate Limits

Domain-specific policies for auth, API, MCP, file access, vault reveal, and expensive actions.

## S6. Security Events

Search/filter/export authorized security events.

## S7. Network/IP Policy

Optional allow/deny policies for privileged staff/API clients where later required.

---

# T. System

## T1. Health

- application health;
- database;
- storage;
- background jobs;
- notification delivery;
- connectors;
- plugins;
- PWA/push service dependencies where relevant.

## T2. Jobs / Queue

- queued;
- running;
- retrying;
- failed;
- dead-letter;
- inspect/retry/cancel with permission.

## T3. Logs

Structured operational logs with masking, filtering, correlation IDs, retention, and permission controls.

## T4. Backups

- backup status;
- last successful backup;
- next scheduled;
- restore documentation/status;
- test-restore record where managed by Re:Solve;
- backup configuration connector/provider where applicable.

## T5. Updates

- current version;
- available version;
- release notes;
- compatibility warnings;
- plugin compatibility;
- migration requirement;
- backup prerequisite;
- update history.

## T6. Feature Flags

- internal/experimental flags;
- owner;
- scope;
- expiration/review date;
- environment restrictions.

## T7. About / Diagnostics

- version/build;
- environment label;
- enabled capabilities;
- diagnostic export with secret masking;
- licenses/acknowledgements where needed.

---

# 8. Settings permissions

Settings permissions must be granular. `Admin` is not sufficient as the only gate.

Examples:

- settings.general.manage;
- users.manage;
- roles.manage;
- portal.settings.manage;
- billing.settings.manage;
- notifications.settings.manage;
- communications.manage;
- ai.settings.manage;
- vault.settings.manage;
- plugins.manage;
- connectors.manage;
- api.manage;
- mcp.manage;
- security.settings.manage;
- system.operations.manage.

High-risk operations may require workspace-owner capability plus step-up authentication.

## 9. Audit requirements

Audit all material settings changes, especially:

- authentication/security;
- permissions/roles;
- billing/payment provider;
- communication destinations/providers;
- AI provider/tools/guardrails;
- vault policy;
- plugin install/enable/update;
- connector credentials/config;
- API/MCP tokens/scopes;
- retention/deletion policy;
- backup/update operations.

Audit entry should contain actor, before/after summary with secret masking, time, source, and correlation/request context.

## 10. Notifications generated by settings changes

Examples:

- user role elevated;
- MFA requirement changed;
- payment provider disconnected;
- WhatsApp session disconnected;
- critical connector auth expiring;
- plugin update failed;
- API/MCP token created;
- vault access policy changed;
- system update completed/failed.

## 11. API and MCP

Settings APIs should exist for machine-manageable configuration, but sensitive areas require stricter scopes and may be read-only through MCP by default.

MCP should never provide blanket `update_settings` access. Expose narrow tools with explicit scopes only when there is a proven use case.

## 12. Responsive behavior

Settings must remain usable on tablet and mobile.

Mobile patterns:

- searchable settings index;
- drill-down section pages;
- sticky save action where appropriate;
- no two-column label/control layout forced into narrow width;
- connector diagnostics readable on mobile;
- high-risk confirmations fit safe-area screens.

## 13. Empty/error/loading states

Every settings section must handle:

- loading;
- no permission;
- feature/plugin not installed;
- connector not configured;
- partial config;
- invalid existing config;
- test failed;
- save failed;
- concurrent modification where relevant;
- stale state;
- offline read-only state.

## 14. Acceptance criteria

Settings is acceptable when:

- every configuration has a clear domain owner;
- high-risk changes are protected and audited;
- provider configuration includes test/health behavior;
- plugin/connector settings extend the control plane without becoming random pages;
- search can locate settings precisely;
- mobile is usable;
- unsupported features clearly show install/configure state;
- configuration status is visible;
- secrets are never casually revealed;
- API/MCP exposure is scoped;
- settings changes do not silently alter existing data without documented behavior.

## 15. Lovable build slices

Do not build all Settings at once.

### Slice A — Settings shell
- settings navigation;
- search;
- section routing;
- configuration health summary;
- responsive mobile settings index.

### Slice B — General
- workspace;
- branding;
- locale;
- currency;
- preview/save behavior.

### Slice C — People & Access
- staff;
- teams;
- roles;
- permission matrix shell;
- sessions.

### Slice D — Notifications
Implement workspace policy/settings after the core notification center exists.

### Slice E — Client Portal
Portal defaults, roles, invitations, navigation policy.

### Slice F onward
Build one domain settings group at a time, only after the corresponding feature domain is specified enough to know what its settings actually control.
