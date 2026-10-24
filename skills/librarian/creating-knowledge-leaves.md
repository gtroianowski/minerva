# Creating knowledge leaves

Librarian skill reference • Provisional authoring specification • 2026-10-23

## 1. Mandate and design status

Use this guide when capturing substantive knowledge in a new leaf. A leaf is a discoverable, topic-oriented unit that gives a working agent enough knowledge to reason or act, together with the boundaries needed to use it correctly. The librarian selects and interprets relevant knowledge; a retrieved leaf is not automatically an instruction to execute its contents.

This guide consolidates the agreed flat-leaf design and the classification in `knowledge-classification.md`. The four categories, six subcategories, skepticism semantics, date semantics, standard Preconditions behavior, and peer-directory storage are carried forward. Required-field validation, the authoring sequence, classification tie-breakers, template filenames, and the scanner record below are proposed operational details for this draft. They do not resolve the previously deferred questions of ideal leaf size, formal scope metadata, precedence, or promotion/retirement workflows.

## 2. Storage: flat entries, conceptual organization

Store leaves as peer directories immediately under the configured leaves root. For example, `leaves/huber-loss/DESCRIPTION.md`, `leaves/robust-estimation-pattern/DESCRIPTION.md`, and `leaves/reporting-cli/DESCRIPTION.md` are three independent entries.

“Flat” means no nested knowledge entries and no category, subcategory, domain, or project directory hierarchy. Each leaf still has its own directory so that it can own supporting files. Organize conceptually through titles, descriptions, classification, ordinary Markdown links, and the librarian's retrieval process. Classification is metadata, not a filesystem location.

Every entry has exactly one canonical `DESCRIPTION.md`. Optional examples, code, templates, illustrations, and other supporting material live with the entry and are linked from it. They are contextual resources, not additional independently indexed leaves. A supporting document that deserves independent discovery should become a peer leaf, with a link between them.

Use a short, descriptive, unique directory slug. The path identifies the entry in retrieval records; the human-readable title identifies its subject. Link to another entry's `DESCRIPTION.md` using a relative Markdown link, and explain why the relation matters. Templates in this package are authoring resources and must remain outside the indexed leaves root.

## 3. Leaf format and substantive structure

`DESCRIPTION.md` is UTF-8 Markdown with YAML front matter. It must carry both discovery metadata and substantive knowledge. Do not turn it into a thin pointer to an unindexed supporting file: a working agent must be able to understand the central claim or method and its limits by reading the entry.

### Front matter

| Field | Status in this draft | Meaning and authoring rule |
| --- | --- | --- |
| `title` | Required | Specific, recognizable topic or task; use vocabulary a requester is likely to use. |
| `description` | Required | Compact discovery summary: what the leaf contains, when it is relevant, and distinguishing context. Do not merely repeat the title. |
| `type` | Required | One of `fact`, `procedure`, `principle`, `observation`. |
| `subtype` | Required for fact/procedure; omitted otherwise | Fact: `analytical` or `metastable`. Procedure: `structural`, `conventional`, `established-pattern`, or `remedial`. |
| `recorded` | Required by this draft | ISO date when this knowledge was captured. It is neither event date nor last verification date. Earlier agreement allowed this field; this draft makes it part of new-leaf authoring. |
| `revisit` | Optional | ISO date requesting review. It does not expire the leaf or revoke an operative choice. |

The token `established-pattern` is a proposed serialization of the agreed label “Established pattern.” Do not introduce alternative spellings within a corpus. Do not add a numeric trust/skepticism score. Do not add scope, roles, lineage, concepts, tags, or authority fields as if their schema were settled. Put needed context and provenance in prose until a separate schema decision adopts a field.

### Body

Use these common sections for all categories. Their headings have the same meaning across templates; category-specific layouts are deliberately deferred.

