# Knowledge Classification and Agent Treatment

**Status:** Provisional design agreement  
**Date:** 2026-10-23  
**Purpose:** Define a small, stable vocabulary for classifying knowledge in an agent-readable Markdown knowledge base, and specify how that classification should influence agent skepticism and behavior.

## 1. Core model: three distinct dimensions

A leaf's classification serves three related but distinct purposes:

1. **Category / subcategory — what kind of knowledge is this?** A closed set of four top-level types; only Fact and Procedure currently have subtypes.
2. **Skepticism — what should an agent question?** Not a single trust score. Distinguish whether the statement remains true, whether its assumptions and context still apply, and whether a prior choice or remedy should be revisited.
3. **Expected treatment — what should an agent do with it?** Use it as a foundation, check ongoing validity, exercise judgment, follow a method, or interpret it as situated evidence.

The classification **informs** agent behavior; it does not replace reading the leaf or reasoning about the task.

## 2. Classification matrix

| Category | Subcategory | Definition / basis of validity | Skepticism: what to question | Expected agent treatment |
|---|---|---|---|---|
| **Fact** | **Analytical** | Self-contained, established knowledge grounded in definitions, mathematics, logical consequences, or sufficiently stable laws of nature | Primarily assumptions and applicability, not the underlying result | Treat as a durable conceptual foundation; apply only when its premises hold |
| **Fact** | **Metastable** | A relatively stable empirical, technical, or institutional fact that could change | Whether the recorded claim still holds, especially after relevant external change | Treat as provisionally stable; verify when age, context, or counterevidence warrants it |
| **Procedure** | **Structural** | A method dictated by constraints, mechanics, an external interface, or protocol | Whether those underlying constraints have changed | Follow the prescribed mechanics while valid; verify against the actual system when warranted |
| **Procedure** | **Conventional** | A chosen and adopted way of doing something among viable alternatives | Whether the choice remains adopted or is due for reconsideration | Respect the operative convention; do not silently substitute another merely because it seems preferable |
| **Procedure** | **Established pattern** | A reusable solution or method with a rationale drawn from accumulated design or practical experience | Whether the problem fits the pattern and the tradeoffs remain appropriate | Adapt intelligently rather than apply mechanically |
| **Procedure** | **Remedial** | A method introduced to address a particular failure, risk, or past issue | Whether the original failure mode and remedy remain relevant | Preserve the safeguard while it is operative; flag possible obsolescence for review |
| **Principle** | — | A durable conceptual lens, framework, or generalizable guiding idea that helps structure interpretation or choice | Relevance, assumptions, competing principles, and limitations—not ordinarily the existence of the principle itself | Use as a reasoning tool with discernment, not as an infallible recipe or automatic command |
| **Observation** | — | A depiction of an aspect of the world: an event, empirical finding, experienced outcome, incident, or localized behavior | Quality of evidence, circumstances, generalizability, and present relevance | Preserve as situated evidence; do not automatically elevate it to a universal rule |

**The four top-level categories are intentionally closed:** `fact`, `procedure`, `principle`, `observation`. Adding categories or subcategories should require an explicit schema decision, not casual authoring.

## 3. Definitions and boundaries

### Fact

A **Fact** is intended to be self-contained: it establishes *what something is*, or what follows from stated assumptions. It is not where we decide *when* to deploy a method.

- **Analytical:** The Huber loss definition, mathematical properties of linear models, or the Black–Scholes result under its assumptions. For this operational taxonomy, very stable physical laws may also be treated as analytical, without making a strict philosophical claim that they are a priori.
- **Metastable:** FIX protocol semantics for a specified version, a stable software interface, or an established market schedule. Their continued validity is an empirical or institutional expectation, not a logical necessity.

Example boundary: **what the Huber method is** is Fact; **when it is a sensible choice** belongs primarily in Principle or an Established pattern; **how to perform the estimation** belongs in Procedure; **what happened when it was used on dataset X** is Observation.

### Procedure

A **Procedure** answers **“How do I do X?”** It may be exact and reproducible, based on an adopted choice, or a flexible method requiring adaptation. Its subtype principally describes **why the method applies and what sustains it**, not simply how strict it sounds.

- **Structural:** The mechanics required to submit an order through a specific exchange interface or satisfy a protocol.
- **Conventional:** An adopted CLI approach using Tyro, a team's selected deployment workflow, or a project's chosen asynchronous architecture. The alternative could be valid elsewhere; switching may be costly.
- **Established pattern:** A Gang of Four design pattern or other reusable solution with identifiable use cases and tradeoffs.
- **Remedial:** A special validation step introduced after an outage, or a tactical workaround for a known filesystem defect.

These subtype boundaries can overlap. A remediation may become a team convention, and a pattern may be mandated by an architecture. For now assign the **primary justification** and explain secondary aspects in prose; do not multiply labels to model every overlap.

Procedural validity depends on different things: structural constraints still holding; a convention still being adopted; a pattern fitting the actual problem; or a remedial procedure still addressing a relevant failure mode. There is **no universal lifetime ranking** among these subtypes.

### Principle

A **Principle** is a generalizable, often synthetic, statement that provides an interpretive or decision-making framework. It may advocate an approach, explain why it helps, or simply offer a useful conceptual lens. It remains meaningful even when another approach is selected.

Examples include separation of concerns, principles from Agile or XP, mathematical duality as a lens, or the idea that misaligned incentives can create systemic risks. In programming, favoring single ownership is a principle; specific `std::unique_ptr` construction steps form a procedure.

