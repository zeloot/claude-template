# Template versions

Current version: **1**

Single source of the template history. Each version states only what changed since the previous one
and how a project applies it. A project on version N reaching version M applies every entry from N+1
to M in order, asks the user only what an entry marks `Ask`, then writes M as its `Template version`
in `CLAUDE.md`.

Rules for whoever writes a new version:
- A version is added only for a change that holds in any project; project specifics never enter.
- Each entry: `Changes` (what is new, altered or removed, naming the file and the rule by its
  heading, never only by number, since projects may number differently) and `Apply` (the exact edit
  a project makes, with the sentence to add or replace).
- `Ask` lists the questions an entry needs answered per project, each with the recommended option
  first. No questions means the entry is applied silently.
- An entry that changes a recipe of area 12 also tells the project to increment its
  `Environment version`.
- Entries are never rewritten after they are committed; a correction is a new version.
- `files/` always holds the result of every version, so a new project bootstraps directly on the
  current version.

---

## Version 1

Changes: first release, extracted from the SIARM Backoffice (Environment version 4).
`files/CLAUDE.md`, `CONTRIBUTING.md`, `BUSINESS.md`, `MAP.md`, `TASKS.md`, `README.md`,
`.gitignore`, with placeholders `{{...}}` filled at bootstrap.

Apply: a new project copies `files/` and follows the `Bootstrap` section of its `CLAUDE.md`. An
existing project that did not start from the template adds to its `CLAUDE.md` the lines
`Template version: **1**` and `Template: ../claude-template`, the `Template sync` step of the 2 day
review, and rule 0.9 of `CONTRIBUTING.md`, then reconciles its core rules with `files/` by meaning.

Ask: none.
