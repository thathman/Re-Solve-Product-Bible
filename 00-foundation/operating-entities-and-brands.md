# Operating Entities and Brands

## Purpose
Re:Solve needs to distinguish the business operating the platform from the Organisations it serves.

The first deployment uses Airix Media as the operating business, while client institutions remain Organisations.

## Core concepts

### Workspace
The top-level installation boundary. A first deployment has exactly one Workspace.

### Operating Entity
A legal/operational business identity that sells services, invoices clients, owns sender identities and may employ or authorize staff.

### Brand
A customer-facing identity associated with an Operating Entity. An entity may use one primary brand or several brands.

### Organisation
A client, prospect, partner, vendor or other external/internal relationship record. It is not the operating entity itself unless a future deployment explicitly models that relationship.

## Operating Entity fields
- legal name
- trading/display name
- internal code
- registration/tax identifiers where applicable
- business addresses
- primary contacts
- default currency
- locale/timezone
- default brand
- invoice/remittance identity
- document identity
- bank/payment instructions references
- sender identities
- portal defaults
- Chatwoot/support brand mapping
- status

## Brand fields
- name
- mark/logo variants
- favicon/app icon
- approved accent tokens
- email identity
- document theme
- portal identity
- support identity
- sender names/numbers
- public/guest document identity

Branding must preserve accessibility and cannot override core semantic status colors.

## Record ownership
Commercial and client-service records should know which Operating Entity owns the relationship when more than one exists.

Relevant records may include:
- Opportunities
- Proposals
- Estimates/Quotes
- Contracts
- Client Services
- Invoices
- Receipts
- Payment configurations
- Projects
- Support entitlements
- Generated documents
- sender communications

The first deployment may default every such record to Airix Media while retaining the field contract for future expansion.

## Staff access
Staff may be authorized for one or more Operating Entities. This is an operational scope, not an HR employee-management feature.

## Client experience
A client should see only the relevant operating brand/entity for its relationship. Do not expose internal multi-brand complexity unnecessarily.

## Settings
Settings should eventually support:
- Entities
- Brands
- Documents
- Billing identity
- Payment/remittance defaults
- Portal branding
- Email/WhatsApp sender identities
- support mappings

## API/MCP
Operating Entity and Brand context should be exposed only where relevant to an action. Machine clients must not infer relationships outside their scope.

## Acceptance criteria
- Airix Media can be represented as the operating business without pretending it is a client Organisation
- client records can attribute commercial/document identity to the correct Operating Entity
- future additional Airix businesses do not require a second application architecture
- client-facing surfaces do not expose irrelevant internal entity structure
- branding remains token-governed and accessible
