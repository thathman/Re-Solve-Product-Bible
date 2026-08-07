# Client Portal — Files, Secure Vault and Knowledge

## Purpose
Provide three clearly separated client information experiences:
1. ordinary shared Files;
2. explicitly authorized protected Vault Items;
3. reusable client-visible Re:Solve Knowledge.

The UI must make the difference obvious so a client never assumes an ordinary File share has Vault-level protection or that Vault content is searchable like ordinary content.

## Files
Files is for ordinary project, billing, Property, Request and Organisation documents.

Capabilities:
- browse recent/shared/contextual Files;
- filter by Project/Property/category;
- search filename/tags/allowed extracted metadata;
- preview supported formats;
- download permitted version;
- upload where a Request/Client Action/Form allows it;
- see version/source/related record/updated time;
- distinguish client upload, staff share and Document Studio artifact where useful.

### Requested uploads
A client may receive a narrow upload action tied to:
- Request;
- Client Action;
- Project/Deliverable;
- onboarding;
- another approved workflow.

The UI clearly shows what is requested, accepted types/limits, due state and upload outcome.

## Files versus Vault — non-negotiable boundary
A protected confidential document is a Vault Item, not simultaneously an ordinary downloadable File.

If an item is promoted to Vault:
- ordinary Portal File links/downloads disappear/invalidate;
- the protected Vault representation becomes authoritative for access;
- source business-record relationship is preserved;
- Activity/Audit reflect the transition.

Do not show the same confidential document in both ordinary Files and Vault with different permissions.

## Secure Vault
Vault is visually and behaviorally distinct.

Client can only see Items explicitly granted under Organisation/Property/item policy.

Capabilities may include:
- list safe metadata;
- request access;
- reveal/copy authorized credential;
- download protected document;
- see access expiry;
- view linked Property/context;
- revoke/decline own temporary access where workflow supports it.

Every sensitive reveal/copy/download/share/grant/revoke is audited. Step-up may be required. Secret values never enter ordinary Search, Notification body, Àríyá context, Activity text or offline cache.

## Protected commercial documents
A Contract/Proposal/other business record may link to a Vault-protected final document where policy requires confidentiality.

The commercial metadata/status remains in its source domain; Vault governs protected content access. Portal must not provide a parallel ordinary Document Studio/File download path that bypasses Vault.

## Knowledge
Client-visible Re:Solve Knowledge supports:
- spaces/categories;
- search;
- article reading;
- related guidance;
- recently updated;
- Property/Project/Service-scoped guidance;
- freshness/review state where useful.

Visibility is explicit. Linking an Article to an Organisation/Property does not automatically publish it to clients.

Re:Solve Knowledge remains separate from Chatwoot Support Knowledge/Captain.

## Àríyá
Optional Portal Àríyá may search/summarize only authorized client-visible Knowledge and ordinary content permitted by AI data policy.

Generic Àríyá retrieval excludes Vault secret values and staff-only Knowledge/Internal Notes. Protected Vault documents require explicit special policy before any AI processing.

## Search
Portal global Search may include ordinary Files and client-visible Knowledge. Vault appears only as safe metadata under explicit Vault authorization and should normally have its own filtered search rather than generic full-text content indexing.

## Notifications / Attention
Examples:
- requested File due/received;
- File shared/new final version;
- Vault access requested/granted/denied/expiring/revoked;
- credential rotation requiring client action where applicable;
- Knowledge materially updated/subscribed.

Persistent requested-upload/access action may be Attention; Notifications are delivery/history.

## Secure External Access
A non-Portal recipient may upload/download an ordinary approved File or view a document through a narrow expiring grant. This does not normalize guest access to raw Vault secrets.

## API / MCP
Separate capability families for Files, Vault metadata, privileged Vault operations and Knowledge.

Generic Search/MCP/AI never leaks Vault secret content. Downloads reauthorize at request time.

## PWA/mobile
### Files
Mobile picker/camera, progress, retry and preview where safe. Selected ordinary client-safe Files may support controlled offline access if policy permits.

### Knowledge
Selected published client-safe Articles may be cached for offline reading with revocation/freshness considerations.

### Vault
No secret/protected content offline persistence. Protected action requires live authorization/step-up where policy applies.

## Accessibility / Core UI
Files, Vault and Knowledge share Re:Solve Core UI quality but use distinct semantic iconography/status/wording. Sensitive actions require explicit labels such as `Reveal password` or `Download protected contract`, not ambiguous icon-only controls.

## Acceptance criteria
- client can distinguish ordinary Files, protected Vault Items and Knowledge;
- protected document has no ordinary File bypass;
- Vault values never appear in generic Search/Àríyá/MCP/cache/Notifications;
- requested uploads are destination/scoped;
- Knowledge visibility is explicit;
- Chatwoot Support Knowledge remains separate;
- mobile upload/read flows are excellent;
- access revocation invalidates future downloads/retrieval.

## Lovable build slices
1. Files library + requested-upload flow.
2. Knowledge browse/search/article.
3. Vault metadata + permission states.
4. Vault step-up/reveal/download/access requests.
5. promotion/boundary behavior + Secure External Access.
6. mobile/offline/security polish.