| Section | Role |
| --- | --- |
| H1 matching title | Recognizable document heading. |
| `Summary` | State the central knowledge directly. A reader should quickly know what this entry establishes or enables. |
| `Applicability and boundaries` | Identify domain, system, versions, assumptions, scope, exclusions, and situations where this entry should not be applied. Scope is explicit prose for now. |
| `Preconditions` | Specify information or conditions that must be resolved before applying the knowledge or carrying out the task. See the operational contract below. |
| `Knowledge` | The substantive definition, method, framework, or situated account. Supporting facts and examples may be included without forcing every sentence into the primary category. |
| `Rationale and evidence` | Explain why the claim or method is supported, who adopted a convention when known, and where the evidence comes from. Distinguish observation, inference, and choice. |
| `Skepticism and reassessment` | State what to question, what changes would matter, and how the agent should respond. Explain classification ambiguity here when relevant. |
| `See also` | Related leaves that provide adjacent knowledge. Explain each relation; these are navigation aids. |
| `References` | Sources bearing on the entry as a whole, with relevant version/date information when known. |

Prefer inline links where a source, example, or neighboring concept is used. `References` is for sources supporting the whole document, not a substitute for attributing a specific claim. `See also` is for useful neighboring knowledge, not a mandatory link graph. Do not fabricate sources. Mark an unavailable source or uncertain claim explicitly. Templates contain every heading; final leaves may omit empty optional navigation sections. If there are no task preconditions, state that explicitly rather than leave unexplained boilerplate.

### Preconditions are an operational contract

A precondition is a requirement for responsible application, not background exposition. State what is needed, when it is needed, and what the agent must do if it is unresolved. Check whether the current request or available context already supplies it. If a required value or material ambiguity remains unresolved, obtain clarification before the dependent action; do not invent a silent default. A documented default is usable only when its stated conditions apply. Independent work can continue.

For realized volatility, specify return horizon and estimation window; state any other choices that materially determine this leaf's calculation. For a report, establish purpose, audience, and an applicable template or required output when these affect the result. For a recurring process, establish cadence and whether execution must align with live markets when relevant. Make conditional requirements explicit: “If annualized output is requested, establish the annualization convention.”

Separate preconditions from applicability: applicability asks whether this leaf fits the situation; preconditions ask what must be known or satisfied before using it. A mathematical fact may need assumptions checked without requiring a user question every time it is read.

## 4. Category, skepticism, and expected treatment

These are three distinct dimensions. Category/subcategory says what role the knowledge plays and what sustains its validity. Skepticism says what the agent should question. Expected treatment says how to use the knowledge. Classification informs behavior; it does not replace reading the body.

The vocabulary is closed. Do not create new types or subtypes during ordinary leaf authoring. Choose the primary role and explain secondary aspects in prose. Do not classify by subject domain, force strict sentence-level homogeneity, or introduce a universal lifetime ordering.

### Fact

A fact establishes what something is or what follows under stated assumptions. It does not by itself establish when a technique should be chosen. An adequately self-contained definition or account belongs here even if it supports subsequent advice elsewhere.

| Subcategory | Deciding criterion | Agent skepticism | Expected treatment |
| --- | --- | --- | --- |
| Analytical | Its validity rests on definitions, logic, mathematics, or sufficiently stable laws of nature. | Check premises, model assumptions, and applicability. | Use as a durable foundation within its assumptions. |
| Metastable | Its validity rests on an empirical, technical, or institutional state that is stable but changeable. | Check whether that state still holds, especially after version, institutional, or environmental changes. | Use provisionally; verify when age, changed context, or counterevidence warrants it. |

Analytical examples: Huber loss definition and properties; mathematical properties of linear models; the Black–Scholes result under its assumptions. Including stable physical laws here is an operational convention, not a philosophical assertion that empirical laws are a priori. State model limitations rather than presenting model consequences as unconditional facts about the world.

Metastable examples: semantics of a specified FIX version, a stable API, or an established market schedule. “Often unchanged” does not make these analytical. Record the relevant version or institution in the body. The fact that weekends are normally nontrading days can change institutionally; it is not a mathematical necessity.

### Procedure

A procedure answers “How do I do X?” Its subtype follows the primary reason this method applies, rather than how imperative or detailed its wording is.

