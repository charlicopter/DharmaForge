# Summary:
It's a fully structured, validated environment for modeling knowledge.
Hierarchy, references, and integrity are rigorously enforced.
Every piece of data has a precise location and ownership.
A structured knowledge modeling environment with rigorous validation and referential integrity.
If something feels strict — IT'S DOING YOU A FAVOR.
### DharmaForge shines in knowledge domains where you have:

• Structure

• Reuse

• Hierarchy

• Cross-references

• Evolution over time

### Philosophy

DharmaForge prioritizes correctness over comfort. The system:

• Makes invalid states impossible to create through the UI

• Surfaces errors clearly without hiding them

• Refuses to auto-fix or mutate data "helpfully"

• Enforces single ownership and referential integrity

• Provides escape hatches (validation warnings) but never silent fixes

# Core Concepts
DharmaForge is built around three key elements:
# Blueprints:
Blueprints define the structure of data. They are the architectural plans from which instances are created.
## Each blueprint contains:

• id (UUID) – unique identifier

• name (string) – descriptive name (e.g., "Task", "User", "Document")

• type (string) – category for filtering (e.g., "Work", "People", "Content")

• fields – array of field definitions

• isStatic (boolean) – true if this blueprint defines reusable shapes with defaults

• staticValues – default values for static blueprints



Static blueprints define shapes and defaults but do not appear as runtime instances.



# Fields:

Fields define the type and behavior of each data slot in a blueprint.



## Field Kinds
### Primitive

• Scalar values (text, number)

• Example: "title": "Math Knowledge Base"



###  (contain mode)

• Ownership link to a single child instance

• Parent owns child; deleting parent deletes child

• Creates instances from blueprints with fieldMode: CONTAIN



###  (reference mode)

• Reference link to a single existing instance

• No ownership; just points to another instance

• References existing instances with fieldMode: REFERENCE



### List (contain mode)

• Ownership link to multiple child instances

• Parent owns all children; deleting parent deletes all children

• Creates multiple instances with fieldMode: CONTAIN



### List (reference mode)

• Reference link to multiple existing instances

• No ownership; just points to other instances

• References multiple existing instances with fieldMode: REFERENCE



### InstanceReference

• Non-owning references to instance(s)

• Stored as array of UUIDs

• Used for semantic relationships, tags, associations

• No implied ownership or ordering



### InstanceReferenceList

• Ordered, non-owning list of references

• Stored as array of UUIDs with meaningful sequence

• Order is semantically significant (priority, steps, playlist order)

• UI displays numbered list with drag-to-reorder capability



## Field Metadata
Fields may include:

• primitiveType → "TEXT" or "NUMBER" (for primitive fields)

• cardTypeFilter → restricts which blueprint types can be linked

• fieldMode → "CONTAIN" or "REFERENCE" (for /List)

• isFieldStatic → marks field as using static default

# Instances

Instances are concrete data objects created from blueprints.

## Each instance contains:

• id (UUID) – unique identifier

• templateId (UUID) – the blueprint it derives from

• fieldValues – actual values for each field defined in the blueprint

• \_parent (UUID) – the owning instance (null for root)

• \_parentField (UUID) – the field in parent that contains this instance



# Ownership and Reference Semantics

### Ownership Rules:

• Every instance except root has exactly one parent.

• Only  (contain) and List (contain) establish ownership.

• Deleting a parent cascades to all owned children.

• Owned children appear in the Instance Tree hierarchy.



# Reference Rules

•  (reference) and List (reference) create non-owning links

• InstanceReference and InstanceReferenceList are always non-owning

• Deleting a parent does NOT cascade to referenced instances

• References do NOT appear as nodes in the Instance Tree hierarchy

• Broken references are valid but flagged in validation.

# Hard Contract Rules

DharmaForge enforces strict invariants:

• UUIDs are immutable and unique – no ID reuse, ever

• Single ownership – instances cannot have multiple parents

• No orphans – all non-root instances must be reachable from root

• Static blueprints are not runtime instances – they define shapes only

