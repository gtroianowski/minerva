# Clerk — initial raw specification

Status: concise draft for review. This is a skill specification, not an installed skill.

## Role

The clerk governs the durable record of an investigation, study, or other prolonged agent effort. It preserves enough context for an agent to resume accurately and enough evidence for a human or agent to audit conclusions. It sees the work as it unfolds, including mistakes and corrections.

## Required investigation record

- **Question-and-answer record:** human-readable summaries of questions and answers, intended for later agent rereading. Preserve clarifications, decisions, and corrections.
- **Current state:** a summary of the subject under scrutiny, open questions, answered questions, conclusions, and overall status (`pending` or `complete`). Keep this synchronized with the work; distinguish provisional conclusions from established ones.
- **Investigation code directory:** retain code used for exploration, probes, statistics, and other analysis so results and conclusions can be audited.
- **Lessons learned:** individual findings and lessons, including mistakes made by the agent, with their evidence and potential value beyond this investigation.
- **Improvement log:** accumulate possible improvements to knowledge capture, discovery, and use; consolidate these into a small set of suggestions at the end.

## Interplay with the librarian

The librarian supplies relevant facts, procedures, principles, observations, and similar incidents throughout the work. The clerk preserves what was learned and proposes reusable leaves for the librarian to integrate:

- Situated results, incidents, and experienced outcomes usually suggest **observation** leaves.
- Newly established descriptive knowledge suggests **fact** leaves, with the appropriate subtype.
- Safeguards and workarounds introduced because of a failure suggest **procedure / remedial** leaves. Record their purpose so later agents can understand why the system is configured that way and avoid removing a necessary safeguard.
- Theoretical learning and newly encountered techniques may suggest facts, principles, or procedures according to their contribution; do not classify everything as an observation merely because it arose during an investigation.

Ask the librarian about similar incidents. When relevant learning already exists, investigate why it did not prevent or shorten this incident. Record the finding and possible improvements to knowledge accessibility.

## Proposed refinements for review

- Preserve the investigation as a chronological evidence record; create distinct reusable leaves with links back to it. A leaf is not a compressed substitute for the investigation record.
- Summarize each substantive question and answer; batch routine exchanges when no material reasoning or decision would be lost. Preserve failed hypotheses and corrections that explain the final result.
- Retain enough execution context to audit code-based findings: input identity/version, relevant configuration, how to run the analysis, and the outputs or results supporting the conclusion. A code directory alone may be insufficient.
- Distinguish observed behavior, inferred explanation, and verified cause. Preserve uncertainty and alternative explanations.
- Recurrence prompts diagnosis of missing knowledge, failed retrieval, misunderstood applicability, an unimplemented remedy, or ineffective guidance. Do not presume that knowledge was ignored.
- For remedial leaves, record the triggering failure, affected conditions, and evidence that would justify reassessment or retirement. Keep operative safeguards in force pending an appropriate decision.
- Consolidate candidate lessons during the work and at closure; ask the librarian to check for duplicates, contradictions, and suitable existing leaves before integration. Formal promotion and retirement rules remain to be designed.

## Responsibility boundary

The clerk governs recordkeeping and continuity. The investigator governs the inquiry and evidential standards. The librarian governs discovery and reusable knowledge organization. These are complementary responsibilities, not necessarily three separate agent processes.
