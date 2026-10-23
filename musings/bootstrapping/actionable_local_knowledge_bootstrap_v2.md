# Actionable Local Knowledge for Coding Agents --- Bootstrap Design

## Purpose

Build a small, auditable local knowledge system that helps a coding
agent determine:

1.  which concepts in a request have locally important meaning;
2.  which local knowledge applies;
3.  how more general local knowledge can be used when specific knowledge
    is absent;
4.  which conclusions are established locally, discoverable, inferred,
    or require user input; and
5.  what reusable knowledge should be proposed after implementation or
    investigation.

The initial system SHOULD remain simple: Markdown files with YAML front
matter, source control, deterministic shell queries, and lightweight
validation.

A graph database, semantic index, embeddings, or dedicated knowledge
service SHOULD NOT be required until demonstrated needs justify them.

------------------------------------------------------------------------

## 1. Normative vocabulary

### LOCAL

**LOCAL** knowledge is knowledge whose interpretation, selection, or
application is specific to this codebase, organization, system, or
domain context.

LOCAL does not mean obscure.

An LLM may already know the dictionary or textbook meaning of a term
such as `realized volatility`, `timestamp`, `ClickHouse`, or `job`. A
concept belongs in the local knowledge system when the agent must
recognize that its meaning, treatment, conventions, or consequences here
matter and SHOULD NOT be silently replaced by generic assumptions.

The glossary therefore records **salient local vocabulary**, not an
encyclopedia.

### MUST, SHOULD, MAY

Normative language follows BCP 14 (RFC 2119 and RFC 8174):

-   **MUST / MUST NOT** indicate an absolute local requirement or
    prohibition.
-   **SHOULD / SHOULD NOT** indicate the expected choice, while allowing
    exceptions when the consequences are understood and justified.
-   **MAY** indicates an explicitly permitted choice.

Only the uppercase forms carry this normative meaning.

These terms SHOULD be used sparingly. Ordinary descriptive knowledge
SHOULD remain ordinary prose.

------------------------------------------------------------------------

## 2. Concepts

A concept is a locally salient unit of meaning.

Concepts contain **semantic routing information, not substantive knowledge**. A concept exists primarily to answer: *does this concept apply to what the user is talking about?* Its name, aliases, parents, and short description help the librarian recognize the concept and navigate toward applicable leaves. Substantive LOCAL knowledge belongs in leaves.

A useful smell test is: if removing a sentence makes concept recognition or routing materially worse, it probably belongs in the concept; if removing it makes the resulting work materially worse, it probably belongs in a leaf.

Example:

``` yaml
id: realized-volatility
name: Realized volatility
aliases:
  - realized vol
  - RV
parents:
  - volatility
  - metric
description: >
  Volatility estimated from observed returns. The term alone does not
  determine estimator, sampling frequency, window, price source,
  annualization, or data-cleaning policy.
```

A concept SHOULD contain:

``` yaml
id: stable-id
name: Preferred human-readable name
aliases: []
parents: []
description: Short local meaning or reason the concept matters
```

### Parents

`parents` is the primary semantic relationship between concepts.

``` text
Concept --parents--> Concept
```

A parent is a more general concept.

Example:

``` text
realized-volatility
    parents → volatility
    parents → metric

volatility
    parents → quantitative-concept
```

A concept MAY have more than one parent.

Children and transitive ancestors SHOULD be computed from `parents`, not
stored redundantly.

`parents` also provides the initial mechanism for specialization and
fallback. No separate `broader`, `narrower`, or explicit intersection
relationship is required.

### Classification is also conceptual

Do not maintain a separate `kind` taxonomy if the classification is
itself meaningful.

Instead of:

``` yaml
kind: metric
```

use:

``` yaml
parents:
  - metric
```

`metric` is then an ordinary concept and can itself have parents,
leaves, conventions, or descendants.

------------------------------------------------------------------------

## 3. Leaves

A leaf is a cohesive unit of substantive LOCAL knowledge.

