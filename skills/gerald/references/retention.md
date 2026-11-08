# Maintained records — Ret2 and above

Keep records concise and distinguish user requirements, agreed decisions, proposals, assumptions, and observations. Retention controls continuity coverage; it does not itself require greater rigor or closure. Use the destination rules in [storage.md](storage.md). Gerald does not write to the KB or propose KB entries.

## State of things

Maintain a mutable, human-readable `<project-directory>/records/<record-slug>/state-of-things.md`, organized for humans and agents alike. Make it understandable without consulting the inquiry log. Include the general topic and a concise conversation summary: purpose, important context, direction, and substantive decisions or changes of direction. Keep this account **current** and **concise**; it reflects the state of things rather than the path that led to it. 

Let Ret determine how much state must persist, and let the other scores shape its contents: breadth determines scope, depth the explanatory detail needed, rigor the evidence and uncertainty, and closure the completion criteria and unfinished obligations. At Ret2, a topic and summary suffice; higher scores in other dimensions do not silently raise Ret. If their needs cannot be met by the selected retention, surface the mismatch.

At Ret3 and above, track in-scope tasks and questions whose resolution matters to the outcome, decisions, or resumption of work. Exclude temporary reasoning steps unless they reveal a material issue. Include the current framing, scores, constraints, and completion criteria where applicable.

For each task or question, maintain a stable identifier, current status, a concise current answer or outcome where available, and the next action or blocker where needed. Use these statuses as applicable:

- **Open:** Still requires an answer or action.
- **In progress:** Work is underway.
- **Answered/completed:** Has an answer or result; link supporting evidence or artifacts as needed at the chosen rigor.
- **Blocked:** Cannot proceed; identify the missing input or dependency.
- **Closed by user:** The user explicitly marked it done or waived further work. Preserve any partial answer and unresolved uncertainty; do not relabel it as answered.
- **Excluded/deferred:** Outside the current scope or postponed; record the reason and whether the user agreed or the change is merely proposed.

Update answers, decisions, scope, and statuses as they change. Reopen an item if later evidence invalidates its answer.

At Ret3 and above, identify unfinished work at pauses, handoffs, and closure. The closure score governs the obligation to finish; the record must still show remaining questions even when the exchange can legitimately stop.

## Artifacts

Choose artifact formats suited to their intended use. At Ret2 and above, reference consequential artifacts from `<project-directory>/records/<record-slug>/state-of-things.md`. Preserve the relevant inputs, methods, conditions, and limitations to the extent required by rigor and the artifact's intended use. Link rather than duplicate artifact contents.

## Resumption in every mode

When retention exists, make every mode resumable to the extent supported by the selected Ret. On resumption, read the existing records and relevant linked artifacts; recover the framing, mode and stage, decisions, questions, and outstanding work they actually preserve. Identify material gaps without inventing history or treating superseded targets as active. Do not require a separate handoff document or detailed plan for every mode. Use the same records across stage changes, and update them within the chosen Ret coverage before pauses or handoffs.

## Maintenance and pushback

Reuse existing records for the same work, use the standard filenames for the selected Ret level, and state the chosen location once. Do not introduce additional structure without a practical need.

Update documents at meaningful changes and before handoff or closure. If work resumes after a knowledge summary, flag when later findings affect it and offer an update at the next closure; revise it on the user's explicit request or acceptance.

When Ret increases, establish newly required documents or sections from available evidence and identify gaps in historical coverage. Do not invent missing history. After a confirmed Ret reduction, stop maintaining only the documents or sections no longer required and preserve the reduction's date and consequences in the remaining state document, or in the conversation at Ret1. Keep the change in the inquiry log if one exists, even when ongoing log maintenance ends.

If the selected documents cannot support the expected continuity or review, explain the gap and propose a different Ret score. Honor the user's override. If persistent storage is unavailable or a write fails, report the limitation and preserve the available notes in the conversation for recovery; do not claim that they were saved elsewhere.
