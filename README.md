## A Note Before You Begin

If DharmaForge feels uneasy to use at first, that reaction is expected.

This is not a tool designed to smooth over uncertainty or guide you along a predefined path. It is designed to make structure visible — including incomplete, contradictory, or unresolved structure.

You may encounter missing links, broken references, empty fields, or states that other software would normally hide or repair. These are not errors to be eliminated on sight. They are part of the model as it exists right now.

DharmaForge does not rush you toward correctness. It gives you time to think.

If you are looking for a system that automatically cleans up after you, this will feel uncomfortable. If you are looking for a system that respects unfinished thought, read on.

---

# The DharmaForge Constitution

## Purpose

DharmaForge exists to make **structural truth explicit**.

It is a system for modeling entities, relationships, and ownership without inference, automation, or repair. Its purpose is not convenience, speed, or presentation, but fidelity: the faithful preservation of intent and structure over time.

This constitution defines the non‑negotiable rules that govern DharmaForge. Any implementation, interface, or extension that violates these rules is not DharmaForge.

---

## Foundational Principles

### 1. Identity Is Sacred

Every instance in DharmaForge is identified by a UUID. That UUID is the identity of the instance and must never change.

Names, labels, and paths are descriptive only. They may change freely. Identity may not.

**Reasoning:**
Without stable identity, references become ambiguous, history collapses, and refactoring becomes destructive. DharmaForge treats identity as the anchor that allows structure to evolve without erasing meaning.

---

### 2. Ownership Is Explicit and Singular

Every runtime instance has exactly one owner, except the root. Ownership is established only through contain‑mode instantiation.

There is no inferred ownership. There is no shared ownership. There is no implicit parentage.

**Reasoning:**
Ownership defines lifecycle. Without clear ownership, deletion, movement, and mutation become unsafe. DharmaForge requires ownership to be explicit so consequences are visible and intentional.

---

### 3. Reference Is Not Ownership

References store UUIDs only. They do not imply containment, lifecycle control, or responsibility.

A reference may be broken. A broken reference is a valid state.

**Reasoning:**
Real systems contain incomplete information, stale links, and unresolved dependencies. DharmaForge preserves these conditions rather than concealing them, because absence and breakage are often meaningful.

---

### 4. Broken States Are First‑Class

Invalid, incomplete, or broken states are allowed to exist.

DharmaForge may detect and surface such states, but it may not repair them automatically or silently.

**Reasoning:**
Automatic repair destroys intent. DharmaForge treats brokenness as information, not error. The system’s responsibility is to reveal structure, not to correct it.

---

### 5. Mutation Is Explicit

All mutations must be deliberate, visible actions.

There are no background reconciliation passes. There are no hidden cascades. There are no inferred defaults.

**Reasoning:**
Hidden mutation breaks trust. DharmaForge requires every structural change to be traceable to an explicit decision made by the user.

---

### 6. Validation Does Not Mutate State

Validation may analyze and report on the structure.

Validation may never modify the structure it inspects.

**Reasoning:**
Inspection and mutation must remain separate. When validation mutates state, analysis becomes untrustworthy.

---

### 7. Blueprints Are Not Instances

Blueprints and static shapes define structure. They are not runtime entities.

They may not appear in runtime graphs. They may not be owned or referenced as instances.

**Reasoning:**
Separating definition from instantiation prevents category errors and preserves the clarity of the model.

---

### 8. The UI Must Not Infer Intent

The interface may present options and warnings.

It may not guess what the user means, auto‑select defaults that imply commitment, or silently repair structure.

**Reasoning:**
Inference trades correctness for convenience. DharmaForge refuses this trade.

---

## Field Semantics

Fields in DharmaForge have precise meaning. Their behavior is defined by their kind, not by context or usage.

- **Primitive fields** store scalar values only.
- **Contain instantiators** establish ownership and lifecycle.
- **Reference instantiators** store UUIDs without ownership.
- **Instantiator lists** behave identically, but allow multiplicity.

Changing a field’s kind may destroy data. Such actions must be explicit and warned.

---

## Deletion Rules

