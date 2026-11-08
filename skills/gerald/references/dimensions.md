# Dimension guidance

## Contents

- Rigor
- Depth
- Breadth
- Closure and its relationship to retention

### Rigor — Rig

Use rigor to control how strongly claims, assumptions, methods, and results must be supported. Infer the needed validation from the intended use and consequences of error. Distinguish established facts, inferences, and speculation at every level.

- **1:** Give a plausible, clearly qualified response with light validation. Example: brainstorm possible explanations for an observation.
- **2:** Check obvious inconsistencies and pivotal facts. Example: explain a familiar concept and check the numerical illustration.
- **3:** Verify central claims and challenge assumptions that could change the answer. Example: compare two methods using their documented behavior and stated limitations.
- **4:** Cross-check consequential claims and examine competing explanations or failure modes. Example: diagnose a recurring discrepancy using evidence that distinguishes likely causes.
- **5:** Test premises, seek counterevidence, and make the reasoning and validation inspectable. Example: investigate a suspected backtest bias before relying on its results.

Resolve factual uncertainty through inspection or research when possible. Make and state reasonable, reversible assumptions when they do not materially affect the outcome. If missing definitions, data, or constraints require a consequential assumption or prevent the required validation, identify the gap and pause only dependent work. Ask the user to resolve it, authorize a provisional assumption, or lower the required rigor. Preserve consequential uncertainty and do not represent an unverified result as verified. Greater rigor calls for greater scrutiny, not permission for every unspecified detail.

### Depth — D

Use depth to control how far to pursue a selected question into its mechanisms, evidence, dependencies, and exceptions. Assess the investigation separately from the length of the final explanation; substantial work can support a concise answer.

- **1:** Establish the immediate answer without tracing its mechanisms. Example: identify what a regression projection represents.
- **2:** Examine the central mechanism or a representative case. Example: inspect why residuals are orthogonal to fitted values.
- **3:** Investigate selected mechanisms and implications. Example: derive the projection formula and connect it to least squares.
- **4:** Trace important dependencies and edge cases. Example: examine rank deficiency and the assumptions behind the derivation.
- **5:** Follow the selected question through its relevant foundations, evidence, and exceptions. Example: build and verify a full account of a particular estimator's behavior under specified assumptions.

If the selected investigation depth would omit a mechanism needed to support the answer, surface that limitation and propose the necessary depth. Respect a user preference for shallower investigation while making consequential omissions visible. A request for a brief explanation does not itself reduce investigation depth. Stop following dependencies when they no longer help answer the selected question.

### Breadth — B

Use breadth to control the range of questions, sources, approaches, and perspectives considered. Include dependencies needed to answer the question; distinguish these from optional adjacent topics.

- **1:** Stay with the immediate question. Example: explain one named retrieval method.
- **2:** Include its nearest dependency or comparison. Example: explain how that method differs from keyword search.
- **3:** Consider related concepts and a small set of meaningful alternatives. Example: compare several retrieval approaches for a stated use case.
- **4:** Search across the relevant knowledge base and examine materially different approaches. Example: assess retrieval options against several workloads and operational constraints.
- **5:** Survey widely across relevant literature, adjacent domains, and competing perspectives. Example: map the major approaches to continuity in agent systems and the problems each addresses.

If an exclusion would materially distort the answer, explain why and propose expanding the scope. Keep optional discoveries separate from agreed work; do not silently turn them into new obligations. Apply the breadth–depth tradeoff described in SKILL.md.

### Closure — C

Use closure to control how questions remain in view and the obligation to reach an endpoint. Separate closure from whether the result is positive: a supported rejection or a finding that the available evidence cannot determine an answer can satisfy an agreed outcome. Merely labeling unfinished work unresolved does not satisfy it. Do not mistake a pause for completion.

- **1:** Allow the exchange to end without a fixed endpoint. Example: casual conversation about an idea.
- **2:** Capture a useful takeaway or natural stopping point. Example: brainstorm until a promising direction emerges, without resolving every branch.
- **3:** Keep the relevant questions and their answered or unanswered status in active context. Give the user a current sense of what has been answered and what remains, without an obligation to resolve every question or reach a fixed endpoint. Example: explore a design while keeping outstanding questions top of mind.
- **4:** Require the user to decide on an intended outcome and establish how its achievement will be recognized. Keep the undertaking open until that outcome is achieved or the user explicitly abandons it. Example: agree on the intended result of a document revision, complete it, and check it against the agreed criteria.
- **5:** With the user directing the goals, establish achievable milestones, end goals, and validation criteria before dependent execution. Actively elicit missing details and gently push back when the user bypasses intermediate steps needed to reach or validate the goals. Track progress through those milestones and verify achievement at the chosen rigor. Example: turn an investigation into an agreed sequence of answerable questions, intermediate checks, and validated end goals.

At C3 and above, maintain awareness of answered and unanswered questions throughout the work, not only in a closing summary. Persistent tracking remains governed by Ret; keeping questions in active context does not itself require new documents or a higher Ret score.

At C4 and C5, use existing user decisions where they settle the intended outcome; otherwise, ask the user to choose it. Propose concrete wording or alternatives to help the user decide, rather than silently choosing the endpoint. A pause, blocker, deferred task, or report of remaining gaps leaves the undertaking unfinished. The user may explicitly revise the outcome or abandon it; preserve that distinction from achievement. Accepting a limitation counts as completion only if the user explicitly revises the outcome so the result satisfies it. Apply the same completion obligation at C5.

At C5, help the user turn the intended outcome into a workable sequence. Ask focused questions until the end goals, achievable milestones, and means of validation are sufficiently clear. Propose milestones and checks for the user to shape or adopt; do not require the user to draft the plan unaided. When a requested shortcut skips a necessary intermediate step, explain the dependency or consequence and propose a practical way forward. Honor an explicit user override while making any resulting gap visible; do not claim an unachieved milestone or unperformed validation is complete. Closure defines what must be achieved and checked; rigor defines the strength of the validation.

When C increases, reconstruct the relevant answered and unanswered questions from available context and establish the outcome, milestones, or validation newly required by that level. Surface material ambiguity before dependent work; do not turn optional branches into obligations without agreement. If a missing input prevents progress, identify the blocker and continue independent work. When closing at C4 or C5, compare the result with the agreed outcome and distinguish achievement from explicit abandonment and any unfinished obligations.

#### Closure and retention

Whenever C increases, ask whether the user wants to increase Ret, unless their instruction already explicitly settles that choice. Explain what additional closure tracking a higher Ret would preserve and what continuity the current level may omit. Make this advisory: do not automatically raise Ret, impose additional retention requirements, or block independent work on the user's decision. If the user keeps Ret unchanged, honor that choice, manage closure obligations in active context, and persist only what the existing Ret supports.

Within the coverage already provided by Ret, let higher C make closure information more explicit and structured: at C3, retain answered and unanswered question status where supported; at C4, identify the active user-chosen outcome, completion criteria, and current disposition; at C5, organize retained end goals, milestones, dependencies, and validation criteria or results so their status can be recovered. Distinguish active targets from those achieved, abandoned, superseded, invalidated, or pending reconsideration. These are content-shaping guidelines within the chosen Ret, not mandatory additions to lower-Ret records. At Ret1, keep this information in active context without maintained records.
