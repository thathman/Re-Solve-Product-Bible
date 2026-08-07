# Custom Fields, Taxonomy and Record Extensibility

## Purpose
Re:Solve needs controlled extensibility for deployment-specific data without turning every record into an unvalidated JSON blob or requiring a plugin for every extra field.

## Custom fields
Supported field types may include:
- short text
- long text
- rich text where justified
- number
- money
- percentage
- date
- date/time
- boolean
- single select
- multi select
- email
- phone
- URL
- user/team reference
- organisation/contact/property/project reference
- file reference where appropriate
- calculated/derived field in a controlled future phase

## Field definition
A definition should declare:
- stable id/key
- label
- description/help
- target record type(s)
- data type
- validation
- default
- required/read-only behavior
- choices/source
- indexing/search eligibility
- API exposure
- Portal visibility
- AI indexing/use policy
- permissions
- sensitivity classification
- plugin/owner
- active/archive state

## Dynamic field rules
A controlled rules layer may later support:
- show/hide based on other fields/status/type
- required when condition matches
- read-only when condition matches
- default from another approved value

Do not create a full arbitrary programming language inside form configuration.

## Calculated fields
If introduced, formulas must use a bounded expression model with declared dependencies and safe types. They must be clearly marked derived and cannot silently become authoritative financial/accounting truth.

## Tags and taxonomy
Tags are lightweight cross-record labels. Taxonomies/categories are controlled vocabularies with domain meaning.

Use tags for flexible grouping/search.
Use taxonomy/categories when reporting, routing or business rules depend on consistent values.

Tag fields:
- id
- label
- optional semantic color token
- description
- scope/domain
- active/archive

Avoid hundreds of inconsistent near-duplicate tags by supporting admin cleanup/merge.

## Native relationships versus custom relationships
Strong native relationships such as Organisation -> Property, Project -> Organisation and Invoice -> Payment remain explicit domain concepts.

A later typed custom-relationship framework may support deployment/plugin-defined associations with labels, cardinality and permissions. It must not replace strong native relationships.

## Custom record types
Custom record types are an advanced future capability for deployments needing a new structured business object without a full plugin.

They are not part of FOUND-001 and should not be used to model core Re:Solve domains.

If implemented later, they require:
- schema/fields
- permissions
- relationships
- list/record UI
- activity
- API
- search
- audit
- plugin migration path if capability grows complex

## Forms
The Forms platform can map submission fields into approved custom fields according to explicit mapping rules.

## Reporting/search
Only fields declared reportable/searchable should participate in corresponding indexes. Permission and sensitivity rules apply before ranking/aggregation.

## API/MCP/Àríyá
Custom fields use stable keys and typed values in APIs. Àríyá can use permitted fields but must respect visibility/sensitivity and identify derived values where material.

## Acceptance criteria
- deployment-specific fields do not require schema hacks in UI code
- custom fields remain typed and validated
- sensitive custom fields can be restricted
- Portal/API/search behavior is explicit
- native domain relationships remain first-class
- extensibility does not devolve into arbitrary JSON or arbitrary executable formulas
