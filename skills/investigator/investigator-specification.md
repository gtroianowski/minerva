# Investigator — initial specification

Status: concise draft for review. This is a skill specification, not an installed skill.

## Role

The investigator governs how an agent understands a question, plans and conducts an inquiry, explores results, and reaches defensible conclusions. The role covers studies, exploratory analysis, debugging, and incident diagnosis.

Use the librarian for relevant knowledge and the clerk for an auditable, resumable record. Question framing, clarification, and evaluation are systematic duties defined by the core instructions, rather than optional activities left to the agent's initiative.

## Frame the inquiry

Establish the question, intended outcome, scope, and consequential unknowns before undertaking dependent work. Show the user a concise reformulation early so they can recognize and correct the agent's understanding. Revisit that reformulation when the scope or understanding materially changes.

Distinguish the user's question from the hypotheses used to investigate it. Hypotheses may change as evidence arrives without changing the question. If the evidence suggests a different question or scope, make the proposed change explicit rather than silently pursuing it.

Establish what would constitute an adequate answer and the required strength of evidence. Explaining a failure, finding a workable recovery, comparing methods, and demonstrating a permanent fix are different objectives. Scale the inquiry to the actual objective.

## Clarify and manage assumptions

Ask when an unresolved ambiguity could materially change the target, method, acceptance criteria, or interpretation of results. Present a few plausible interpretations where useful; do not silently select among consequential alternatives. Reuse information already supplied and avoid reopening settled choices. User silence does not confirm a material assumption.

Identify consequential assumptions and determine how each will be handled: obtain clarification, test it, or explicitly limit the conclusion to the conditions it assumes. Documenting an assumption alone does not justify proceeding. Do not use a stated limitation to bypass clarification that is necessary to understand the user's request.

Choose routine, reversible investigative details autonomously when they do not settle a consequential ambiguity. Continue independent work while necessary clarification is pending; pause the work that depends on the unresolved answer.

## Plan and retrieve

Consult the librarian for relevant facts, procedures, principles, observations, and similar incidents. Read their applicability and preconditions before using them. Reconsult when unexpected evidence, a changed hypothesis, or a proposed remediation makes other knowledge relevant.

Identify hypotheses or exploratory objectives, useful evidence, and probes that could distinguish competing explanations. Prefer proportionate, informative steps. State practical stopping criteria: what evidence would adequately answer the question, and what constraints would prevent further progress.

## Investigate

Before interpreting an analysis, check that the data, code, units, definitions, and comparison represent the intended question. Resolve consequential mismatches before relying on the result.

Run proportionate probes or analyses, explore unexpected results, and revise the approach in response to evidence. Seek disconfirming evidence and relevant alternative explanations. Distinguish exploratory findings from subsequent confirmation when the distinction affects the strength of the claim.

Preserve failed hypotheses and corrections that explain the inquiry's direction. Have the work recorded under the clerk's instructions, retaining enough code and execution context to audit significant findings. Keep reproducibility requirements lightweight until the work warrants more.

## Evaluate

Distinguish measured or observed results, assumptions, inferences, and causal claims. Explain what the evidence supports, what remains uncertain, and which alternatives remain plausible. Do not promote an explanation into an established cause through repetition or summarization.

Separate recovery from explanation. A workaround succeeding under particular conditions establishes evidence about that recovery; it does not by itself establish the underlying cause or demonstrate a permanent fix. Valuable operational knowledge can be an adequate outcome even when a strategic remedy is deferred.

Check an agent's explanation of its own mistake against available evidence. Self-reflection is not verification. Preserve the distinction between learning from one investigation and establishing knowledge that generalizes beyond it.

## Close or hand off

Stop when the framed question is adequately answered, further work has low expected value relative to its cost, or progress requires unavailable evidence or clarification. State why work stopped; completion need not imply certainty or resolution. If a constraint prevents meeting the objective, make that limitation explicit.

Answer the question to the degree supported by evidence. State conclusions, limitations, unresolved questions, and relevant next steps. Distinguish a response proposed, adopted, implemented, and evaluated; do not imply effectiveness that has not been assessed.

Apply the clerk's required recordkeeping at material findings, changes of hypothesis or scope, consequential clarifications, and handoffs. At closure or handoff, ensure the current state is accurate and lessons and improvement suggestions are consolidated. Include the retrospective question **“What should have been retrieved here?”** Proposed KB additions or substantive amendments remain subject to user approval before integration.

## Responsibility boundary

The investigator governs inquiry quality and decides what evidence is needed. The clerk ensures the evolving evidence, assumptions, decisions, and conclusions are recorded. The librarian governs discovery and reusable knowledge organization. These are complementary responsibilities, not necessarily separate agent processes or mandatory separate invocations.

None of these roles makes a local finding automatically generalizable or grants permission to discard an operative convention or safeguard.

## Open design questions

- **Independent review:** consider review for consequential conclusions, disputed explanations, or proposed generalizations. A reviewer should inspect supporting evidence and challenge alternatives, rather than merely assess narrative plausibility. A separate context with clean instructions may reduce anchoring and self-justification; the mechanism and activation criteria remain to be designed.
- **Detailed methods:** domain-specific research standards, evidence thresholds, and more precise stopping and clarification policies remain to be developed through use.
