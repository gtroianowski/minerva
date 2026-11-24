# Minerva

Minerva develops skills and simple tools for maintaining records and accumulating useful project knowledge.

Gerald replaced the earlier Engineer and Clerk approaches. It frames work and serializes records at the chosen retention level. The next system will consume those records to support semi-directed knowledge accumulation: the user conveys the KB’s objectives, and feedback refines what knowledge is worth retaining for that project.

## Reading map

- [Gerald](skills/gerald/SKILL.md): current skill package, with focused references.
- [RFCs under review](rfc/under-review/README.md): core knowledge-system proposals and residual ideas from retired skills; not active instructions.
- [Librarian authoring guide](skills/librarian/creating-knowledge-leaves.md): provisional leaf format, classification, retrieval, and templates; not yet a complete installed skill.
- [Investigator specification](skills/investigator/investigator-specification.md): uninstalled draft with historical role dependencies flagged for review.
- [Musings](musings/README.md): exploratory ideas that have not been adopted.
- [Graveyard](graveyard/README.md): retired Engineer/Clerk and shelved bootstrapping material, retained for provenance only.
- [Setup notes](SETUP.md): existing host-integration notes, still requiring refinement for multiple repositories.

Consumer-project data belongs outside this framework checkout. The preferred layout is `minerva-artifacts/records/` for serialized work and `minerva-artifacts/kb/` for reusable knowledge. Integrating these paths with Gerald’s logical project-directory contract remains to be specified. No artifact directories are created by this documentation change.

Markdown files with YAML frontmatter remain the intended knowledge representation. Strict schema validation, retrieval tools, promotion workflow, and inspectable retrieval breadcrumbs are still design/implementation work; there is no SQLite dependency.