- Deleting an instance deletes all instances it owns.
- Deleting a reference removes only the UUID.
- Removing a contain‑mode field must either cascade deletion or be blocked.

No operation may result in multiple ownership.

---

## Validation Guarantees

A conforming DharmaForge implementation must be able to detect:

- Duplicate UUIDs
- Multiple ownership
- Orphaned non‑root instances
- Leakage of static shapes into runtime graphs
- Broken references (as warnings)

Detection does not imply repair.

---

## AI Constraints

AI systems interacting with DharmaForge must obey all invariants.

AI may propose changes. AI may analyze structure. AI may not autonomously mutate state.

Any AI‑generated mutation must validate before acceptance.

---

## Scope and Limits

DharmaForge is not a database, a document editor, a simulation engine, or a productivity platform.

It does not execute logic. It does not resolve ambiguity. It does not optimize for ease of use.

It exists to preserve structural truth.

---

## Closing Statement

DharmaForge is intentionally strict.

Its constraints are not incidental; they are the point. Any feature, extension, or interface that weakens these rules undermines the system’s purpose.

This constitution exists to prevent that erosion.

If you accept these terms, DharmaForge will show you your structure honestly.

If you do not, it will not pretend to be something else.


---

## How DharmaForge Differs From Other Tools

DharmaForge is often compared to note-taking apps, graph databases, game engines, or knowledge graphs. These comparisons are useful only up to a point. The differences matter more than the similarities.

**Compared to productivity and knowledge tools (Notion, Obsidian, Roam):**
Those tools prioritize convenience, automatic organization, and inferred structure. They often repair broken links, auto-create missing objects, or silently reshape data to preserve usability. DharmaForge does none of this. If a relationship is broken, it stays broken. If structure is incomplete, it remains visible as such. The system prefers truth over smoothness.

**Compared to graph databases and modeling tools:**
Graph systems typically enforce schemas or normalize data behind the scenes. DharmaForge exposes structure directly and allows it to be wrong. Invalid or partial graphs are not errors to be fixed; they are states to be examined.

**Compared to game engines or world-building tools:**
Game engines tend to assume runtime correctness and often collapse authoring-time ambiguity into runtime certainty. DharmaForge is explicitly *not* a runtime engine. Blueprints and static shapes are authoring constructs only. Nothing is assumed to be executable or complete.

**Compared to an IDE:**
An IDE does not write correct programs for you; it provides visibility, warnings, and tools to reason about code. Broken builds, type errors, and incomplete implementations are first-class states. DharmaForge takes the same stance toward structure. It is closer to an IDE for structure than to a generator or automation system. The presence of warnings does not imply automatic fixes.

---

## What DharmaForge Is Not

DharmaForge is not an automation engine. It will not infer intent.

It is not a recommendation system. It will not suggest "better" structures.

It is not a self-healing graph. It will not repair broken references or missing ownership.

It is not a runtime system. It does not execute, simulate, or resolve behavior.

It is not a collaborative consensus tool. Conflicts are not merged or smoothed over.

If you are looking for a system that optimizes for ease, speed, or guardrails, DharmaForge is likely the wrong tool.

---

## Invalid States Are Intentional

DharmaForge allows and preserves invalid states by design. These include, but are not limited to:
- Broken references
- Missing type filters
- Orphaned instances
- Incomplete ownership chains

Invalid does not mean meaningless. Many real design and reasoning processes pass through states that are incomplete, contradictory, or temporarily inconsistent. DharmaForge treats these as legitimate phases, not errors to be erased.

Warnings may be shown. State is never mutated as a side effect of validation.

---

## Validation Philosophy

Validation in DharmaForge is observational, not corrective.

It may:
- Detect and surface structural violations
- Report ownership conflicts
- Warn about broken references or missing types

It may not:
- Modify data
- Create or delete instances
- Reassign ownership
- Infer intent

This separation is strict. Validation exists to inform human judgment, not replace it.

---

## On AI and Automation

DharmaForge may integrate with AI-assisted tools, but AI is never autonomous within the system.