**Concepts route; leaves teach.** The complete knowledge base consists of concepts plus leaves; a task uses only the applicable subset.

A leaf is **not** defined by a single knowledge type. One leaf may
contain reference facts, rationale, practices, conventions, and failure
modes when they belong together.

Example:

``` yaml
id: clickhouse
concepts:
  - clickhouse
description: Local operational and software knowledge about ClickHouse.
lineage: []
```

Its Markdown body might contain:

``` markdown
# ClickHouse

## Reference
...

## Practices

### Connection management
...

### Appropriate storage
...

## Failure modes

### Connection-pool exhaustion
...

### Network partition
...
```

### When to split a leaf

Start with cohesive subject leaves.

Split part of a leaf into its own leaf when it becomes independently
useful to:

-   retrieve;
-   link;
-   maintain;
-   assign lineage;
-   supersede;
-   discuss in substantial detail.

For example, connection-pool exhaustion may begin as a section of
`clickhouse.md` and later become:

``` yaml
id: clickhouse-connection-pool-exhaustion
concepts:
  - clickhouse
  - connection-pool
  - resource-exhaustion
```

The split is driven by usefulness, not by an obligation to make every
fact atomic.

------------------------------------------------------------------------

## 4. Knowledge vocabulary inside leaves

The initial controlled vocabulary is:

### REFERENCE

A factual LOCAL nugget.

It SHOULD state enough context, restrictions, conditions, units, or
exceptions to result in unambiguous use.

### RATIONALE

A concise explanation of why something behaves as it does or why a local
choice exists.

It SHOULD identify the mechanism or reason and SHOULD include lineage
when the rationale came from an incident, experiment, code
investigation, or other identifiable source.

It is a reusable summary, not a full investigation or postmortem.

### PRACTICE

The preferred local way of doing something.

Practices help preserve continuity across implementations and agents.

A practice MAY be expressed as steps when that is the clearest way to
describe it.

### FAILURE MODE

A known way in which a calculation, process, dataset, or software
component can produce an incorrect, misleading, or operationally
undesirable result.

A failure mode SHOULD identify, where known:

-   the symptom;
-   the mechanism;
-   the context in which it occurs;
-   detection;
-   mitigation.

A generic failure mode and a locally important interaction may live in
different leaves.

For example:

``` text
outlier
```

may have generic local knowledge, while:

``` yaml
concepts:
  - realized-volatility
  - outlier
  - rolling-window
```

may document the specific entry/exit discontinuity created by an extreme
observation in rolling realized volatility.

### CONVENTION

A normative LOCAL rule governing a coherent class of representations or
choices.

Examples include:

-   units;
-   time zones;
-   date and time semantics;
-   displays;
-   terminology;
-   naming;
-   identifier formats;
-   input/output representation.

Conventions use MUST, SHOULD, and MAY when normative force matters.

A convention is ordinary knowledge in a leaf. It does not require a
special graph relationship.

------------------------------------------------------------------------

## 5. Shelved knowledge types

The following types are deliberately **not part of the initial
vocabulary**:

``` text
GUARDRAIL
INVARIANT
DECISION
PROCEDURE
```

They SHOULD be introduced only if repeated experience shows that
existing vocabulary loses a distinction that materially changes
retrieval, validation, maintenance, or agent behavior.

The ontology SHOULD grow from demonstrated need rather than anticipated
completeness.

------------------------------------------------------------------------

## 6. Multi-concept knowledge: use a Venn diagram

A leaf declares all concepts needed to describe its applicability:

``` yaml
concepts:
  - realized-volatility
  - rolling-window
  - outlier
```

This represents intersection knowledge, a conceptual lineage that justifies the leaf's existence. 

A multi-concept leaf SHOULD exist only when the interaction contains
knowledge that is more than the union of the knowledge attached to its
individual concepts.

For example:

``` text
outlier
```

can describe generic outlier knowledge.

``` text
realized-volatility + rolling-window + outlier
```

can describe the specific phenomenon in which an extreme observation
causes a discontinuity when it enters a rolling window and another when
it leaves.

### Specificity

