# Project-relative resource locations

Express every project data or artifact path as `<project-directory>/path/to/resource`. Treat `<project-directory>` as a logical placeholder defined by the environment's base instructions, not a shell variable, a literal directory name, or a destination for Gerald to choose.

For Codex, use the definition supplied in the loaded project instruction file (normally AGENTS.md); for a ChatGPT project, use its project instructions. Follow that definition and the environment's storage tools. The same Gerald skill can therefore use a local project root in one environment and a Library project folder in another.

## Resolve and use

1. Obtain the meaning of `<project-directory>` from the base project instructions before the first project resource operation. Reuse a definition already in context; do not repeatedly reread it.
2. If the definition is missing, ambiguous, or conflicting, ask only for the missing definition and pause dependent resource operations. Do not infer a Library folder or local root from the project name or current working directory.
3. Resolve the logical resource through the tools appropriate to the defined destination. Reuse verified file and folder identities where the tools require them; these are access details, not an additional Gerald configuration or mapping registry.
4. Retain records and task artifacts under `<project-directory>/records/<task-slug>/`. Reuse the same task directory across conversations and stages; identify the existing undertaking before creating a new directory. State the chosen logical location once.
5. If the destination is inaccessible or a write fails, report the limitation and preserve available recovery notes in the conversation. Do not silently save to a different destination, create divergent copies, or claim a save succeeded.

Keep other project resource references under the same convention, for example `<project-directory>/knowledge-base/…` or `<project-directory>/tools/…`. This defines how paths are interpreted; it does not authorize Gerald to write knowledge entries or add tools.

## Renames, moves, and resumption

Use the current base-instruction definition after a deliberate rename or move. Do not create a second destination because a display name changed. If a changed definition leaves the intended existing records unclear, ask for the missing identification before dependent work.

On resumption, read only the records and linked artifacts relevant to the undertaking and supported by its Ret coverage. Recover what they actually preserve; disclose material gaps. At Ret1, existing records may be read when relevant without restarting their maintenance.

Bundled instruction links in SKILL.md are relative to the skill itself so the installed skill remains portable. They are not project data locations and do not redefine `<project-directory>`.