| Subcategory | Deciding criterion | Agent skepticism | Expected treatment |
| --- | --- | --- | --- |
| Structural | Mechanics are required by constraints, an interface, a protocol, or the system itself. | Have those underlying constraints or versions changed? | Follow required mechanics while valid; check the actual system when warranted. |
| Conventional | The method is an adopted choice among viable alternatives. | Is the choice still adopted, or is there evidence it should be reconsidered? | Respect the operative choice. Surface concerns without silently replacing it. |
| Established pattern | A reusable solution is justified by a recurring problem shape and known tradeoffs. | Does this problem fit, and do the tradeoffs remain appropriate? | Adapt with judgment; explain relevant tradeoffs. |
| Remedial | The method exists to address an identified failure, risk, or incident. | Does the failure mode still exist, and is this safeguard still useful? | Preserve the operative safeguard; flag possible obsolescence for review. |

Structural example: required steps to submit an order through an exchange interface. Describe the constraint that makes the sequence necessary.

Conventional examples: using Tyro for a project's CLI, an adopted deployment workflow, or a chosen asynchronous architecture. State the applicable project and adoption basis when known. Expense of switching can explain stability, but does not turn a convention into a structural requirement.

Established-pattern examples: a Gang of Four pattern or a reusable estimation approach with recognizable applicability and costs. Describe when to use it and when another approach may be preferable.

Remedial examples: a check introduced after an outage or a workaround for a filesystem defect. Identify the failure mode, evidence, affected environment, and conditions that would support retiring the remedy. Never remove it solely because its recorded date is old.

If a remedy later becomes a convention, classify by its current primary justification and preserve the history in prose. If a pattern is mandatory because of the project's chosen architecture, distinguish that adoption from a mechanically unavoidable constraint. Do not multiply labels to represent every overlap.

### Principle

A principle is a durable conceptual lens or generalizable guiding idea used to interpret situations or make choices. It can advocate an approach, explain why it helps, or reveal a useful relationship. It remains meaningful even when a different approach is selected. There are no subcategories currently.

Examples: separation of concerns; Agile or XP principles; mathematical duality as a lens; how misaligned incentives can create systemic risk. Explain what the principle illuminates or advocates, why, and its limits and tradeoffs. Question relevance, assumptions, competing principles, and limitations. Use it as a reasoning tool, not an unconditional command or mechanical recipe. A principle favoring single ownership differs from steps for constructing `std::unique_ptr`.

### Observation

An observation records what the world exhibited under identifiable circumstances: an event, incident, empirical finding, experiment, or localized behavior. There are no subcategories currently. Classification as observation does not imply weak credibility.

Examples: an outage and its outcome; a reproducible filesystem bug; an estimator's measured improvement on dataset X; a historical crisis and its aftermath. Describe circumstances, evidence, and uncertainty. Separate what happened from the interpretation of why it happened. Question evidence quality, context, generalizability, and present relevance. Preserve situated evidence; do not automatically promote it into a general rule. An old event can remain true while its usefulness for today's decisions declines.

## 5. Choosing a classification

Classify the leaf's central contribution, using this sequence:

1. Write a one-sentence statement of what the reader gains. If the point is a situated event or measured outcome, start with observation. If it establishes a definition or descriptive claim, start with fact. If it gives a method, start with procedure. If it guides interpretation or choice through a general idea, start with principle.
2. For a fact, ask what could make it false: failure of its stated premises points toward analytical; a changed external state points toward metastable. Historical or experimental accounts remain observations when their situated evidence is the contribution.
3. For a procedure, ask why this method applies: unavoidable mechanics → structural; adopted choice → conventional; reusable solution with tradeoffs → established-pattern; response to a particular failure/risk → remedial.
4. Explain close calls using the primary justification. A method can have secondary conventional or remedial aspects without receiving multiple subtypes.
5. If uncertain, make an educated provisional choice, record the reason and the ambiguity in `Skepticism and reassessment`, and identify what evidence would settle it. Do not invent a classification-confidence field or assert unknown adoption/authority. Ask for clarification only if the ambiguity materially changes treatment and cannot be resolved from available evidence.
6. Consider splitting when substantial contributions need independently different discovery or treatment. Do not split every supporting sentence; ideal granularity remains unsettled.