For an active concept set, a leaf matching several active concepts is
normally more specific than a leaf matching one.

Specificity SHOULD influence retrieval order but SHOULD NOT be treated
as proof that a leaf is relevant. The agent still interprets the leaf in
the context of the task.

------------------------------------------------------------------------

## 7. Minimal relationship model

The initial semantic model SHOULD be deliberately small.

### Required relationships

``` text
Concept --parents--> Concept
Leaf    --concepts--> Concept
```

These two relationships provide:

* Semantic hierarchy — represents concepts from more specific to more general through their parents.
* Classification — treats categories such as metric, job, or data-store as ordinary ancestor concepts rather than a separate type system.
* Multi-concept applicability — lets a leaf declare that its knowledge applies to the combination of several concepts.
* Specialization — allows more specific concepts or multi-concept leaves to add knowledge that only applies in their narrower context.
* Fallback retrieval — lets retrieval move from a specific concept to its parents when the specific local knowledge is insufficient.

### Optional leaf lifecycle relationship

When needed:

``` yaml
supersedes:
  - old-leaf-id
```

This preserves historical lineage when a leaf replaces another.

### Ordinary links

Other relationships SHOULD initially use normal Markdown links unless
the system repeatedly needs to query or reason about their exact
semantics. 

### Protocol for proposing a new relationship

A new relationship MAY be proposed only when an observed use case cannot be adequately represented by existing relationships or ordinary Markdown.

A proposal MUST contain:

1. Definition — A short, unambiguous statement of what A → relationship → B means. The direction of the relationship MUST be clear from the definition.
2. Use cases — Concrete examples, preferably from existing knowledge, showing where the relationship would be used. The proposal SHOULD demonstrate more than one occurrence so that a one-off case does not become ontology.
3. Why existing representation is insufficient — Explain why parents, concepts, an existing relationship, leaf content, or an ordinary Markdown link cannot adequately represent the distinction.
4. Behavioral consequence — State what an agent, retrieval process, validator, or maintenance process can do differently because the relationship is structured. If nothing behaves differently, the relationship SHOULD remain plain text.
5. Domain and range — State which objects may appear on each side, for example Leaf → Leaf, Leaf → Concept, or Concept → Concept.
6. Examples and counterexamples — Give at least one valid example and one superficially similar case where the relationship MUST NOT be used.
7. Validation rules — State any mechanically checkable constraints introduced by the relationship, including whether multiple targets are permitted and whether cycles are meaningful or forbidden.
8. Migration — Identify existing knowledge that SHOULD adopt the relationship if accepted. A relationship that has no existing instances deserves particular scrutiny.

#### Acceptance test

A relationship SHOULD be accepted only if all three are true:

Distinct: it expresses semantics not already represented adequately.

Repeated: the distinction occurs often enough to deserve vocabulary.

Operational: representing it structurally changes retrieval, reasoning, validation, or maintenance.

Otherwise, keep the relationship in prose or as an ordinary Markdown link.

------------------------------------------------------------------------

## 8. How retrieval works

Retrieval separates concept recognition from substantive knowledge retrieval.

The user passes a manifest in a way described by [this document](./bootstrap_manifest_section.md)

### Stage 1 — Read the request

The librarian identifies words, phrases, and meanings that may correspond to LOCAL concepts.

### Stage 2 — Resolve concepts

While the catalog is small, the librarian SHOULD receive a compact catalog of **all concepts**:

```text
id | name | aliases | short description
```

It selects concepts that materially apply. This deliberately postpones a smarter retrieval system until scale or observed recognition failures justify one.

Concepts may enter the active set as:

```text
MATCHED
    Recognized from a name or alias.

INFERRED
    Recognized from the meaning of the request even though no name or
    alias appears literally.

ACTIVATED
    Introduced later because retrieved LOCAL knowledge establishes
    that another concept materially matters.
```

These labels describe retrieval provenance, not ontology types. Prefer the most specific supported concepts; do not replace them with their parents.

### Future coarse candidate generation

