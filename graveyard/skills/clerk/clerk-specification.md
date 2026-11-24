# Clerk — initial specification

Status: concise draft for review. This is a skill specification, not an installed skill.

## Role

The clerk governs the durable record of an investigation, study, or other prolonged agent effort. It preserves enough context for an agent to resume accurately and enough evidence for a human or agent to audit conclusions. It records the work as it unfolds, including mistakes, corrections, and changes of direction.

Recordkeeping and consultation of existing knowledge are systematic duties defined by the core instructions, rather than optional activities left to the agent's initiative.

## Required investigation record

- **Question-and-answer record:** human-readable summaries of each substantive question and answer, intended for later agent rereading. Preserve clarifications, consequential assumptions, decisions, failed hypotheses, and corrections. Routine exchanges may be grouped when no material context is lost.
- **Current state:** a summary of the subject under scrutiny, the current question and scope, open questions, answered questions, conclusions, and overall work status (`pending` or `complete`). Distinguish provisional conclusions from established ones and preserve unresolved alternatives. Completion does not require resolution: record why work ended and what remains unknown.
- **Investigation code directory:** retain code used for exploration, probes, statistics, and other analysis. Keep enough context to identify relevant inputs, configuration, execution steps, and results supporting conclusions. Keep this lightweight; more elaborate reproducibility machinery is deferred until needed.
- **Lessons learned:** findings and lessons from this investigation, including mistakes made by the agent, their supporting evidence, and potential value beyond the immediate work. These remain part of the investigation record and are distinct from reusable KB leaves.
- **Improvement log:** accumulate possible improvements to knowledge capture, discovery, interpretation, and use; consolidate these into a small set of suggestions at closure.

Update the current state at material findings, changes of hypothesis or scope, consequential user clarifications, and handoffs. Preserve uncertainty through summaries: an inferred explanation must not become a verified cause merely through repetition or compression.

## Systematic interplay with the librarian

Consult the librarian at the start of an investigation, when selecting a substantive method, when unexpected or contradictory evidence changes the inquiry, and when proposing a remediation or consolidating learning. Retrieve relevant facts, procedures, principles, observations, and similar incidents. Scale each consultation to the work; avoid repeatedly retrieving unchanged material without a reason.

During retrospective review, explicitly ask **“What should have been retrieved here?”** Record relevant knowledge that was available, whether it was retrieved, and whether it was correctly understood and applied. Where the evidence supports it, distinguish missing knowledge, failed retrieval, misunderstood applicability, an unimplemented remedy, and ineffective guidance. Recurrence alone does not establish that existing learning was ignored. Record uncertainty when the reason cannot be established.

The librarian supplies reusable knowledge throughout the work. The clerk supplies the evidence and context from which new leaves or amendments can be proposed:

- Situated findings and experienced outcomes may contribute to **observation** leaves.
- Newly established descriptive knowledge may contribute to **fact** leaves, with the appropriate subtype.
- Safeguards, workarounds, and recovery methods introduced in response to a failure may contribute to **procedure / remedial** leaves.
- Theoretical learning and newly encountered techniques may contribute to facts, principles, or procedures according to their role. Do not classify everything as an observation merely because it arose during an investigation.

## Consolidating observations and proposing KB changes

Keep the question log, current state, investigation lessons learned, and proposed KB changes distinct. Preserve the investigation as a chronological record; a reusable leaf does not replace it. New leaves and substantive amendments are subject to user approval before integration.

Before proposing a new observation, retrieve and read related observations. An observation should synthesize the situation or phenomenon it describes, with explicit scope and supporting evidence; it need not correspond one-to-one with an incident.

Prefer amending an existing observation when new evidence concerns the same underlying phenomenon. Explain whether the evidence corroborates the synthesis, expands its demonstrated scope, introduces an exception, contradicts it, or challenges its explanation. Do not broaden a claim beyond what the combined evidence supports. Propose a separate observation when the situation or reusable contribution is materially different, and explain the relationship.

For each proposed addition or amendment, identify the supporting investigation material and the substantive change. Preserve links to relevant cases and explain their relationship in plaintext. Structured relationships and PROV integration are deferred.

Distinguish observed behavior, inferred explanations, and verified causes. An agent's account of why it made a mistake is a candidate explanation, not verification. Check proposed learning against available evidence, and ask the librarian to identify duplicates, contradictions, and suitable existing leaves before approval.

## Operational memory and remedial procedures

An investigation can produce valuable operational memory without eliminating the underlying source of uncertainty. Documenting how to recognize and recover from a recurring problem can be appropriate while a strategic fix remains deferred. Do not equate successful learning with implementing a permanent change.

The investigation's lessons learned record what was learned in that effort. A remedial procedure records the reusable response, safeguard, or solution being proposed or evaluated. Distinguish its state: proposed, adopted, implemented, and evaluated are not interchangeable. State the evidence for its effectiveness and any remaining uncertainty.

When proposing a remedial procedure, supply material for a **“Why we did it this way”** section covering:

- The triggering failure and affected conditions.
- The historical, temporal, or code context that mattered to the decision.
- The chosen response, rejected alternatives, and relevant tradeoffs or maintenance costs.
- The evidence supporting the response and conditions that would justify reassessment or retirement.

Record this rationale so future agents can understand why the system is configured that way and avoid removing a necessary safeguard during refactoring. Preserve operative safeguards pending an appropriate decision; documenting their purpose does not make them permanent.

## Closure and handoff

At closure or handoff, synchronize the current state, consolidate lessons and improvement suggestions, and identify proposed KB additions or amendments awaiting approval. Distinguish conclusions reached, operational responses documented, changes proposed or implemented, and effectiveness actually evaluated. Keep unresolved questions visible.

## Responsibility boundary

The clerk governs recordkeeping, continuity, and systematic capture of learning. The investigator governs the inquiry and evidential standards. The librarian governs discovery and reusable knowledge organization. These are complementary responsibilities, not necessarily three separate agent processes.

## Open design questions

- **Independent reviewer:** consider reviewing conclusions and proposed learning in a separate context with clean instructions and access to the supporting evidence. This may reduce anchoring and self-justification; a fresh context does not itself guarantee independent or correct judgment.
- **Formal lifecycle:** detailed approval, promotion, amendment, supersession, and retirement mechanisms remain to be designed.