• UI is observational – never auto-fixes or mutates state "helpfully"

• Broken references are valid – must be flagged but not auto-deleted

• Validation reveals, never fixes – invalid states remain visible

# State Structure

javascriptstate = {

&nbsp; blueprints: Blueprint\[],           // All blueprint definitions

&nbsp; instances: { \[uuid]: Instance },  // All runtime instances

&nbsp; rootInstanceId: string            // UUID of the single root instance

}

The root instance is the single entry point to the entire data graph.

# Three-Pane Interface.
## Instance Tree (Left Panel)

• Displays the full containment hierarchy starting from root

• Shows only contain-mode relationships (ownership tree)

• Does NOT show reference-mode or InstanceReference links

• Click to select and navigate instances

• Expand/collapse nodes to explore nested structures

• Verbose mode shows field values inline

## Instance/Blueprint Editor (Center Panel)

Main workspace for editing the selected item.

### When an instance is selected:

• Edit primitive field values (text, number)

• Add/remove  children (contain or reference mode)

• Add/remove List children (contain or reference mode)

• Manage InstanceReference and InstanceReferenceList links

• Override static defaults (with visual indicators)

• Navigate via clickable reference chips

### When a blueprint is selected:

• Edit blueprint name and type

• Add/remove/reorder fields

• Set field kinds and constraints

• Define static default values for primitives

• View instance usage statistics

# Blueprint Library (Right Panel)

• Searchable list of all blueprints

• Create new blueprints via "New Blueprint" button

• Click a blueprint to edit its definition in the center panel

• Delete blueprints (blocked if instances exist)

• Visual indicators for static blueprints

## Interaction Flow

• Select an instance in the Instance Tree (left)

• Editor activates for that instance (center)

• Edit fields – all changes respect contract rules

• Or select a blueprint in the Blueprint Library (right)

• Editor switches to blueprint editing mode

• Create instances from the selected blueprint

• Validation runs in the background, surfaces errors without fixing

# Key Behaviors

Containment enforces single ownership – multi-parent selection blocked

Static blueprints are read-only – fields visible for reference only

References are UUID-based – picker UI for selecting target instances

Broken references are surfaced – flagged in validation, not auto-fixed

UI prevents contract violations – structural safeguards built-in

Drag-and-drop reordering – available for InstanceReferenceList only

Smart instance labeling – uses primitive values → container names → IDs

Click navigation – reference chips are clickable to jump to targets

# Field Kind Decision Guide:

### Use  (contain) when:

• Parent owns and manages child's lifecycle

• Child only makes sense in parent's context

• Example: Document → ContentBlocks, Form → FormFields

### Use  (reference) when:

• Parent needs a single reference to an existing instance

• Referenced instance exists independently

• Example: Task → assignedUser, Invoice → customer



### Use List (contain) when:

• Parent owns and manages multiple children

• Children only make sense in parent's context

• Example: Project → Tasks, Album → Photos



### Use List (reference) when:

• Parent needs multiple references to existing instances

• Referenced instances exist independently

• Example: Project → teamMembers, Article → relatedArticles



### Use InstanceReference when:

• Representing semantic relationships (not ownership)

• Need to reference instances across hierarchy

• Order doesn't matter

• Example: Task → tags, Person → interests



### Use InstanceReferenceList when:

• Representing ordered semantic relationships

• Order is meaningful (priority, sequence, ranking)

• Need explicit reordering UI

• Example: Playlist → songs, Recipe → steps, TodoList → tasks



# Example Use Case

Modeling a Mathematics Knowledge Base:

\### Blueprints:

• Root (type: "Root")

• Concept (type: "Content")

• Example (type: "Content")

• Task (type: "Work")



### Instances:

• Root: "Math Knowledge Base"

• Concept: "Algebra" (contained)

Example: "Linear Equations" (contained)

Example: "Quadratic Formula" (contained)

• Concept: "Geometry" (contained)

• Task: "Prove Pythagorean Theorem" (contained)



### References:

