# Platform — Global Search, Command and Activity

## Purpose
Make Re:Solve easy to navigate at OS scale without bloating the Sidebar. Search finds records/content; Command invokes navigation/registered actions; Activity explains meaningful business chronology.

## Global Search
Accessible from the strong persistent TopBar Search/Command entry and keyboard shortcut.

Search domains may include:
- Organisations / Contacts;
- Properties;
- Projects / Tasks / Client Actions;
- Requests;
- Opportunities / Services;
- Proposals / Estimates / Contracts / document metadata;
- Invoices / Payments / Receipts;
- Renewal Obligations / Incidents;
- Files;
- Re:Solve Knowledge;
- safe Support references;
- Notifications;
- Vault metadata only when permitted;
- plugin-provided records.

## Search behavior
Results are typed/grouped and can rank by relevance, current context, recency/favorite and exact match.

Support useful identifiers such as:
- human references;
- Organisation/Property names;
- domain/URL;
- Invoice/Project/Request/Incident numbers;
- aliases/migrated references;
- approved metadata/content terms.

Filters may include type, Organisation, Property, Project, owner, status and date.

## Authorization / privacy
Search authorization happens before results are surfaced/ranked.

Never index/return:
- inaccessible record existence/count;
- raw Vault secret values;
- hidden client/internal Notes;
- provider credentials;
- private external-calendar details outside granted scope;
- protected document content outside its access policy.

Search history/recents store only safe metadata.

## Source and freshness
Synced/derived results may show source/freshness when it affects interpretation, for example a stale external Support summary or Property connector state.

## Search and Àríyá
Search is deterministic record/content retrieval. Àríyá can consume curated Search tools to synthesize answers, but does not replace Search indexing/permission logic.

A user should be able to search directly without asking AI.

## Command Palette
Command combines:
- navigation;
- record search;
- recent records;
- favorites/pinned records;
- Quick Create;
- registered Actions relevant to current context;
- Saved Views;
- Àríyá entry;
- plugin-contributed approved commands.

Examples:
- Create Request
- Create Project/Task
- Create Opportunity
- Draft Invoice
- Add Property
- Create Reminder
- Open Renewal Desk
- Open current Organisation
- Run a permitted Automation/Action

There is **no start-timer/Timesheet command**.

## Action Registry relationship
Commands that mutate state map to `03-platform/action-registry.md`.

The palette does not invent authorization/confirmation behavior. Risk class, confirmation, step-up and approval come from the registered Action and are checked at execution time.

High-impact actions must not become accidental one-keystroke mutations.

## Favorites / Recents / Saved Views
The command/search experience is a primary way to reach:
- favorites/pinned records;
- recent records;
- personal/team/shared Saved Views.

These improve navigation without adding more permanent Sidebar items and never grant access.

## Activity
Activity is a normalized human-readable business timeline, not a copy of Audit.

Examples:
- Project/Milestone/Deliverable change;
- Request submitted/triaged/completed;
- Proposal accepted;
- Contract executed;
- Invoice issued/Paid;
- Property Posture/Incident transition;
- Renewal completed;
- File shared;
- Support reference linked;
- Vault access approved/revoked;
- client onboarding step completed;
- operational communication recorded;
- Comment/Mention where appropriate.

Activity may be scoped to Workspace, Organisation, Contact, Property, Project, Request, commercial record and other first-class context.

## Collaboration distinction
Comments/Internal Notes/Mentions/Following use the Collaboration platform. Important Collaboration actions may appear in Activity, but Activity is not a discussion system.

## Audit distinction
Activity = useful narrative chronology.
Audit = append-only accountability/security evidence.

Some consequential actions produce both at different detail/sensitivity.

## Notification / Attention distinction
Notification = recipient awareness/delivery.
Attention = unresolved actionable condition.
Activity = chronology.

An event can generate any combination according to product policy without these records becoming interchangeable.

## Activity rendering
Each item should provide as applicable:
- semantic event icon/type;
- concise human language;
- actor;
- target/source link;
- Organisation/Property context;
- timestamp;
- safe summarized change;
- client/internal visibility;
- provenance/source label only when useful.

Avoid rendering every low-level field save as noisy Activity.

## Search providers / plugins
Plugins may register typed searchable resources, fields and commands through approved contracts.

They must declare permissions, result rendering, route/deep link and indexing sensitivity. Plugin search cannot bypass core authorization.

## API / MCP / Àríyá
Search API is typed/scope-aware with pagination/filtering.
MCP uses curated Search and Activity tools rather than unrestricted DB search.
Àríyá uses the same permission-filtered sources and registered Actions.

Potential tools:
- search_records
- search_knowledge
- get_recent_records
- get_record_activity
- list_saved_views

## PWA/mobile
Search/Command is excellent on phone and desktop. Mobile uses touch-friendly grouped results and quick return to recent/favorite destinations. Safe recent metadata may be cached; protected content is not.

Activity rows/cards recompose cleanly on mobile.

## Accessibility
Search/Command supports keyboard navigation, screen-reader result grouping/selection and visible focus. Activity changes are understandable without color alone.

## Acceptance criteria
- Search reduces navigation complexity rather than creating another module tree;
- records/content are permission-filtered before display;
- Vault/hidden Notes/protected content cannot leak;
- mutations use Action Registry;
- Favorites/Recents/Saved Views improve discoverability without granting access;
- Activity/Collaboration/Audit/Attention/Notifications remain distinct;
- no Timesheet/timer command exists;
- mobile Search/Command is first-class.

## Lovable build slices
1. Search/Command Core UI with fictional index, recents/favorites.
2. typed results/filtering/navigation + Saved Views.
3. registered Quick Create/low-risk Actions.
4. scoped Activity timeline + contextual record Activity.
5. plugin providers + API/MCP/Àríyá integration + mobile polish.