When the complete catalog becomes too large, insert a high-recall first pass:

```text
query
  ↓
coarse concept candidates
  ↓
LLM reads candidate names, aliases, and descriptions
  ↓
active concepts
```

Candidate generation MAY later use aliases, lexical/full-text search, fuzzy matching, semantic retrieval, or a hybrid. It SHOULD favor recall over precision. False positives can be removed in the semantic pass; missing a relevant concept is harder to recover from.

The downstream librarian algorithm SHOULD remain independent of the candidate-provider implementation.

### Stage 3 — Retrieve leaves

Retrieve leaves whose `concepts` contain active concepts. Leaves matching several active concepts are normally more specific than leaves matching one. This provides the Venn-diagram behavior without an explicit intersection model.

### Stage 4 — Use parents for fallback

Parents expand the candidate knowledge space when specific concepts do not provide sufficient LOCAL knowledge:

```text
realized-volatility
→ volatility
→ quantitative-concept
```

Search exact concepts before parents. Parent knowledge is a retrieval candidate, not automatically inherited truth.

The DAG answers:

> Given that this specific concept matters, where can I look for more general LOCAL knowledge if its own leaves are insufficient?

### Stage 5 — Read leaves and reinterpret the task

The librarian reads the substantive LOCAL knowledge and rereads the request in that light. Generic wording may acquire local consequences.

The librarian MUST distinguish implications established by LOCAL knowledge from conclusions based primarily on general knowledge.

### Stage 6 — Activate newly material concepts

Retrieved knowledge may reveal another material concept:

```text
"daily market job"
↓
daily-job
↓
read daily-job leaf
↓
LOCAL knowledge establishes trading-date semantics
↓
ACTIVATE trading-date
↓
retrieve trading-date leaves
```

Retrieval MAY iterate, but this is not unrestricted graph traversal. Activate a concept only when the task or retrieved LOCAL knowledge makes it materially relevant.

### Stage 7 — Assess coverage

After retrieval and reinterpretation, enumerate material questions and classify them using Section 10.

- **Hierarchy:** where else should I look?
- **Coverage:** do I understand this material part of the task well enough to proceed?

DISCOVERABLE items SHOULD be investigated where practical before asking the user.

### Stage 8 — Produce the task context

Emit a standardized task context containing:

- concepts and how they were recognized;
- ancestors actually used for fallback;
- leaves read;
- task-specific interpretations;
- coverage;
- unresolved user questions.

The task context is the librarian's compact, auditable **proof of retrieval and interpretation** and the implementation agent's input contract.

### Stage 9 — Build the expanded context

The task context references leaves rather than copying all substantive content.

The **expanded context** is:

```text
task context
+ bodies of referenced leaves needed for execution
```

Distinguish:

```text
KNOWLEDGE BASE
    all concepts + all leaves

RETRIEVED KNOWLEDGE
    applicable leaves selected for this task

TASK CONTEXT
    structured interpretation and coverage record

EXPANDED CONTEXT
    task context + required referenced leaf content
```

The expanded context is the task-specific LOCAL knowledge package supplied to the implementation agent.

### Stage 10 — Stop

Stop iterating when no materially relevant concepts are newly activated, useful parent fallback has been considered, and further deterministic retrieval or discovery does not materially improve coverage.

## 9. Worked example: timestamp conventions

Assume these concepts exist:

``` text
timestamp
time-zone
persisted-data
user-display
market-data
trading-date
daily-job
```

with relationships such as:

``` text
daily-job
    parents → job

trading-date
    parents → date

market-timestamp
    parents → timestamp
```

Assume this leaf exists:

``` yaml
id: timestamp-conventions
concepts:
  - timestamp
  - time-zone
description: >
  Local rules for representing timestamps and choosing time zones.
```

with:

``` markdown
## Convention

Persisted event timestamps MUST be represented in UTC.

Exchange-local trading dates MUST use the exchange calendar and its
local time zone.

User-facing timestamp displays MAY convert timestamps to the requested
display time zone.
```

### Example A --- Persist an event timestamp