• "Algebra" → InstanceReference to "Number Theory" (semantic link)

• "Linear Equations" → InstanceReference to "Variables" (related concept)



### Result:

• Containment ensures "Algebra" belongs to "Math Knowledge Base"

• References allow pointing to "Number Theory" without ownership

• Deleting "Algebra" cascades to "Linear Equations" and "Quadratic Formula"

• Deleting "Algebra" does NOT cascade to "Number Theory" (reference only)




# Code Constants (Legacy Naming)

Internal code uses legacy constant names for backward compatibility:

&nbsp;   const FIELD\_KIND = {

&nbsp;       PRIMITIVE: 'primitive',

&nbsp;       CARD\_REF: '',

&nbsp;       LIST\_OF\_CARDS: 'List',

&nbsp;       ENTITY\_REF: 'instanceReference',

&nbsp;       LIST\_ENTITY\_REF: 'instanceReferenceList'

&nbsp;     };



const FIELD\_MODE = {

&nbsp;   CONTAIN: 'CONTAIN',    // Ownership

&nbsp;   REFERENCE: 'REFERENCE' // Non-ownership

};



const PRIMITIVE\_TYPE = {

&nbsp;   TEXT: 'TEXT',

&nbsp;   NUMBER: 'NUMBER'

};

UI and documentation use conceptual names (instantiator, InstanceReference, etc), while code uses legacy constants for stability.

# Validation (Important!)

Validation runs automatically and surfaces errors without mutating state.

### Validates:

• All UUIDs are valid format

• All instances reference existing blueprints

• All field values match their field kind expectations

• No orphaned instances (except root)

• No circular references in containment tree

• No multi-ownership violations

• Broken references are flagged but allowed

# Undo/Redo integrity
Undo in DharmaForge isn’t: “Reverse this action” - It’s: “Go back to an earlier universe”

• Identities matter

• References matter

• History matters

• Carefully avoids resurrecting deleted things incorrectly and breaking references silently

Validation is the "Truth Button" - When you press it, DharmaForge checks:

• Does anything have two parents?

• Does anything exist without a parent?

• Are there references to deleted things?

• Are static-only items leaking into runtime?

• It does not auto-fix - it simply tells you the truth.

• Validation tells you if the data structure can be trusted.

DharmaForge enforces hierarchy, ownership, and data contracts to ensure every piece of information has a precise location and well-defined relationships.

### Does NOT:

• Auto-delete broken references

• Auto-fix invalid data

• Mutate state to "correct" errors

• Hide invalid data from the user


# Static Defaults

Blueprints can define static default values for primitive fields.

### Behavior:

• New instances inherit static defaults automatically

• Instances can override defaults by editing the field

• Overridden values are independent from blueprint changes

• Visual indicators show defaults vs overrides (amber borders, tooltips)

• "Reset to Default" button available for overridden fields


### Example:

javascript{

&nbsp; "id": "task\_blueprint",

&nbsp; "name": "Task",

&nbsp; "fields": \[

&nbsp;   { "id": "status\_field", "name": "status", "fieldKind": "PRIMITIVE" }

&nbsp; ],

&nbsp; "staticValues": {

&nbsp;   "status\_field": "TODO"  // Default for new instances

&nbsp; }

}

The goal is a trustworthy structured environment where users can model complex knowledge with confidence that the system enforces constraints rigorously and transparently.

# Technical Notes

• Single HTML file – entire application in one file for portability

• localStorage persistence – state saved automatically

• Undo/redo support – full history for all mutations

• Export/import – JSON export for data backup and migration

• Validation on demand – "Validate" button for comprehensive checks

• Orphan cleanup – removes unreachable instances (user-triggered)

• Deep linking – navigate to instances via selection

• Verbose mode – inline field values in Instance Tree





License

MIT License - see LICENSE file for details



Contributing

DharmaForge is a single-file application with a strict architectural contract. Contributions should:



Respect the Hard Contract rules

Never auto-fix or mutate state silently

Prioritize correctness and explicitness

Maintain referential integrity

Include validation for new features