A good principle explains **what it illuminates or advocates, why, and its limitations or tradeoffs**. Principles are typically durable as ideas, even as their relevance in a particular situation changes. They must not be treated as mechanically binding recipes.

### Observation

An **Observation** records **what the world exhibited** under identifiable circumstances, ranging from history to localized technical behavior. It is not defined by low credibility.

Examples: the global financial crisis and its aftermath; the outcome of an outage; a reproducible bug arising from a network filesystem's deviation from expected POSIX behavior; an experiment in which one estimator improved results on a particular dataset.

An observation may be highly reliable as a historical record while providing only limited grounds for generalization. The event does not become untrue with age; its bearing on today's decisions may decline. Observations may inspire principles or procedures, but neither promotion is automatic.

## 4. Skepticism is multidimensional

Avoid a single numeric “skepticism level.” At minimum distinguish:

- **Truth stability:** Is the underlying claim expected to remain true? Analytical facts are exceptionally stable within their premises; metastable facts can become outdated. Historical observations remain historical claims, though their evidence can be challenged.
- **Applicability:** Do the assumptions, context, version, problem shape, and constraints match the present request? This question matters even for perfectly stable facts and principles.
- **Need for reassessment:** Is an adopted choice, workaround, or operational method worth revisiting because of age, changed conditions, evidence, or a scheduled review?

These questions can move independently. An old mathematical fact may remain true but not apply; an old outage account remains historically relevant but its workaround may have outlived its purpose. Skepticism permits an agent to **flag, verify, or seek clarification**, not silently disregard an operative requirement.

## 5. Record age and optional review trigger

Every leaf can carry a **recorded date** to provide temporal context. The retrieval manifest can compute and expose the leaf's age. An optional **revisit date** explicitly requests reassessment of potentially changing content or choices.

```yaml
---
title: CLI argument parsing
description: Adopted approach to argument parsing in this project
type: procedure
subtype: conventional
recorded: 2026-10-23
revisit: 2027-04-23
---
```

Other valid examples include `type: fact` with `subtype: analytical` or `subtype: metastable`, and `type: principle` or `type: observation` without a subtype.

A retrieval result might expose:

```yaml
title: CLI argument parsing
type: procedure
subtype: conventional
age_days: 183
revisit_due: true
```

**Semantics:**

- `recorded` is **when the knowledge was captured**, not necessarily when it became true or was last verified.
- `age_days` is retrieval-time context, not proof of obsolescence.
- `revisit` is a **review prompt, not an expiration date**. When due, the agent should reconsider continued applicability or flag it for review, not automatically revoke the choice.
- Type and subtype influence the agent's interpretation of age; **do not hardcode freshness deadlines by category**.
- A verified change to a convention or protocol may matter far more than an arbitrary age threshold.

## 6. Illustrative classification of one subject

For the same topic, different statements belong to different categories:

| Statement | Classification |
|---|---|
| The Huber loss has a specified mathematical form and associated properties. | Fact / Analytical |
| A particular FIX version defines specified message sequencing behavior. | Fact / Metastable |
| Robust estimators can reduce sensitivity to extreme observations, subject to tradeoffs. | Principle |
| Fit the Huber estimator by following specified computational steps. | Procedure / Structural or Established pattern, depending on whether the leaf describes required mechanics or a reusable method |
| This team uses estimator X for reporting to maintain system compatibility. | Procedure / Conventional |
| We introduced a validation check after missing observations caused erroneous output. | Procedure / Remedial, if describing the required check |
| In last quarter's dataset, Huber estimation reduced an identified error measure. | Observation |

The classification follows **the claim's role**, not its domain. A single subject may generate leaves of several types.

## 7. Authoring and agent guardrails

1. **Choose the primary category for the leaf's main purpose.** Do not require every sentence to belong to that category; strict leaf homogeneity and granularity are deliberately unresolved.
2. **Use prose for reasons and boundaries.** State assumptions, justification, limits, and the conditions that would invalidate or motivate revisiting a method.
3. **Keep facts distinct from advice.** Defining a method does not establish that the method should be used in a particular context.
4. **Keep principles distinct from commands.** A useful lens is not automatically a requirement.
5. **Keep observations distinct from generalizations.** A local event may motivate a stronger claim but does not itself establish it.
6. **Do not equate skepticism with permission to override.** The agent may surface concerns or contradictions; it should not silently replace an adopted procedure or remove a safeguard.
7. **Avoid inflated structure.** Subtypes are intentionally limited, and skepticism/expected treatment are primarily semantics derived from classification rather than additional numeric metadata fields.

## 8. Explicitly deferred decisions

This document is **about knowledge classification and treatment**, not the whole knowledge-base architecture. The following remain open:

- Scope and how it is encoded or inherited.
- The ideal size or homogeneity of leaves.
- Typed versus prose-explained links (current preference: prose and ordinary Markdown links).
- Conflict resolution and precedence (current preference: surface contradictions for user judgment, then document resulting distinctions).
- Formal knowledge promotion, modification, or retirement workflows.
- Quantitative retrieval and classification testing, although inverse testing through known-answer questions and retrieval manifests is a promising direction.

**Design principle:** Add metadata or classification structure only when it enables reliably different retrieval, interpretation, or agent behavior. Maintain a small, inspectable Markdown corpus rather than inventing a large ontology upfront.
