# Privacy, Consent and Data Rights

## Purpose
Re:Solve stores client, contact, communication, billing and operational data. Privacy controls must be explicit rather than added after integrations and exports exist.

This specification defines product capabilities, not jurisdiction-specific legal advice.

## Consent and communication preference
Where applicable track:
- purpose/category
- status
- collection source
- captured at
- evidence/reference
- expiry/review where required
- withdrawal
- destination/channel

Communication eligibility may differ by:
- operational service message
- billing notice
- security notice
- optional marketing/broadcast communication

Mandatory contractual/security communications should not be mislabeled as marketing consent.

## Contact preferences
Support channel preferences and do-not-contact states where applicable, while allowing mandatory system/security notices under policy.

## Data rights workflow
Authorized workflows may support:
- data access/export request
- correction request
- restriction/communication preference update
- deletion/anonymization request
- objection/consent withdrawal where applicable

Requests should be tracked with identity verification, scope, status, decision, completion evidence and audit.

## Retention
Retention policy can differ by:
- audit/security evidence
- billing/commercial records
- Files
- Vault
- notifications
- communications
- AI activity
- connector/integration events
- imports/exports

Deletion does not automatically override a legal/contractual retention hold.

## Legal/operational hold
Where enabled, a hold prevents automated purge for specified records and records the reason/authority/expiry/reviewer.

## Anonymization versus deletion
Some historical operational records may need identity minimization rather than destructive removal. The product should distinguish:
- archive
- soft delete
- purge
- anonymize
- retain under hold

## Integrations
Connector sync policy must consider deletion/consent propagation. Re:Solve must not claim a third-party deletion happened unless the connector confirms it.

## AI
Provider data policy, retention and sensitive classes belong in AI settings. Privacy-restricted content should not be sent merely because the user can see it if provider policy disallows that class.

## Export
Privacy/data-right exports must be permissioned and scoped. Generic export tools do not automatically satisfy a formal data-right request.

## Audit
Privacy requests and material consent changes are auditable.

## Acceptance criteria
- communication preference and mandatory notice policy are distinguishable
- data-right workflows verify requester identity
- retention/hold rules prevent unsafe automatic purge
- connector deletion/sync is evidence-based
- AI/provider use respects configured data policy
- product supports privacy operations without becoming a legal compliance oracle
