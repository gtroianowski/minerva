### Bootstrap manifest

Bootstrapping begins from a persistent **manifest** supplied by the
user. The manifest is an orientation document: it describes the
bootstrapper's mandate, the corpus it should inspect, and the domains,
goals, and principles that should guide its attention.

The manifest is not itself a knowledge base and MUST NOT prescribe the
concepts or leaves that the bootstrapper is expected to discover.

The manifest SHOULD be written primarily as structured Markdown prose.
Structure SHOULD be used where deterministic interpretation is useful,
such as identifying files; prose SHOULD be used to communicate meaning,
purpose, expectations, and special cases.

#### Mandate

The manifest MUST begin with a mandate describing what knowledge the
bootstrapper is expected to collect and what future agent work that
knowledge is intended to support.

The mandate is the primary relevance test during bootstrap:

> Would understanding this materially improve the agent's ability to
> fulfill the mandate?

The mandate MAY justify investigation beyond the explicitly listed
corpus, including inspecting data, runtime behavior, or executing
probes. Such investigation SHOULD begin from a material question raised
during bootstrap rather than from unrestricted exploration.

#### Corpus

The manifest SHOULD divide its input into meaningful sub-corpora. Each
sub-corpus SHOULD normally contain:

``` markdown
### <sub-corpus title>

**Includes**

- <file pattern or prose inclusion rule>

**Excludes**

- <file pattern or prose exclusion rule>

**Description**

<what this corpus represents, why it matters, and what role it plays>

**Special handling**

<optional instructions specific to reading or investigating this corpus>
```

`Includes` and `Excludes` MAY combine filesystem patterns with prose
when patterns alone cannot adequately express the intended scope.

`Description` SHOULD explain the role of the material rather than merely
restating its file type. In particular, it SHOULD help the bootstrapper
understand how future agents are expected to use or modify the code or
knowledge represented by the corpus.

`Special handling` MAY provide additional instructions when a corpus
requires them.

For example:

``` markdown
### Core implementation

**Includes**

- `src/**/*.py`
- `jobs/**/*.py`
- Files directly imported by these paths when needed to understand their behavior.

**Excludes**

- `**/generated/**`
- `**/vendor/**`

**Description**

This is the primary implementation of the system. Future agents are expected to understand, modify, extend, and diagnose this code. Read it not merely to describe its software structure, but to identify LOCAL knowledge needed to change it without inadvertently changing its intended behavior.

**Special handling**

Pay particular attention to repeated abstractions, implicit assumptions, boundary handling, differences between historical and live execution, and implementation details that appear to encode unexplained domain knowledge.
```

#### Domains

The manifest SHOULD describe domains that are particularly relevant to
the mandate.

A domain is a **lens for discovery**, not an ontology. It explains a
family of concerns and the kinds of observations that may deserve
special attention. Examples mentioned by a domain are illustrative and
MUST NOT automatically become concepts.

For example:

``` markdown
### Temporal integrity

Calculations should be understood in terms of what information was actually available at the point in time they represent. This is particularly important when historical calculations are intended to correspond to behavior that could have occurred live.

While reading, pay attention to things such as:

- event, receipt, publication, and processing times;
- as-of joins;
- forward filling;
- rolling calculations;
- trading dates and calendars;
- train/test boundaries.

These are examples of potentially relevant phenomena, not required concepts. Discover and use the vocabulary actually supported by the corpus.
```

Domains SHOULD cause the bootstrapper to notice potentially meaningful
implementation choices. For example, a domain concerned with statistical
robustness may cause unusual handling of nulls, outliers, fat tails, or
minimum sample sizes to receive further investigation rather than being
dismissed as incidental implementation detail.

#### Goals and principles

The manifest SHOULD describe the broader goals that future agent work is
intended to advance.

Goals guide judgments about what knowledge is likely to matter but are
not ordered. If two goals materially conflict and existing LOCAL
knowledge does not resolve the conflict, the bootstrapper MUST surface
it to the user rather than inventing a priority.

Principles SHOULD be separated into:

-   a small set of **normative principles**, which constrain acceptable
    interpretations or implementations; and
-   a larger set of **illustrative principles**, which communicate
    useful ways of thinking and direct the bootstrapper's attention
    without imposing requirements.

For example, a normative principle might state:

> Historical calculations MUST NOT use information unavailable at the
> represented point in time.

An illustrative principle might state:

> Careful handling of extreme observations may encode important
> assumptions about the intended meaning of a calculation.

Illustrative principles MUST NOT be promoted into normative rules merely
because supporting examples are discovered.

#### Persistence and reconciliation

The manifest is persistent, but its primary role is bootstrapping. As
the knowledge base develops, accepted LOCAL knowledge becomes a richer
and more specific description of the system.

Before onboarding another substantial corpus, the bootstrapper SHOULD
therefore read both the persisted manifest and the existing knowledge
base and construct an **effective manifest** for the new bootstrap
operation.

During reconciliation:

-   compatible LOCAL knowledge MAY refine or expand manifest guidance;
-   specific accepted LOCAL knowledge SHOULD supersede broader
    non-normative manifest guidance for the cases it covers;
-   the original manifest SHOULD remain available as provenance rather
    than being silently rewritten;
-   contradictions MUST NOT be resolved by inventing priorities;
-   contradictions involving normative principles MUST be surfaced to
    the user before proceeding.

Conceptually:

``` text
initial bootstrap:

    manifest
       ↓
    corpus
       ↓
    knowledge base


later substantial ingestion:

    persisted manifest
          +
    existing knowledge base
          ↓
      reconciliation
          ↓
    effective manifest
          ↓
       new corpus
          ↓
    expanded knowledge base
```

The manifest therefore acts as the **bootstrap lens**, while the
knowledge base represents the accumulated LOCAL knowledge. As the
knowledge base matures, it increasingly informs how the manifest is
interpreted without eliminating the manifest's role as the user's
persistent statement of mandate, scope, goals, and principles.
