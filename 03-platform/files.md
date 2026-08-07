# Files Platform

## Purpose
Files is the shared document and attachment layer for Re:Solve. It supports normal operational files across organisations, contacts, properties, projects, billing, sales, knowledge, forms, and portal experiences. Sensitive material belongs in Secure Vault when confidentiality requirements exceed normal file access.

## Core records
File, File Version, Folder, File Link, Share, Upload Session, Retention Policy, File Activity, Storage Provider Reference.

## Principles
- one file may be linked to multiple business records without unnecessary duplication
- storage implementation is provider-abstracted
- permissions are inherited from owning/linked records unless explicitly overridden
- file metadata and content permissions are independently enforceable where necessary
- file versioning must preserve history for important documents
- confidential content should be routed to Secure Vault rather than pretending normal file storage is a vault

## Main surfaces
Admin:
- All Files
- Recent
- Shared
- By Client
- By Property
- By Project
- Storage / Health

Client Portal:
- Files
- Shared With Me
- Project Files
- Property Files
- Billing Documents

## File metadata
Name, extension/type, MIME, size, owner, organisation, property, project, folder, linked records, uploaded by, created/updated, version, description, tags, visibility, client visibility, retention class, checksum, storage provider, scan status.

## Upload flow
1. user selects/captures file
2. validate type/size/policy
3. create upload session
4. upload to storage provider
5. malware/security scanning where configured
6. finalize metadata
7. link to requested record
8. emit audit/activity/notification events as needed

Partial/failed uploads must be recoverable or cleanly abandoned.

## Versions
Important files can create new versions while preserving stable logical identity. Version history shows uploader, timestamp, change note, size/checksum, and current status.

## Sharing
Internal sharing normally follows record permissions. External/client sharing supports explicit audience, expiry, download permission, and revoke. Public anonymous links are disabled by default and require explicit system policy.

## Search and organization
Search by filename, tags, linked client/property/project, file type, uploader, date, and permitted extracted metadata. Full-text indexing is optional and must respect access controls.

## Retention
Retention policies may depend on file category, source module, client agreement, or legal/operational needs. Deletion can be soft-delete, scheduled purge, or protected hold. Vault retention is governed separately.

## Permissions
files.read, files.upload, files.manage, files.delete, files.share, files.versions.manage, files.retention.manage, files.storage.manage. Object-level authorization still applies.

## Notifications
Only meaningful events: client file shared, requested file uploaded, approval-related file replaced, share expiring, malware/scan failure, storage failure. Avoid notifying on routine internal uploads.

## Automations
- form submission attachment → link to target record
- deliverable approved → mark selected version final
- project completed → apply archival policy
- file requested from client → notify/remind until received
- storage/scan failure → operational alert

## API
Expose metadata, authorized upload/download, links, versions, sharing, and search. Downloads must verify permissions at request time. Large uploads should use resumable/direct provider mechanisms where supported.

## MCP
Candidates: search_files, list_files_for_project, list_files_for_property, get_file_metadata, request_file_from_client. Raw file retrieval is permission-gated and should use controlled resource access rather than embedding unrestricted binary content into tool responses.

## PWA/mobile
Support camera/gallery/file picker, upload progress, retry, mobile previews for common types, and safe share actions. Do not offline-cache confidential or permission-sensitive files by default. Clearly show when a file requires connectivity.

## Acceptance criteria
- links do not bypass source-record permissions
- revoking client access invalidates future downloads
- version history remains intact
- failed upload does not create misleading complete file record
- sensitive files can be explicitly moved/routed into Secure Vault
- storage provider outages display degraded state without losing metadata truth

## Lovable build slices
1. shared file model + upload/list/download
2. record linking + folders/tags
3. versions + client sharing
4. portal files
5. retention, scan states, provider health
