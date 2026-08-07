# Platform — Global Search & Activity

## Purpose
Make Re:Solve navigable at OS scale. Search finds things; Activity explains what changed.

## Global Search
Accessible from persistent search/command entry and keyboard shortcut.

Search domains:
- organisations
- contacts
- properties
- projects
- tasks/client actions
- opportunities
- services
- invoices/payments
- files
- knowledge
- support references
- notifications
- Vault metadata only when permitted
- plugin-provided searchable records

## Search behavior
Results are grouped by type, ranked by relevance and optionally recency/context. Support exact identifiers, aliases, domains, invoice numbers and natural-language-like keywords where practical. Filters include type, client, property, owner and status.

Search must never index or return content the caller cannot read. Secret values and confidential Vault content are excluded from generic indexing.

## Command palette
Beyond navigation, the palette may expose safe actions such as create record, open recent item, switch organisation context, start timer, create task or launch a permitted automation. Destructive/high-risk actions should not be one-keystroke accidents.

## Activity
Activity is a normalized event timeline, not a copy of the audit log.

Examples:
- project updated
- deliverable approved
- invoice issued/paid
- property incident opened/resolved
- client action completed
- file shared
- support conversation linked
- Vault access granted
- service renewed

Activity may be scoped to system, organisation, property, project, contact and user. Internal-only activity is not exposed in the client portal.

## Audit distinction
Activity answers “what happened in the business?” Audit answers “who performed or attempted a sensitive/system action, with evidence?” Some events appear in both with different detail.

## Notifications distinction
Notifications are recipient-specific attention. Activity is durable chronology. An activity event may cause zero, one or many notifications.

## API / MCP
Search API is scope-aware and typed. MCP search tools should call this curated search layer instead of unrestricted DB search. Activity API supports scoped timelines and pagination.

## PWA/mobile
Command search works well on phone and desktop. Recent/search history may be cached locally without sensitive content. Activity cards collapse elegantly on mobile.

## Lovable build slices
1. Search command UI with demo index.
2. Typed results/filtering/navigation.
3. Scoped activity timeline.
4. Contextual activity on records.
5. Plugin search providers, MCP exposure and mobile polish.