Task:

> Add `received_at` to the stored quote records.

#### Concept recognition

The librarian recognizes or infers task concepts:

``` text
timestamp
persisted-data
quote
```

`received_at` is strongly indicative of a timestamp even though the word
`timestamp` does not appear literally.

#### Retrieval

`timestamp` directly retrieves `timestamp-conventions`.

The leaf states that persisted event timestamps MUST use UTC.

#### Coverage

``` text
representation/time-zone → KNOWN
```

The implementation agent does not need to ask which time zone to use.

The task context records the convention and its source leaf.

------------------------------------------------------------------------

### Example B --- Add a timestamp to a UI

Task:

> Show the last quote update time on the instrument page.

Recognized concepts:

``` text
timestamp
user-display
quote
```

The same `timestamp-conventions` leaf is retrieved through `timestamp`.

The relevant rule is:

> User-facing timestamp displays MAY convert timestamps to the requested
> display time zone.

Coverage might then be:

``` text
storage semantics      → KNOWN
display-zone policy    → KNOWN: conversion is permitted
actual desired zone    → DISCOVERABLE if UI preferences/config establish it
                         otherwise INFERRED if an established UI pattern is clear
                         otherwise NEED_USER if the product meaning remains ambiguous
```

The convention does not answer every timestamp question. It narrows what
remains unresolved.

------------------------------------------------------------------------

### Example C --- Daily market job

Task:

> Run this calculation once per day and write the result with the date.

Recognized concepts:

``` text
daily-job
date
```

Suppose `daily-job` has parent `job`, but no timestamp relationship.

The librarian SHOULD NOT retrieve every timestamp convention merely
because jobs often have timestamps.

A `daily-job` leaf may establish that market-facing daily jobs use a
trading date. That causes recognition of:

``` text
trading-date
```

which may then retrieve a leaf about trading-date conventions.

This demonstrates staged reinterpretation:

``` text
request
→ daily-job knowledge
→ recognize trading-date as material
→ retrieve trading-date knowledge
→ refine interpretation
```

Retrieval may therefore require more than one pass.

------------------------------------------------------------------------

### Example D --- Unix milliseconds from an external API

Task:

> Parse the `ts` field returned by vendor X.

Initial concepts:

``` text
timestamp
vendor-x
```

The timestamp convention is retrieved, but it may not establish:

-   whether `ts` is seconds or milliseconds;
-   whether it is UTC;
-   whether it represents event time or receipt time.

Coverage:

``` text
local persisted representation → KNOWN
vendor field units             → DISCOVERABLE
vendor field semantics         → DISCOVERABLE
```

The librarian SHOULD inspect vendor-local code, schemas, fixtures, or
documentation available to the project.

If it establishes that `ts` is Unix milliseconds representing event
time, that discovery may justify a LOCAL leaf for `vendor-x + timestamp`
so future tasks become KNOWN rather than repeatedly DISCOVERABLE.

------------------------------------------------------------------------

## 10. Coverage

Hierarchy answers:

> What knowledge should I look for?

Coverage answers:

> After looking, what material parts of the task do I actually
> understand well enough to proceed?

Use four states.

### KNOWN

The conclusion is established by:

-   the task itself; or
-   applicable LOCAL knowledge.

Example:

``` text
Persisted event timestamps use UTC
→ KNOWN from timestamp-conventions
```

### DISCOVERABLE

The answer is not yet known but SHOULD be obtainable from local evidence
such as:

-   code;
-   configuration;
-   schemas;
-   data;
-   tests;
-   execution;
-   repository documentation;
-   an available empirical probe.

The agent SHOULD investigate before asking the user.

A repeated DISCOVERABLE conclusion is a candidate for new LOCAL
knowledge.

### INFERRED

The agent has a satisfactory working conclusion based substantially on
general knowledge or reasoning rather than explicit LOCAL knowledge.

Inference is permitted, but it MUST remain distinguishable from locally
established fact.

Repeated important INFERRED conclusions are evidence of a knowledge-base
gap.