| Main contribution about the same subject | Classification |
| --- | --- |
| Definition and mathematical properties of Huber loss | fact / analytical |
| Robustness as a lens for balancing outlier sensitivity and efficiency | principle |
| A reusable method for fitting robust estimators, with use cases and tradeoffs | procedure / established-pattern |
| Required invocation mechanics of a specified fitting interface | procedure / structural |
| The team's adopted estimator for comparable reports | procedure / conventional |
| A validation check added after missing observations corrupted a report | procedure / remedial |
| The measured estimator result on a specified dataset | observation |
| The currently supported estimator options in a versioned API | fact / metastable |

## 6. Metadata and information retrieval

Metadata enables candidate discovery and helps interpret retrieved knowledge. It is not a substitute for the body, a source of automatic authority, or a hierarchy of topics.

Titles provide a compact route for direct conceptual matches. Descriptions make the leaf discoverable when the request uses different wording, expresses a task rather than a topic, or needs disambiguation among related entries. Include ordinary domain vocabulary and important alternative terms naturally. Avoid keyword dumping and unsupported promises about coverage.

The earlier retrieval design uses independent paths: a title/description-oriented candidate search and a body grep/search path through canonical `DESCRIPTION.md` files. Keep those paths independent during candidate generation so that a missed title or misleading summary does not suppress the other path. Join candidates by canonical leaf path, retain why each matched, then read and filter for semantic relevance and applicability. Links can supply targeted follow-up reading; do not expand the entire link graph by default. For larger corpora, add a candidate-narrowing stage before loading many bodies without abandoning independent retrieval paths.

A proposed scanner record contains `path`, `title`, `description`, `type`, `subtype` when present, `recorded`, and `revisit` when present. At retrieval time it can add `age_days` and `revisit_due`; these computed fields are not stored in front matter. Joined results should retain match source and brief relevance reasons so the working agent can audit selection. The scanner inventories entries and extracts metadata; semantic relevance and category interpretation remain agent work. Links may be extracted as navigation hints, without requiring typed edges or an ontology.

Type/subtype tells the agent how to interpret a result, including what deserves verification. Avoid filtering away all observations or principles merely because the user asked for an action: either may supply essential evidence or reasoning. `recorded` provides temporal context; it is not proof of freshness or truth. `revisit` requests reassessment; passing it never automatically invalidates a convention or removes a safeguard. Do not hardcode freshness deadlines by category. A verified protocol change matters more than an arbitrary age threshold.

The corpus manifest is a separate librarian input defining what corpus is in scope and how it is interpreted. Describe subcorpora through inclusion/exclusion patterns with prose for exceptions and their role, rather than fixed flags such as `code: true`. Keep corpus goals, principles, and domain context there. It does not organize leaves into category folders, nor should an author infer that an excluded supporting file is independently discoverable.

## 7. Authoring procedure

1. **Read the mandate.** Read the librarian's corpus manifest and applicable authoring instructions. Establish the intended corpus and the knowledge to capture.
2. **Retrieve before creating.** Search titles/descriptions and canonical bodies for the same topic, synonyms, related methods, and likely contradictions. Read plausible matches. Decide whether to extend an existing leaf or create a distinct one; avoid duplicate authority and near-identical entries.
3. **Identify the contribution.** Write the central claim or task in one sentence. Establish context and intended use. Separate observed results, inferred explanations, adopted choices, and recommendations.
4. **Choose type/subtype.** Apply section 5. Use evidence rather than imperative wording. Keep necessary classification uncertainty visible in prose.
5. **Select the matching template.** Use the exact subtype template when known. Parent fact/procedure templates are starting points requiring a subtype before completion. Principle/observation templates are complete category selections. All templates currently share one body structure.
6. **Create a peer entry.** Choose a unique descriptive slug under the leaves root. Create `DESCRIPTION.md`; keep reusable supporting files local to this entry and link them contextually.
7. **Write discovery metadata.** Draft a specific title and useful description, select valid type/subtype tokens, and set the actual capture date. Add a revisit date only with a meaningful review intention. Do not represent capture time as verification time.
8. **Write the substantive body.** State the knowledge, assumptions, limits, rationale, and sources. Explain the primary justification for a procedure and the circumstances of an observation. Keep the central knowledge in `DESCRIPTION.md` even when examples are separate.
9. **Make Preconditions actionable.** For each material unresolved input, say when it is required and how to resolve its absence. Distinguish an authoritative default from an author guess. Do not require clarification for information already supplied.
10. **Specify expected treatment.** Explain truth stability, applicability, and reasons for reassessment separately where relevant. State what the agent should check, follow, adapt, or flag. Skepticism does not authorize silent replacement of an operative convention or safeguard.
11. **Connect and attribute.** Add contextual inline links. Add useful neighboring leaves in See also and whole-entry sources in References. Surface contradictions with their scope and evidence; do not invent a precedence policy or silently erase one side.
12. **Validate.** Check metadata, content, retrieval discoverability, paths, and operational meaning using section 8. Resolve unfinished placeholders. Report the created leaf, chosen classification, and material uncertainty. Do not claim external adoption, verification, or authority absent evidence.

