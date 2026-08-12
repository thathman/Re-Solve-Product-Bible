# Platform — First-Run Setup and Installation

## Purpose
First-run setup/installation is a built-in product capability. A fresh Re:Solve deployment should be able to verify prerequisites, bootstrap the first Owner securely, configure a usable Workspace/Operating Entity and lock the installer without requiring operators to hand-edit business state.

This is separate from ordinary Settings and separate from deployment documentation.

## Goals
- make self-hosted installation understandable and verifiable;
- fail safely when infrastructure/configuration is incomplete;
- avoid half-initialized production state;
- securely create the first Owner/Admin;
- establish Workspace/Operating Entity/commercial identity;
- validate core dependencies before declaring ready;
- lock bootstrap after successful setup;
- hand ongoing health/maintenance to System Operations.

## Setup state
Suggested installation state:
- `UNINITIALIZED`;
- `IN_PROGRESS`;
- `READY_TO_LOCK`;
- `LOCKED`;
- `RECOVERY_REQUIRED` only through a separately authenticated recovery process, never an ordinary browser toggle.

A normal application route must never infer `UNINITIALIZED` merely because a query failed.

## Entry/security boundary
`/setup` is available only when server-authoritative installation state allows it and appropriate bootstrap proof is presented where required.

Bootstrap token/secret is server-only, high entropy, one-time/rotatable and never stored in browser analytics/logs.

After `LOCKED`, `/setup` may show a safe “already configured” state or redirect to System/Health but **must not create another Owner or reset security**.

There is no public registration path.

## Step 1 — System Check
Verify and display truthful status/freshness for:
- Re:Solve version/build;
- supported runtime/platform;
- required environment variables without exposing secret values;
- database/Supabase connectivity;
- migration/schema version and pending migrations;
- auth service readiness;
- storage/files availability;
- public/base URL;
- HTTPS/security expectations;
- queue/job worker/runtime;
- Monitoring Worker/probe readiness where required now or marked optional;
- health endpoint;
- background schedule/heartbeat;
- email prerequisites if email is required to finish activation;
- backup destination/readiness where configured.

States distinguish pass, warning/optional, fail/blocking, unknown and skipped-by-policy.

## Step 2 — Security Bootstrap
Create/verify the first Owner/Admin Human User.

Requirements:
- server-authoritative actor creation;
- strong credential/invite/auth flow appropriate to deployment;
- no caller-controlled role escalation;
- explicit Owner capability assignment;
- MFA/passkey setup can be required or completed during/after onboarding according to policy;
- bootstrap token invalidated/retired after use;
- Audit/install evidence recorded without secrets.

## Step 3 — Workspace
Collect:
- Workspace name/code;
- timezone;
- locale/language;
- date/number formats;
- base/enabled currencies;
- default operational preferences that are truly global.

## Step 4 — Operating Entity / Brand
Collect:
- legal/trading name;
- address/contact details;
- registration/tax identifiers where relevant;
- base/default currency;
- logo/brand assets;
- email/document identity;
- default remittance/billing identity;
- default document signatory configuration or explicit “configure before issue” blocker.

## Step 5 — Commercial defaults
Configure or consciously defer:
- Proposal numbering/prefix;
- Invoice numbering/prefix;
- Receipt/Credit numbering;
- payment terms;
- tax mode/definitions where known;
- default Proposal validity;
- default pricing units including duration units;
- Service Catalogue starter items/import where helpful;
- late-fee/Adjustment defaults only when owner explicitly configures them.

Do not invent tax/legal assumptions.

## Step 6 — Communications / Email
Configure provider-neutral email capability:
- Connected Mailbox or outbound provider;
- sender identity/reply-to;
- Operating Entity header/footer/system signature;
- send test message;
- receive/sync test where inbound mail is enabled;
- queue/retry health.

Staff personal HTML signatures are configured in Staff profiles, not copied into Workspace defaults.

Email may be skippable only when the resulting limitations are clearly shown.