### NEED_USER

The librarian cannot reach a satisfactory conclusion from:

-   LOCAL knowledge;
-   discovery;
-   acceptable inference.

This includes unresolved conflicts.

The user SHOULD be asked only when the unresolved matter is material to
the task.

### Why coverage is separate from hierarchy

A rich hierarchy can retrieve every relevant leaf and still leave an
important question unanswered.

Conversely, a task may have sparse local knowledge but still be safe to
execute because the remaining details are readily discoverable or
reasonably inferred.

Coverage therefore evaluates **task understanding**, not graph
completeness.

------------------------------------------------------------------------

## 11. Task context: standardized proof of work

Every substantial task SHOULD produce a standardized task context before
implementation.

Example:

``` yaml
task: >
  Make a daily job that computes realized volatility.

concepts:
  explicit:
    - realized-volatility
    - daily-job

  activated:
    - trading-date
    - rolling-window

  ancestors_used:
    realized-volatility:
      - volatility
      - metric
    daily-job:
      - job

leaves_read:
  - realized-volatility
  - rolling-realized-volatility
  - daily-jobs
  - trading-date-conventions

interpretation:
  - statement: The calculation is a locally defined realized-volatility calculation.
    status: KNOWN
    source: realized-volatility

  - statement: The job date represents a trading date.
    status: KNOWN
    source: trading-date-conventions

coverage:
  - subject: volatility-window
    status: NEED_USER
    reason: >
      No local knowledge or task wording establishes the intended window,
      and the choice changes the economic meaning of the result.

  - subject: canonical-price-source
    status: DISCOVERABLE
    reason: >
      Existing market-data jobs and schemas should identify the canonical source.

  - subject: annualization
    status: KNOWN
    source: realized-volatility

  - subject: implementation decomposition
    status: INFERRED
    conclusion: >
      Keep the reusable calculation independent from scheduling.
    reason: >
      No applicable local practice currently establishes this.
```

### Purpose

The task context serves four roles:

1.  **retrieval audit** --- what knowledge did the librarian actually
    inspect?
2.  **interpretation audit** --- what did that knowledge cause it to
    conclude?
3.  **coverage audit** --- what remains uncertain and why?
4.  **agent contract** --- what context is passed to the implementation
    agent?

It also makes librarian behavior testable independently of
implementation quality.

------------------------------------------------------------------------

## 12. Iterative retrieval

Retrieval SHOULD allow a small number of iterations.

A leaf may reveal that another concept is material.

Example:

``` text
"daily job"
↓
retrieve daily-job
↓
daily-job knowledge establishes trading-date semantics
↓
activate trading-date
↓
retrieve trading-date convention
```

This is not unrestricted graph traversal.

A new concept SHOULD be activated only when the current task or
retrieved LOCAL knowledge makes it materially relevant.

The librarian SHOULD stop when:

-   no materially relevant concepts are newly activated; and
-   coverage no longer improves through deterministic retrieval or
    discovery.

------------------------------------------------------------------------

## 13. Lineage

Lineage belongs in leaf metadata.

Example:

``` yaml
lineage:
  - type: incident
    ref: incidents/2026-08-rv-spike
    note: >
      Entry/exit discontinuity identified while investigating
      unexplained 60-day realized-volatility jumps.

  - type: code
    ref: src/volatility/realized.py
    note: >
      Existing implementation confirmed the current annualization convention.
```

Initial controlled lineage types:

``` text
user
code
data
incident
experiment
external
derived
```

### Derived knowledge

``` yaml
lineage:
  - type: derived
    from:
      - leaf-a
      - leaf-b
    note: >
      Combined implication of the two established local facts.
```

### Detailed source artifacts

Lineage metadata SHOULD point to a separate incident report, experiment,
code location, dataset, or external source when that artifact contains
useful detail.

The leaf SHOULD contain only the reusable knowledge and enough lineage
to explain where it came from.

------------------------------------------------------------------------

## 14. Knowledge reconciliation

After a task, incident, discovery, or investigation, the librarian
SHOULD ask whether anything learned should become LOCAL knowledge.

