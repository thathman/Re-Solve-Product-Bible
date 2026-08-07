# Saved Views, Favorites and Recents

## Purpose
Re:Solve is an operational system with many records. Users need personal and shared ways to return to the information they care about without expanding the permanent navigation.

## Saved Views
A Saved View captures an approved query/presentation configuration such as:
- filters
- sort
- columns
- grouping
- density
- date range
- search where safe
- selected visualization/list mode

## Visibility
Saved Views may be:
- Private
- Team shared
- Workspace shared
- system/default

Shared views require appropriate permissions and must not bypass record-level security.

## Supported areas
Likely examples:
- Organisations/Clients
- Contacts
- CRM Leads/Opportunities
- Properties
- Projects/Tasks
- Requests
- Billing
- Monitoring/Renewals
- Files
- Reports
- Audit where authorized

## Favorites / Pinned records
Users can favorite/pin frequently used records and destinations.

Favorites may appear in:
- command palette
- search
- optional compact quick-access area
- My Work/Saved

Do not bloat the root sidebar with every favorite.

## Recents
Maintain permission-filtered recent destinations/records for fast return.

Recent history should avoid storing sensitive Vault reveal content. A recent Vault item may reference safe metadata only if permitted.

## Default views
A domain may ship curated defaults such as:
- Active Clients
- My Clients
- Renewals Next 30 Days
- Overdue Invoices
- Degraded Properties
- Active Projects

Admins may set safe defaults where useful, while users can preserve personal preferences.

## URLs and sharing
View state may be represented in URLs where safe so filters are deep-linkable. A shared URL never bypasses authorization.

## Plugins
Plugins may contribute view definitions/columns/filters through approved contracts.

## API/MCP/Àríyá
Saved views can be listed/applied through controlled APIs. Àríyá may interpret a user's active view context or help create a view, but must not expose hidden records.

## Acceptance criteria
- users can return to high-value slices without navigation growth
- shared views respect current caller permissions
- favorites do not become access grants
- recent history avoids sensitive content leakage
- view definitions remain portable across desktop/mobile rendering