## Step 7 — Documents / Signatures / Storage
Verify:
- File storage;
- generated-document storage;
- upload limits/policy;
- Operating Entity PDF issuer-signature rule;
- document hash/verification capability;
- backup policy/destination if available;
- storage health/test object where safe.

If final PDFs cannot be signed, commercial document issue should remain disabled/attention-required rather than silently issue unsigned documents.

## Step 8 — Optional Integrations
Offer skippable setup for relevant Connectors such as:
- payment provider;
- calendar;
- Chatwoot;
- Cloudflare;
- AI provider for Ariya;
- WhatsApp/other communications;
- storage/provider integrations;
- webhooks/API/MCP.

Skipping optional integration must not prevent core app use unless the operator explicitly enabled a feature that depends on it.

## Step 9 — Import / migration
Optional guided import for Organisations, Contacts, Leads/Opportunities, Properties and Service Catalogue/price data.

Imports use the shared Import/Data Quality engine with dry-run, mapping, duplicate review, rollback/reconciliation and provenance.

Do not seed synthetic client/business records into production just to make setup look complete.

## Step 10 — Readiness review
Show one truthful readiness summary such as:

- Database: ready;
- Migrations: current;
- Auth/Owner: ready;
- Storage: ready;
- HTTPS/base URL: ready;
- Jobs/queue: ready;
- Email: ready / intentionally skipped;
- Document signing: ready;
- Backups: warning if not configured/tested;
- Ariya: configured / optional;
- Chatwoot: configured / optional;
- Monitoring Worker: ready / optional current stage.

The operator sees blockers, warnings and consequences before lock.

## Lock Setup
`Lock Setup` is a high-risk registered action requiring current bootstrap/Owner authority and a final confirmation.

On lock:
- installation state becomes `LOCKED`;
- bootstrap token/one-time path is invalidated;
- initial configuration version/timestamp/actor is recorded;
- normal login/Admin becomes the control path;
- missing optional items become Settings/System Attention rather than reopening the installer.

## Recovery
Recovery from lost Owner/access or corrupted setup is a separate documented secure recovery procedure/CLI/server operation with explicit proof, Audit and safeguards. It is not “unlock setup” from an unauthenticated webpage.

## Ariya in setup
When an AI provider is available, Ariya may explain checks, configuration consequences and troubleshooting. It cannot manufacture a pass, reveal secrets, bypass bootstrap controls, grant itself/another Principal Owner authority or lock setup without the registered action.

Setup remains fully operable without Ariya.

## System Operations after installation
After lock, ongoing status belongs in System Operations:
- health;
- jobs/queues;
- Monitoring workers;
- logs;
- storage;
- delivery;
- backups/restore tests;
- updates/migrations;
- Connector/Plugin health;
- Ariya provider health.

## Self-host / portability
Setup must not assume a single hosting vendor. Provider-specific deployment helpers remain outside the business/domain model. Health checks consume provider-neutral contracts where possible.

## Responsive/accessibility
Setup must be usable on common laptop/tablet widths and remain readable on phone for emergency/self-host operations. Use clear step state, error summary, keyboard/focus behavior and no color-only pass/fail meaning.

## Acceptance criteria
- fresh install can reach a deterministic setup state;
- missing prerequisites fail truthfully and safely;
- first Owner bootstrap is server-authoritative;
- setup cannot be silently reopened after lock;
- business defaults are explicit rather than guessed;
- email/storage/document-signing readiness can be tested;
- unsigned final-PDF configuration blocks issue rather than weakening the signed-document rule;
- optional connectors are genuinely optional;
- imports use Data Quality/provenance;
- final readiness clearly separates blockers/warnings/optional items;
- ongoing operations move to System Health;
- no public registration, HR or CMS feature is introduced.

## Build slices
1. installation-state/bootstrap boundary + System Check.
2. first Owner + Workspace/Operating Entity.
3. commercial/email/storage/document-signing setup.
4. optional Connector setup + tests.
5. import/data-quality entry.
6. readiness/Lock Setup + System Operations handoff.
7. recovery documentation/diagnostics/responsive-accessibility review.
