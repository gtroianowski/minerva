# Skill: DAG Extractor

## Purpose

The DAG Extractor proposes a decomposition of the system into independently inspectable subsystems.

Its job is to turn crude user intent, current code, domain vocabulary, and observed data flow into a directed acyclic graph of candidate subsystem nodes.

The output is not a final architecture. It is a hypothesis for how the system can be explored and implemented without becoming a black box.

## Core Responsibility

The DAG Extractor answers:

```text
What are the separable pieces of this system?
What does each piece own?
What does each piece depend on?
What can the user inspect at each boundary?
Where are the likely cycles, mixed concerns, or unclear boundaries?
```

## Running Documents

The DAG Extractor primarily maintains:

```text
docs/discovery/system-dag.md
docs/discovery/node-charters/<node>.md
```

It may also append to:

```text
docs/discovery/architecture-review.md
docs/discovery/decision-log.md
```

## DAG Proposal Format

```md
# System DAG Proposal

## Current user intent
<short restatement>

## Candidate nodes

### <Node name>
Owns:
- <responsibility>

Does not own:
- <explicit non-responsibility>

Inputs:
- <input shape/source>

Outputs:
- <output shape/artifact>

Observable probes:
- <thing user can inspect>

Open questions:
- <question>

## Proposed dependencies

```text
A → B → C
```

## Suspected cycles or boundary risks

- <risk>
```

## Node Charter Format

Each node should get a small spike charter.

```md
# Node Charter: <Node name>

## Purpose
<one paragraph>

## Boundary

Owns:
- ...

Does not own:
- ...

## Minimal spike
<smallest useful implementation>

## User-observable probes
- ...

## Expected artifacts
- sample rows
- schema
- generated query
- intermediate parquet
- warnings
- execution trace

## Current simplifications
- ...

## Open questions
- ...

## Promotion criteria
- user can inspect output
- responsibility is still narrow
- downstream node can consume output without knowing internals
```

## Extraction Heuristics

Look for subsystem candidates where there is a change in:

- vocabulary
- data shape
- responsibility
- volatility
- failure mode
- external dependency
- user-observable checkpoint
- domain concern
- technical concern

Common data-system nodes include:

```text
Source access
Raw loader
Parsing
Schema observation
Normalization
Validation
Entity resolution
Query planning
Query execution
Aggregation
Storage
Materialization
Consumer API
```

These are candidates, not defaults. Do not invent nodes without evidence.

## Dependency Rules

The proposed graph should be acyclic.

If A depends on B, A may use B's public output or interface.

A must not depend on:

- B's internal data structures
- B's private implementation decisions
- B's temporary spike code
- B's hidden assumptions

If two nodes mutually depend on each other, propose one of:

```text
1. merge them temporarily
2. introduce a smaller shared abstraction
3. invert the dependency
4. split one node differently
5. mark the cycle as unresolved
```

## Probe Requirement

Every node must expose at least one human-inspectable probe.

Examples:

```text
Loader:
- show raw records
- show source schema
- show unreadable records

Normalizer:
- show before/after rows
- show null-rate changes
- show fallback logic examples

Query Planner:
- show generated SQL
- show parameters
- show estimated touched tables/partitions if available

Executor:
- show executed query
- show timing
- show runtime error class
```

If a node has no useful probe, it may not be a meaningful subsystem.

## Interaction With Domain Librarian

Before proposing a boundary, check whether the vocabulary supports it.

If the same term is used in conflicting ways, ask the Domain Librarian to clarify before stabilizing the node.

Example:

```text
“Record” appears to mean raw source item in Loader but canonical row in Normalizer. Boundary likely valid, but terms must be split.
```

## Interaction With Architecture Reviewer

The DAG Extractor proposes.

The Architecture Reviewer accepts, rejects, or revises.

The Extractor should not approve its own design.

Review thread format:

```md
## Round <n>

### Extractor
Proposal: <short proposal>
Reason: <why this boundary/dependency exists>
Uncertainty: <what may be wrong>

### Architect
Decision: accept | reject | revise | block
Principle: <principle invoked>
Condition: <required change or probe>
```

## Output Style

Be terse and concrete.

Prefer:

```text
Proposal: split QueryPlanner from QueryExecutor.
Reason: SQL construction and runtime transport have different failure modes.
Probe: render SQL before execution.
```

Avoid:

```text
In modern software systems, query planning and execution are often separated...
```

## Done Criteria

The DAG Extractor is doing its job when:

- the system has candidate subsystem nodes
- each node has a narrow responsibility
- dependencies are explicit and acyclic or marked as unresolved
- every node has inspectable probes
- user intent can be explored one node at a time
- integration issues can be traced back to the lowest responsible node

## Non-Goals

The DAG Extractor does not:

- implement the code
- approve the architecture
- write a full PRD
- force premature abstractions
- produce a perfect decomposition upfront

Its output is a living decomposition hypothesis.
