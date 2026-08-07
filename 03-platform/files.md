# Files Platform

## Purpose
Files is Re:Solve's ordinary document/attachment layer across Organisations, Contacts, Properties, Projects, Billing, Sales, Requests, Knowledge, Forms and Portal.

Secure Vault is a separate protected domain. A protected confidential document must **not** remain available through a parallel ordinary File access path.

## Core records
File, File Version, Folder, File Link, File Share, Upload Session, Retention Policy, File Activity and Storage Provider Reference.

## Storage relationship to Vault
Files and Vault may use the same provider-neutral storage infrastructure/object storage service, but they have different domain identities and authorization contracts.

Conceptually:
```text
Storage Provider / Binary Object
      ├── ordinary File domain metadata/access
      └── protected Vault Item metadata/access
```

If an ordinary File is promoted/moved into Vault:
- create/convert to the protected Vault representation;
- preserve provenance/link to originating business record where useful;
- remove/invalidate ordinary File access paths;
- update search/share links;
- Audit the transition.

Do not model the same confidential binary as both an ordinary downloadable File and a Vault Item.

## Principles
- provider-abstracted storage;
- stable logical File identity with versions where useful;
- links to multiple records without unnecessary binary duplication;
- object-level authorization on metadata/content/share;
- client visibility explicit;
- upload/finalization truth separate from partial upload;
- scan/processing state truthful;
- protected content routes to Vault;
- downloaded content is authorized at request time.

## Main surfaces
Admin:
- All Files
- Recent
- Shared
- By Client
- By Property
- By Project
- Requested Uploads
- Storage / Health
- Trash where enabled

Portal:
- Files
- Shared With Me
- Project Files
- Property Files
- Billing/Documents
- Requested Uploads

Vault appears separately only for authorized protected items.

## File metadata
May include:
- human/file id;
- name/extension/MIME/size;
- owner;
- Organisation/Property/Project/Request context;
- folder;
- linked records;
- uploaded by;
- created/updated;
- version;
- description/tags;
- visibility/client visibility;
- retention class;
- checksum;
- storage provider reference;
- scan/processing state;
- source/provenance;
- extracted metadata/indexing eligibility.

## Upload lifecycle
1. authorize intended destination/context;
2. select/capture File;
3. validate type/size/policy;
4. create Upload Session;
5. upload via provider-safe mechanism;
6. verify checksum/finalization;
7. scan/process where configured;
8. finalize File metadata;
9. link to source record;
10. emit Activity/Audit/Notification as policy requires.

Failed/abandoned uploads must not look like complete Files.

## Requested uploads
Requests/Client Actions/Forms may ask a client or guest to upload a specific File.

The upload grant must constrain:
- destination record;
- recipient/session;
- allowed types/size;
- expiry;
- number of uploads;
- client visibility;
- scan policy.

Secure External Access can provide the narrow guest upload experience.

## Versions
Version history shows uploader, timestamp, change note, size/checksum, source and current/final state.

A stable logical File can have versions while client/download links resolve only to authorized/current or specifically shared versions.

Document Studio generated artifacts may reference rendered versions/snapshots but business document status remains owned by its business record.

## Sharing
Internal sharing normally follows record scope.

External/client File Share may define:
- recipient/audience;
- expiry;
- download/view permission;
- version;
- revoke;
- optional Secure External Access wrapper.

Anonymous public links are disabled by default.

## Search / indexing
Search filename, tags, permitted metadata, related Organisation/Property/Project/Request and optional extracted text.

Indexing happens only for declared safe File classes and respects current authorization before result display.

Vault Items/content are excluded from ordinary File full-text index.

## Retention / Trash
Policies may support Archive, soft-delete/Trash, restore, scheduled purge and protected hold.

Purge honors linked-record constraints/privacy/retention policy. Vault has separate retention/access rules.

## Permissions
Canonical examples:
- `files.read`
- `files.upload`
- `files.manage`
- `files.delete`
- `files.share`
- `files.versions.manage`
- `files.retention.manage`
- `files.storage.manage`

Record-level source scope still applies.

## Attention / Notifications
Meaningful events:
- requested upload overdue/completed;
- client File shared;
- share expiring;
- approval-related version replaced;
- scan/processing failed;
- storage unavailable;
- orphaned/invalid File Data Quality issue.

Routine internal uploads should not spam users.

## Automations
Examples:
- Form Submission File -> link to resulting Request/record;
- Deliverable approved -> mark chosen File Version final;
- Project completed -> archival/retention policy;
- requested File overdue -> Reminder/Attention;
- scan/storage failure -> operational Attention;
- File promoted to Vault -> remove ordinary share/access.

## API / MCP / Àríyá
Expose permitted metadata, upload/download, links, versions, sharing/search and requested-upload operations.

Raw downloads reauthorize at request time and may use short-lived signed URLs/secure streaming.

MCP candidates:
- search_files
- list_files_for_project
- list_files_for_property
- get_file_metadata
- request_file_from_client

Raw binary retrieval is tightly permissioned. Àríyá may summarize authorized ordinary document content under data policy; Vault content follows Vault AI restrictions.

## PWA/mobile
Support camera/gallery/file picker, progress, retry, mobile preview and safe share actions.

Do not offline-cache confidential/sensitive Files by default. Files requiring network show a deliberate online-required state.

## Acceptance criteria
- ordinary File links cannot bypass source-record authorization;
- revoking access invalidates future download;
- version history remains stable;
- failed upload cannot become a misleading complete File;
- promotion to Vault removes ordinary access path;
- Vault protected documents are not ordinary File search results;
- provider outage preserves File metadata truth with degraded state;
- guest upload grants are narrow/expiring.

## Lovable build slices
1. File model + upload/list/download.
2. linking/folders/tags + requested uploads.
3. versions + client sharing/Secure External Access.
4. Portal Files.
5. Trash/retention/scan/provider health.
6. Vault promotion boundary + search/indexing controls.
