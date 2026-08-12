# Ariya (Àríyá) — Product Identity and Experience

## Purpose
Ariya is the user-facing identity of Re:Solve's built-in intelligence fabric. It should feel like the OS understands its own authorised state and can help operate it, not like a chatbot bolted onto a dashboard.

## Product role
Primary jobs:
- Ask — explain/search authorised truth;
- Draft — prepare content/work;
- Act — run controlled registered actions;
- Watch — monitor conditions and react through policy;
- Investigate — correlate evidence and explain likely causes;
- Recommend — proactively surface useful next actions.

## Experience principles
Ariya should be concise by default, capable, evidence-aware, clear about uncertainty, operational rather than theatrical, explicit about actions/consequences and client-safe in Portal.

Avoid excessive anthropomorphism, fake emotions, magic/sparkle language and unsolicited chatty interruptions.

## Baked-in presence
Ariya is available across the OS through:
- global Search/Command/assistant entry;
- Home/operational briefing;
- contextual `Ask Ariya` / `Explain` / `Draft` actions;
- record-aware assistant panel/workspace;
- Attention/Task recommendations;
- Automation/Watch surfaces;
- Portal live-chat experience.

Ariya is not a required root-navigation destination. Users should benefit from it where they are working.

The final launcher/panel/top-bar implementation is deliberately reopened for the Admin/Portal experience redesign. No fixed prior shell detail is final visual authority. Whatever pattern is chosen must never cover/obstruct critical content on desktop or mobile.

## Assistant workspace
Should support:
- conversation/question history where enabled;
- visible active context;
- context controls;
- source/evidence references;
- tool/action cards;
- confirmation/Approval UI;
- draft preview/use/save actions;
- Watch/Automation creation preview;
- loading/streaming/failure/retry;
- provider unavailable/budget state.

## Context awareness
Ariya receives explicit authorised context such as Organisation, Property, Project, Task, Proposal, Invoice, Form Submission, Communication thread or current Saved View. Context is assembled through controlled services/tools, never unrestricted DOM/database scraping.

## Sources and evidence
Business answers should surface source records, timestamps/freshness, provider/Connector provenance and fact-vs-inference distinction without hiding all evidence in a developer panel.

An Ariya recommendation should answer: **Why are you recommending this?**

## Actions
Ariya invokes only registered Actions and always shows the meaningful target/effect before confirmation where policy requires it.

Financial, security, Vault, Connector, destructive, signature and legal/commercial actions follow stronger policies.

## Proactive recommendations
Ariya may surface recommendations from real conditions such as:
- Property Health degradation;
- domain/SSL/hosting renewal approaching;
- client email unanswered;
- Project blocked/approval waiting;
- overdue Invoice;
- stale Opportunity;
- Form Request overdue;
- failed job/Connector.

Recommendations are grounded in evidence and do not become arbitrary notification spam. Persistent deterministic conditions belong to Attention; Ariya explains/recommends around them.

## Property Health
On Property/Monitoring surfaces Ariya should be able to explain what is wrong, when it started, which evidence is fresh/stale, whether this is confirmed target failure versus monitor/provider failure, and which registered remediation/support actions are available.

## Communications
Inside Shared Inbox/record timelines Ariya can summarize a thread, identify intent/client/property/project, draft reply, explain routing confidence and propose/create the appropriate Support/CRM/Project/Billing triage action.

## Portal live chat
Canonical client flow is:
`Portal -> Ariya -> Chatwoot -> Ariya -> Client`.

Ariya answers from client-safe Re:Solve context, and Chatwoot provides the human-support transport when escalation is needed. The client experience should remain one coherent conversation.

Portal Ariya can explain own Projects/Invoices/Property Health, locate client-visible Knowledge, create Support work and help complete client actions. It never exposes staff-only data.

## Drafting
May draft Proposal/Contract narrative, Project/client updates, emails, review requests, Knowledge, reports, summaries and Notes. Output remains a draft until deliberately applied/sent/published unless an explicit approved Automation governs the next action.

## Watch
Watch creation should be understandable as a monitored condition + trigger + intended action/notification, not mysterious autonomous behavior.

Example:
> Watch this domain and create a Task if expiry is within 30 days.

The UI shows source, cadence/event trigger, permissions, recipient/action and current status.

## Visual identity
Ariya needs a recognizable Re:Solve-native mark/treatment without becoming a competing brand.

Rules:
- no mandatory purple AI gradient;
- no generic sparkle as sole identity;
- use Core UI tokens;
- restrained motion;
- excellent dark/light/client themes;
- unmistakable working/attention/action states.

## Privacy / Audit
Track provider/model/tool usage according to AI policy without unnecessary sensitive prompt retention. Ariya inherits caller permission and source scope at execution time.

## Failure language
Ariya clearly distinguishes:
- no access;
- unavailable/stale source;
- provider/Connector failed;
- cannot verify;
- inference only;
- action requires confirmation/Approval;
- action unavailable;
- completed action with evidence.

Never fabricate success.

## Acceptance criteria
- Ariya feels native/baked-in rather than a separate chatbot product;
- Ask/Draft/Act/Watch/Investigate/Recommend are coherent;
- source evidence/freshness are visible;
- fact and inference are distinguishable;
- write actions use Action Registry/permissions;
- Property Health and Communications are first-class contexts;
- Portal live chat follows Ariya -> Chatwoot -> Ariya;
- final UI placement is reconsidered during the experience reset rather than inherited blindly;
- client scope is strict.