Possible outcomes:

``` text
instance-specific
    Do not add.

already represented
    No change.

new LOCAL fact
    Add or amend REFERENCE.

new explanation
    Add or amend RATIONALE.

new preferred approach
    Add or amend PRACTICE.

new failure behavior
    Add or amend FAILURE MODE.

new normative rule
    Add or amend CONVENTION.

new vocabulary
    Add concept or alias.

repeated inference
    Consider encoding as LOCAL knowledge.

repeated discovery
    Consider encoding as LOCAL knowledge.

conflict
    Escalate rather than silently overwrite.
```

The agent MAY propose changes autonomously.

Changes to important normative conventions SHOULD be reviewed before
becoming authoritative.

------------------------------------------------------------------------

## 15. Deterministic access before indexing

Do not build generated indexes initially.

The schema and filesystem SHOULD remain the source of truth.

The agent SHOULD use deterministic commands based on `fd` and `yq`. While the concept set is small, these commands SHOULD also generate the compact complete concept catalog used during concept resolution.

A query cookbook SHOULD document canonical operations.

Example layout:

``` text
knowledge/
    concepts/
    leaves/
    incidents/
    SCHEMA.md
    QUERIES.md
```

Example operations include:

### List concept files

``` bash
fd --extension md . knowledge/concepts
```

### Extract every concept ID

``` bash
fd --extension md . knowledge/concepts -0 |
  xargs -0 yq --front-matter=extract '.id'
```

### Show concept ID and description

``` bash
fd --extension md . knowledge/concepts -0 |
  xargs -0 yq --front-matter=extract \
    '{"id": .id, "description": .description}'
```

### Find leaves mentioning a concept

The exact command SHOULD be standardized in `QUERIES.md` against the
chosen YAML/front-matter tooling.

The important property is deterministic selection against structured
fields rather than fuzzy text search.

### When to add an index

Introduce derived indexing only when measurement shows that
deterministic filesystem queries are inadequate because of:

-   scale;
-   latency;
-   repeated graph traversal cost;
-   fuzzy concept resolution;
-   semantic retrieval needs.

Generated indexes MUST remain derived state, never the authoritative
knowledge representation.

------------------------------------------------------------------------

## 16. Validation

Validation SHOULD begin small and grow from observed failure modes in
the knowledge system.

Initial checks SHOULD include:

-   unique concept IDs;
-   unique leaf IDs;
-   valid `parents`;
-   valid leaf `concepts`;
-   no forbidden parent cycles;
-   aliases that do not silently resolve to multiple concepts;
-   valid lineage types;
-   valid `supersedes` targets;
-   required front-matter fields.

More semantic validation SHOULD be added only when actual authoring or
retrieval failures justify it.

------------------------------------------------------------------------

## 17. Initial schemas

### Concept

``` yaml
id: realized-volatility
name: Realized volatility
aliases:
  - realized vol
  - RV
parents:
  - volatility
  - metric
description: >
  Local meaning and ambiguity of realized volatility.
```

### Leaf

``` yaml
id: rolling-rv-outliers
concepts:
  - realized-volatility
  - rolling-window
  - outlier
description: >
  Local knowledge about the effect of extreme observations on
  rolling realized-volatility calculations.
lineage:
  - type: incident
    ref: incidents/example
    note: Example provenance.
supersedes: []
```

The Markdown body contains the actual knowledge using the controlled
vocabulary where useful.

------------------------------------------------------------------------

## 18. Initial librarian algorithm