## 8. Completion checks

- Exactly one canonical `DESCRIPTION.md` exists in the new peer entry; no nested entry or category hierarchy was introduced.
- YAML parses; title, description, type, and recorded date are present. Facts/procedures have valid subtypes; principles/observations omit subtype. Optional dates are valid ISO dates.
- The body states useful substantive knowledge and its boundaries, rather than merely advertising linked files.
- Category follows the primary contribution; the reason is defensible. An observation has not silently become a rule, and a principle has not silently become a command.
- Required missing inputs and conditional requirements have explicit behavior. Unsupported defaults, guessed authority, and invented citations are absent.
- Skepticism distinguishes truth, applicability, and reassessment where relevant. Age or a due revisit date does not revoke operative requirements.
- Links resolve to intended files. Supporting material is reachable from the canonical entry and is not treated as an independently indexed leaf.
- Try one natural title-oriented query and one plausible body-oriented query. Confirm the entry has wording that supports both, and that its description distinguishes it from nearby leaves. This is a lightweight authoring check, not a claim that retrieval quality has been quantitatively validated.

## 9. Template inventory

There are ten templates: one for each of the four categories and one for each of the six subcategories. They have identical headings and body prompts. Only the classification values differ. Parent templates for fact and procedure deliberately leave subtype unresolved; they are not valid completed leaves until it is chosen.

| Selection | Template |
| --- | --- |
| Fact, subtype undecided | [fact.md](templates/fact.md) |
| Fact / Analytical | [fact-analytical.md](templates/fact-analytical.md) |
| Fact / Metastable | [fact-metastable.md](templates/fact-metastable.md) |
| Procedure, subtype undecided | [procedure.md](templates/procedure.md) |
| Procedure / Structural | [procedure-structural.md](templates/procedure-structural.md) |
| Procedure / Conventional | [procedure-conventional.md](templates/procedure-conventional.md) |
| Procedure / Established pattern | [procedure-established-pattern.md](templates/procedure-established-pattern.md) |
| Procedure / Remedial | [procedure-remedial.md](templates/procedure-remedial.md) |
| Principle | [principle.md](templates/principle.md) |
| Observation | [observation.md](templates/observation.md) |

## 10. Source basis and open decisions

Classification and treatment are grounded in the existing `knowledge-classification.md` (2026-10-23). Leaf-directory storage, canonical DESCRIPTION.md indexing, contextual supporting files, standard Preconditions, independent retrieval paths, and ordinary Markdown links are reconstructed from the October 8–9 flat knowledge-base discussions. Manifest guidance also reflects the earlier corpus-design discussion. The prior `flat_knowledge_base_librarian_design.md` was identified in conversation retrieval but its original file was not available for direct inspection; this guide does not claim a verbatim reproduction of that document.

Still open: ideal size/homogeneity, formal scope encoding, conflict precedence, formal promotion/modification/retirement, and quantitative retrieval evaluation. This package is a proposed reference component of the librarian skill, not an installed skill or a change to the existing classification source.
