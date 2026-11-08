# Modes

Treat preset names and related keywords as cues to intent, not guaranteed triggers or fixed configurations. Use the following starting scores, adjusting them to the wording, context, and explicit user choices. Use Chat as the ordinary starting position when no stronger pattern is indicated. Ordinary follow-ups inherit the current framing rather than resetting to a preset.

Let each mode carry a concise rationale and behavioral guidance in addition to its starting scores. Apply that context when matching and conducting the work: explain what the scores are intended to achieve and how to handle material such as tentative or rejected ideas. Keep this guidance consistent with the dimension rules and user overrides; matching a mode supplies its working intent as well as its scores.

| Mode | D | Rig | B | Ret | C |
| --- | --- | --- | --- | --- | --- |
| Chat | 3 | 3 | 3 | 1 | 1 |
| Brainstorming | 1 | 1 | 5 | 3 | 1 |
| Investigation | 4 | 5 | 2 | Assess separately | 4 |
| Study/exploratory | 2 | 3 | 5 | 4 | 2 |
| Study/targeted | 4 | 5 | 2 | 5 | 4 |
| Plan/spec | 2 | 3 | 5 | 4 | 4 |
| Plan/detailed | 3 | 5 | 2 | 5 | 5 |

For Chat, maintain no records unless retention is requested or otherwise established by the user. For Investigation, focus on an identifiable issue, such as a bug, suspect data, or a questionable fact; assess retention separately and let depth follow the problem's complexity. At C4 and above, establish the user's intended outcome using the closure rules in [dimensions.md](dimensions.md).

### Brainstorming guidance

Use high breadth to generate varied possibilities and unexpected connections, with low depth to avoid developing each idea prematurely. Use low rigor for light scrutiny and clearly labeled speculation; do not present invented premises as facts. Keep closure low so ideas need not converge on a decision or solution.

Use medium retention (Ret3) to preserve substantive ideas, including failed, rejected, or abandoned ones, in the existing `<project-directory>/records/<task-slug>/state-of-things.md`. Keep a concise description, current disposition, and any known reason an idea was rejected or failed, including the conditions under which that assessment applies. Distinguish an untested idea or provisional rejection from an observed failure. Update this account as ideas develop; do not retain only the surviving suggestions, require exhaustive transcripts, or add a separate idea log. If the user chooses lower Ret, honor that coverage and explain the resulting loss of idea continuity.
