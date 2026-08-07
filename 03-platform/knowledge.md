# Re:Solve Knowledge Platform

## Purpose
Knowledge is Re:Solve's internal and client-operational knowledge system. It supports SOPs, project procedures, service documentation, client-only guidance, property documentation, reusable templates, and AI retrieval inside Re:Solve.

It is separate from Chatwoot Knowledge, which remains the support knowledge system for managed client support and Chatwoot AI.

## Core records
Knowledge Space, Article, Category, Article Version, Attachment, Source, Visibility Rule, Property Scope, Organisation Scope, Review Record, Suggestion, Embedding/Index Reference.

## Knowledge spaces
Initial space types:
- Internal Operations
- Service Delivery
- Client Knowledge
- Property Knowledge
- Project Knowledge
- Policies & SOPs
- Templates & Playbooks

Spaces define audience, owners, editors, review cadence, indexing behavior, and whether articles may surface in Portal or Re:Solve AI.

## Article lifecycle
Draft → Review → Published → Needs Review → Archived.

Every publication creates a version. Significant edits preserve history and author/reviewer information.

## Article structure
Title, summary, body, category, tags, owner, authors, reviewers, related organisation/property/project/service, visibility, status, version, effective date, review date, sources, attachments, related articles, AI indexing eligibility.

## Visibility
Visibility is explicit and composable:
- staff only
- selected teams/roles
- selected organisation
- selected properties
- selected project participants
- client portal users with required role

No article becomes client-visible merely because it is linked to a client record.

## Search
Search across title, body, tags, categories, related records, and approved indexed content. Results must be permission-filtered before ranking/display.

## Re:Solve AI
Published and authorized knowledge can feed Re:Solve AI retrieval. AI retrieval must preserve caller permissions and article visibility. Draft/internal content must never be exposed to portal users through AI.

## Chatwoot separation
Chatwoot support knowledge may be linked or referenced but is not mirrored wholesale into Re:Solve by default. A future connector may sync approved articles in either direction through deliberate workflows and version rules.

## Knowledge suggestions
Users may suggest new articles or corrections from support incidents, project retrospectives, repeated questions, failed automations, or manual submission. Suggestions remain separate from published content until reviewed.

## Reviews and freshness
Articles can have owner, review frequency, next review date, stale status, and review history. Overdue reviews surface in My Work and notifications when policy requires.

## Templates/playbooks
Reusable process content may define checklists, guidance, or links to project templates/automations without becoming executable logic itself.

## Permissions
knowledge.read, knowledge.create, knowledge.edit, knowledge.review, knowledge.publish, knowledge.archive, knowledge.client_publish, knowledge.settings.manage, knowledge.ai_index.manage.

## Notifications
review requested, review overdue, article published, article materially updated for subscribed users, client article published, stale critical SOP, suggestion assigned.

## Automations
- article review date reached → My Work item/notification
- project closeout → suggest lessons-learned article
- repeated incident/category threshold → suggest knowledge article
- article archived → remove from AI retrieval index
- client/property access revoked → article access follows scope automatically

## API
Expose spaces, articles, versions, search, suggestions, review states, and visibility-filtered retrieval. Publishing and client visibility changes require stronger permissions and audit.

## MCP
Candidates: search_knowledge, get_article, list_articles_for_property, list_stale_articles, suggest_knowledge_article, draft_article_from_authorized_context. MCP retrieval must apply identical visibility filters as the UI/API.

## PWA/mobile
Knowledge must be highly readable on mobile. Selected non-sensitive published articles may be cached for offline reading if policy allows; permissions and revocations must invalidate future access. Editing on mobile supports drafts but complex publishing workflows may optimize for larger screens.

## Acceptance criteria
- Chatwoot Knowledge and Re:Solve Knowledge remain separate systems
- search and AI retrieval cannot bypass visibility
- client-visible publication requires explicit scope
- version history is preserved
- archived content is removed from active AI retrieval
- stale critical knowledge can surface operationally without spamming users

## Lovable build slices
1. spaces + article list/editor + versioning
2. permissions/visibility + search
3. review workflow + freshness
4. portal knowledge experience
5. AI retrieval/index controls
6. suggestions + optional Chatwoot sync connector later