AI may:
- Read structure
- Propose mutations
- Simulate outcomes

AI may not:
- Commit changes
- Repair structure automatically
- Bypass validation or invariants

All mutations must be explicit and attributable.

---

## Anticipated Criticisms

**"This feels hostile."**
The system prioritizes clarity over comfort. This is intentional.

**"Why won’t it just fix things?"**
Because fixing requires assumptions. Assumptions destroy provenance.

**"This is unfinished."**
DharmaForge distinguishes between incomplete *models* and incomplete *tools*. The former are allowed. The latter are not silently masked.

**"This could be simpler."**
Simplicity achieved by hiding complexity is not simplicity; it is opacity.

---

## Amendment and Versioning

This constitution is versioned.

Changes may occur, but no version will retroactively redefine the meaning of existing structures. Backward reinterpretation is forbidden.

Any amendment must:
- State what invariant it affects
- State why the previous rule was insufficient
- Preserve explicitness and non-inference

---

## Final Note

DharmaForge is designed for people who care more about structural truth than immediate usability.

If that tradeoff feels uncomfortable, the system is working as intended.


---

## Why It Feels Uncomfortable

Most software is designed to protect you from seeing your own uncertainty.

DharmaForge is not.

If you feel a low-grade tension while using it — a sense that the tool is refusing to “help” in ways you expect — that reaction is not a bug. It is the consequence of a different set of priorities.

### You Can See Incomplete Thought

Most tools hide intermediate states. They autosave, auto-correct, auto-complete, and quietly repair structures before you ever see them.

DharmaForge shows you the shape *while it is still forming*.

You can have fields that don’t yet point anywhere, references to things that don’t exist anymore, and structures that are valid in isolation but unresolved in context.

This is uncomfortable because people are trained to equate visibility with correctness. DharmaForge breaks that association.

### Errors Are Not Rescued

In most systems, an error is a failure that must be resolved immediately.

In DharmaForge, an error is an observation.

Broken references, missing filters, or orphaned instances are allowed to exist because they represent real modeling conditions. You are permitted to leave them unresolved while you think.

This feels wrong at first because modern software treats intervention as kindness. DharmaForge treats restraint as respect.

### The Tool Will Not Decide For You

DharmaForge refuses to guess your intent.

It will not auto-select the “closest” blueprint, infer what you meant by a partial structure, or reinterpret your model to make it nicer.

You must choose when something is linked, moved, created, or left alone.

That responsibility creates friction — and that friction is intentional. The tool will not quietly rewrite your thinking on your behalf.

### You Can Break Things Without Being Stopped

DharmaForge allows you to do things that other tools prevent: moving instances in ways that create orphans, deleting structures that are still referenced, or constructing contradictory graphs.

Most software enforces local correctness at all times.

DharmaForge enforces structural honesty instead.

If something is broken, it stays broken until *you* decide what that means.

### There Is No “Happy Path”

Many tools are optimized around a golden workflow. Deviating from it feels like misuse.

DharmaForge has no preferred path. It does not reward linear progress or punish detours.

As a result, you do not get the emotional feedback loop of “doing it right.” You get clarity instead.

That can feel isolating.

### It Treats You Like an Author, Not a User

DharmaForge assumes you can hold contradictory or incomplete ideas without collapsing.

It does not guide you gently forward. It does not smooth rough edges. It does not apologize for ambiguity.

This can feel confrontational — especially if you are used to tools that continuously reassure you.

DharmaForge offers no reassurance. Only fidelity.

### The Discomfort Is Diagnostic

The unease many people feel when first using DharmaForge is not confusion about the interface.

It is exposure.

You are seeing where your model is vague, where your assumptions conflict, and where you were relying on the tool to make decisions for you.

That discomfort is similar to reading raw source code or unpolished drafts. It removes the illusion of completion.

### On Trust

If you sit with the discomfort long enough, something shifts.

You stop asking why the tool will not fix something for you, and start asking why you want it fixed right now.

At that point, DharmaForge stops feeling hostile and starts feeling honest.

It does not try to make you comfortable.

It tries to make your thinking visible.

