# Discovery-Gated Agent System Skills

This folder defines three cooperating skills for an AI-assisted coding workflow where architecture emerges through small, inspectable prototypes rather than through a large up-front PRD.

The three skills are:

1. **Domain Librarian**  
   Maintains the shared vocabulary between user, code, data, and agent.

2. **DAG Extractor**  
   Proposes a decomposition of the system into independently inspectable subsystems and dependencies.

3. **Architecture Reviewer**  
   Reviews the proposed subsystem DAG and implementation changes against architectural principles.

The skills are meant to interact through running markdown documents, not long freeform chat. Each skill should write terse, auditable notes that the user can skim and interrupt.

## Core Loop

```text
User intent
  ↓
Domain Librarian clarifies vocabulary
  ↓
DAG Extractor proposes subsystem graph
  ↓
Architecture Reviewer accepts / rejects / revises boundaries
  ↓
One subsystem spike is implemented
  ↓
User inspects probes/checkpoints
  ↓
Vocabulary, DAG, and architecture notes are updated
  ↓
Small code changes continue
```

## Recommended Repo Structure

```text
docs/
  discovery/
    domain-glossary.md
    system-dag.md
    architecture-review.md
    decision-log.md
    node-charters/
      loader.md
      normalizer.md
      planner.md
      storage.md
```

## Invariant

The system should grow through small, inspectable semantic changes.

No agent may perform a large rewrite or introduce broad abstractions unless the current behavior is already observed, documented, and preserved.
