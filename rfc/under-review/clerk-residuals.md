# Clerk residuals: learning from records and inspecting retrieval

Status: under review; extracted 2026-11-24. No behavior is adopted by this RFC.

Sources: [Clerk specification](../../graveyard/skills/clerk/clerk-specification.md) and [earlier draft](../../graveyard/skills/clerk/clerk-initial-spec.md).
Baseline: [Gerald](../../skills/gerald/SKILL.md), especially [retention](../../skills/gerald/references/retention.md) and [knowledge summary](../../skills/gerald/references/knowledge-summary.md).

Gerald replaced Clerk. Current state, question/task statuses, uncertainty, resumption, evidence-linked artifacts, and updates at meaningful changes are already covered at the selected Ret level. Clerk’s unconditional logs, code directories, and closure requirements must not be imported wholesale. Gerald’s optional knowledge summary is not a promotion pipeline.

## Residual proposals

1. **Knowledge consultation and breadcrumbs.** Consider retrieval at inquiry start, substantive method selection, unexpected evidence, and remediation review. Expose which leaves/evidence were actually read, what they contributed, and material gaps so the user can debug an answer. Avoid repeated retrieval without a reason. Clerk provides consultation triggers and the retrospective seed; the exact user-facing breadcrumb format remains to be designed.
2. **Retrieval retrospective.** Ask “What should have been retrieved here?” Distinguish missing knowledge, failed retrieval, misunderstood applicability, an unimplemented remedy, and ineffective guidance where evidence supports the distinction. Recurrence alone does not establish ignored learning. Preserve uncertainty about why an agent erred; self-explanation is not verification.
3. **Learning candidates and improvement feedback.** Derive candidate lessons and knowledge-access improvements from records, keeping them distinct from authoritative KB leaves. Use the user’s stated KB objectives and reactions to refine what deserves capture. Do not impose an additional lessons or improvement log irrespective of Ret. Decide where a downstream process stores proposals and how it records user feedback.
4. **Promotion and amendment review.** Retrieve duplicates and contradictions before proposing additions. Prefer amending an observation about the same phenomenon; explain corroboration, expanded scope, exceptions, or contradictions. Create a peer observation when the contribution is materially distinct. Do not force every investigation result into the observation category. The archived proposal requires user approval before substantive integration; formal approval, supersession, and retirement mechanics remain open.
5. **Evidence and remedial rationale.** Link reusable knowledge to the relevant record, inputs, code/configuration, and results. Gerald already requires proportionate artifact evidence; the additional reusable-remedy contract is to preserve the triggering failure, historical context, alternatives, tradeoffs, effectiveness evidence, and reassessment/retirement conditions. Distinguish proposed, adopted, implemented, and evaluated responses. Recovery need not establish a cause or permanent fix. Preserve operative safeguards pending a decision.
6. **Independent review.** Consider a fresh-context review of consequential conclusions or generalizations against supporting evidence. Activation criteria and mechanism are undecided; a separate context is not proof of independence or correctness.

## Responsibility and storage boundary

These proposals concern the downstream knowledge system, not a revived Clerk. Gerald continues to serialize work without writing or proposing KB entries. A separate process would read those records and propose reusable knowledge under an agreed mandate.

The preferred consumer-project layout is `minerva-artifacts/records/` and `minerva-artifacts/kb/`. Keep source records available as evidence; do not assume promotion means moving or deleting an entire record. Mapping Gerald’s logical project directory and any configurable roots to this layout remains an integration decision, not a change made by this RFC.

## Questions before adoption

Define the project-specific objective/mandate, feedback capture, candidate format, human review boundary, and retrieval breadcrumb format. Specify how this process respects Gerald’s actual recorded coverage and discloses missing history. No SQLite, embeddings, or autonomous bulk ingestion is required.
