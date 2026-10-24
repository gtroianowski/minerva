# Knowledge and investigation system — general directions

Status: concise direction-setting draft, capturing this discussion. Suggestions are distinguished from the user's proposed design.

## Direction

Start creating leaves using the current librarian authoring design. Keep entries flat and organize knowledge through metadata and links. More structured relationships may become useful as real investigations expose recurring needs; do not require a complete ontology before beginning.

An outage, for example, can produce a new fact about a data system, a situated observation about the incident, an explanation connecting the two, and a remedial procedure. Preserve their distinct roles and the relationships between them.

## Complementary skills

| Role | Primary responsibility | Supplies to the others |
| --- | --- | --- |
| Librarian | Retrieve, interpret, and organize reusable knowledge | Facts, procedures, principles, observations, and similar incidents |
| Clerk | Preserve the evolving investigation and its evidence | Resumable context, audit material, lessons, and knowledge-access improvements |
| Investigator — proposed name | Govern question framing, clarification, inquiry, and conclusions | A disciplined inquiry whose evidence and learning can be recorded and reused |

The librarian feeds the investigation with existing knowledge. The clerk sees the steps, outcomes, and mistakes and supplies candidate learning back to the librarian. The investigator governs how the question is understood and studied. These responsibilities can be enacted by one agent or several; deployment structure is not decided.

## Clerk record and knowledge capture

Maintain question/answer summaries, a current-state document with open and answered questions and pending/complete status, investigation code, individual lessons, and a running improvement log. Consolidate suggestions at closure.

Lessons may become observations; discovered facts and theoretical learning may yield other categories. Remediations belong to the existing **procedure / remedial** category. Capture why each safeguard exists so future investigations can explain it and future refactors can preserve its purpose.

Retrieve similar incidents. Repeated problems are useful evidence about whether knowledge is discoverable, understood, applicable, and acted on. Proposed refinement: diagnose these possibilities rather than infer that recurrence alone proves ignored learning.

## Tooling direction

Provide Python and/or Rust scripts as the librarian's routine interface to the Markdown corpus. Initial capabilities include:

- Load one canonical leaf.
- Return titles or metadata for leaves matching a filter.
- List titles, categories/subcategories, and age computed from recorded metadata.
- Extract links for inspection and navigation.

The files remain authoritative. Proposed refinement: scripts should parse, select, and report deterministically; agents should judge semantic relevance, applicability, evidential meaning, and classification. The exact CLI and output schema are a later design task.

## Relationship direction

Begin with ordinary links and prose explaining their meaning. Likely future relationships include incident-to-fact, explanation-to-evidence, remediation-to-failure, and lesson-to-investigation. These are examples for exploration, not adopted relation types.

Proposed refinement: distinguish a factual observation from an inferred explanation or verified cause. Preserve links from reusable leaves to the investigation evidence, and record what would justify changing a remedy. Decide which relationships deserve machine-readable structure after practical use shows a retrieval or reasoning benefit.

## Next design topics

Review the concise clerk and investigator drafts; refine the clarification threshold and record format; implement the small corpus tools; then use real investigations to improve templates, relationships, and retrieval. Formal promotion, conflict precedence, retirement, and structured relation schemas remain open.