```text
1. Read task.
2. Load the compact concept catalog.
3. Resolve MATCHED and INFERRED concepts.
4. Retrieve leaves for the most specific active concepts.
5. Prefer relevant multi-concept leaves.
6. Use concept parents as bounded fallback when specific knowledge is insufficient.
7. Read retrieved LOCAL knowledge.
8. Reinterpret the task in light of that knowledge.
9. ACTIVATE newly material concepts revealed by LOCAL knowledge.
10. Repeat bounded retrieval when activation or fallback improves understanding.
11. Enumerate material task questions.
12. Classify each as KNOWN, DISCOVERABLE, INFERRED, or NEED_USER.
13. Investigate DISCOVERABLE items where practical.
14. Update coverage.
15. Ask the user only about material NEED_USER items.
16. Emit the standardized task context.
17. Expand referenced leaf bodies needed for execution.
18. Hand the expanded context to the implementation agent.
19. After work, reconcile discoveries and inferences into proposed LOCAL knowledge.
```

When the complete concept catalog becomes too large, replace step 2 with a high-recall candidate provider followed by the same semantic concept-resolution step. The rest of the algorithm SHOULD remain stable.

## 19. Design principles

1.  **LOCAL knowledge is the reason the system exists.**
2.  **The glossary records salient local vocabulary, not dictionary
    knowledge.**
3.  **Concept classification uses the same `parents` relationship as
    semantic hierarchy.**
4.  **Leaves are cohesive knowledge units, not one-record-per-fact
    objects.**
5.  **REFERENCE, RATIONALE, PRACTICE, FAILURE MODE, and CONVENTION
    describe knowledge within leaves.**
6.  **Multi-concept leaves provide intersection knowledge without a
    special intersection model.**
7.  **Knowledge about an interaction SHOULD be recorded only when it
    adds more than its component concepts already provide.**
8.  **Hierarchy expands retrieval candidates; it does not automatically
    propagate truth.**
9.  **The initial graph has only the relationships required to support
    useful behavior.**
10. **Retrieved LOCAL knowledge can activate additional concepts,
    enabling bounded iterative retrieval.**
11. **Coverage is separate from retrieval: it measures whether the task
    is sufficiently understood.**
12. **KNOWN and INFERRED MUST remain distinguishable.**
13. **DISCOVERABLE questions SHOULD be investigated before asking the
    user.**
14. **Repeated important inference or discovery is evidence of missing
    LOCAL knowledge.**
15. **NEED_USER is reserved for material questions the system cannot
    satisfactorily resolve.**
16. **The standardized task context is the librarian's proof of work and
    the coder's input contract.**
17. **Lineage lives with the leaf and points outward to detailed
    evidence when necessary.**
18. **Use deterministic `fd` + `yq` access before introducing indexes or
    retrieval infrastructure.**
19. **Validation and ontology complexity SHOULD grow from observed
    failures, not anticipated possibilities.**
20. **The knowledge base is useful only insofar as it changes or
    validates agent behavior.**

------------------------------------------------------------------------

### Additional retrieval principles

- **Concepts contain routing information; leaves contain substantive LOCAL knowledge.**
- **While practical, let the librarian see the complete compact concept catalog rather than prematurely optimizing concept retrieval.**
- **When candidate generation becomes necessary, optimize the coarse pass for recall and let semantic concept resolution provide precision.**
- **The task context is the compact proof of work; the expanded context is the task-specific LOCAL knowledge package used for execution.**

## 20. External precedents

The design borrows selected ideas without adopting a full Semantic Web
stack:

-   **SKOS**: concept labels and semantic hierarchy.
-   **BCP 14 / RFC 2119 + RFC 8174**: precise normative vocabulary.
-   **W3C PROV**: provenance and derivation as structured metadata.
-   **SHACL**: the principle that graph/schema constraints can be
    machine-validated.

The implementation remains intentionally lighter than these standards.

### References

-   W3C, *SKOS Simple Knowledge Organization System Reference*:
    https://www.w3.org/TR/skos-reference/
-   W3C, *SKOS Primer*: https://www.w3.org/TR/skos-primer
-   RFC Editor, *RFC 2119*: https://www.rfc-editor.org/info/rfc2119/
-   RFC Editor, *RFC 8174*: https://www.rfc-editor.org/info/rfc8174/
-   W3C, *PROV Model Primer*: https://www.w3.org/TR/prov-primer/
-   W3C, *Shapes Constraint Language (SHACL)*:
    https://www.w3.org/TR/shacl/
