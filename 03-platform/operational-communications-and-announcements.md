# Platform — Communications and Announcements

## Purpose
Communications is Re:Solve's provider-neutral business-communication layer for connected email, outbound operational messages, Shared Inbox/Triage, record-linked communication history, review requests and announcements.

It is not a second live-chat/helpdesk console and not a bulk-marketing platform.

## Canonical records
- Connected Mailbox / Communication Connector mapping;
- Communication Thread;
- Message / Outbound Message;
- Message Template / Template Version;
- Sender Identity;
- Staff HTML Email Signature;
- Delivery Attempt;
- Inbox Triage item/state;
- Review Request;
- Announcement;
- Files/attachments linked through the Files domain.

## Connected mailboxes / Shared Inbox
Re:Solve may connect Gmail/Google Workspace, Microsoft 365 or provider-neutral IMAP/SMTP/API implementations behind Connector contracts.

Mailbox configuration declares:
- provider/Connector instance;
- inbound/outbound capability;
- ownership/sync direction;
- Operating Entity/Brand identity;
- sender/reply-to addresses;
- staff/team eligibility;
- last sync/freshness/health;
- retention/privacy policy.

Provider identifiers and thread/message IDs are preserved so Re:Solve does not guess conversation identity from subject text alone.

## Email composition architecture
Email is rendered from separately configurable layers:

`Universal HTML head/styles -> Operating Entity/Brand header -> Template/body -> Staff personal HTML signature OR Operating Entity/system signature -> Footer/legal content`

### Workspace / Operating Entity
May configure:
- universal HTML head and approved styles;
- header/logo/brand treatment;
- system/automated signature;
- footer;
- legal/company/address/tax content;
- default sender identity;
- locale/formatting.

### Staff profile
Each staff User may configure a sanitized **personal HTML email signature** independently of Workspace/Operating Entity templates and independently of their Document/PDF Signature.

### Template body
Template Version owns subject/body/declared safe variables. Preview/test should render the complete final composition against approved sample/real context before enabling/sending.

Do not allow arbitrary template code/variables to bypass security or inject unsafe HTML.

## Outbound communication
Users/Automations/Ariya may draft/send authorised messages linked to Organisation, Contact, Opportunity, Proposal, Project, Request, Invoice, Property or another approved record.

Send is a controlled action with recipient/identity preview. Automated sends follow template/version, preference, quiet-hour and retry policies.

## Inbound ingestion and threading
For each inbound message Re:Solve should:
1. preserve provider/message/thread identifiers and raw-source reference;
2. identify sender Contact/User where possible;
3. resolve Organisation context without silently merging identity;
4. inspect explicit thread/reply links;
5. relate authorised Property/Project/Proposal/Billing/Support context where evidence exists;
6. process Files/attachments through Files policy;
7. route confidently or place in Inbox Triage.

Unknown senders do not automatically become trusted clients/Portal Users.

## Ariya email intelligence
Ariya may classify inbound email using authorised evidence such as:
- sender/Organisation;
- existing thread;
- Property/Project;
- open Support/Incident;
- commercial/Billing context;
- intent/urgency;
- requested action;
- dates/deadlines;
- attachments.

Examples:
- outage/problem -> attach/create Support case under policy;
- hosting renewal quote request -> Opportunity/Proposal follow-up;
- project answer/approval -> Project context;
- payment-proof attachment -> Billing reconciliation **triage**, never automatic Payment verification from text alone.

### Confidence policy
High-confidence classifications may invoke pre-approved registered routing Actions. Medium/uncertain classification creates Inbox Triage with Ariya recommendation/evidence for one-click human confirmation. Low-confidence/unknown remains unassigned.

Every automated route records why it happened and which evidence/model/run was used.

## Support/live-chat boundary
Canonical Portal live-chat path:
`Client Portal -> Ariya -> Chatwoot -> Ariya -> Client`.

Chatwoot is the human-conversation transport/handoff surface. Re:Solve does not duplicate the Chatwoot agent console.

Email-originated support can create/link Re:Solve Support work and, when required, map/handoff to Chatwoot through controlled integration. Chatwoot Captain remains separate from Ariya.

## Communication timeline
Where authorised, Organisation/Opportunity/Project/Billing/other record workspaces may show linked communication history with channel, direction, sender/recipients, timestamp, subject/summary, Files and delivery/source evidence.

Do not duplicate/store unnecessary protected provider content when a safe reference is sufficient.

## Delivery evidence
Represent only evidence actually supplied:
- queued;
- sent/provider accepted;
- delivered;
- bounced/failed;
- opened/clicked only where provider/privacy policy supports it.

Open/click never proves a human read/comprehended a message.

## Review Requests
A Review Request may be created manually or triggered after configured events such as Project completion, Support resolution, verified full Payment or a follow-up date.

Fields may include Organisation/Contact, related Project/Support/Invoice/Service, destination, requested/reminder dates, message template, clicked timestamp/evidence and completion status/evidence.

Destinations may include Google, Facebook, Clutch, Trustpilot or custom URLs.

Re:Solve never claims a public review was posted without verifiable evidence. Ariya can draft a personalised request from permitted context.

## Announcements
Controlled operational broadcasts for staff/client audiences: maintenance, service notice, portal announcement, policy/process change, holiday/support-hours notice, incident update.

Announcements are not marketing campaigns. Sophisticated newsletters/campaigns remain specialist Connector/Plugin territory.

## Preferences / consent
Operational/security/billing communications distinguish mandatory service communications from optional preferences and marketing consent. Recipient selection respects Organisation designations and per-user preferences where applicable.

## Attention / Tasks
Examples:
- client email unanswered beyond policy threshold;
- mailbox sync/auth degraded;
- delivery repeatedly failing;
- Inbox Triage backlog;
- review request due for follow-up.

Ariya may Watch these conditions and recommend/create Tasks through policy.

## Security / privacy
- mailbox credentials remain in Connector/Vault boundaries;
- raw provider payloads are redacted/retained deliberately;
- sender identity and recipients are permission-scoped;
- email HTML/signatures are sanitized;
- hidden client/record context cannot leak through search/timeline;
- public unsubscribe/consent is separate from mandatory operational notice rules.

## API / MCP
Expose scoped thread/message/template/review metadata and registered send/triage Actions. No arbitrary mailbox credential access.

## Acceptance criteria
- inbound/outbound email is first-class and record-linked;
- threading uses provider identifiers, not subject guessing;
- universal head/header/body/signature/footer are independently configurable;
- staff HTML signatures remain separate from entity/system and PDF signatures;
- Ariya can classify/reroute with evidence and confidence policy;
- uncertain messages have safe Inbox Triage;
- inbound email cannot fabricate Payment truth;
- Chatwoot remains the live-chat human handoff surface;
- review completion is not fabricated;
- provider delivery evidence is represented honestly;
- marketing suite scope is excluded.

## Build slices
1. sender identities/templates/email composition + staff HTML signature.
2. outbound email/delivery evidence.
3. Connected Mailbox/inbound sync/threading.
4. Organisation/record linking + Shared Inbox/Triage.
5. Ariya classification/routing policies.
6. Review Requests/Announcements/preferences.
7. Chatwoot handoff integration/degraded-state polish.
