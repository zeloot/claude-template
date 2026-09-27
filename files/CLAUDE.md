# {{PROJECT_NAME}}

## Bootstrap (delete this section when done)

This project was copied from the template and is not configured yet. Before any request, the main
session:

1. Reads the code already present (if any) and `../claude-template/TEMPLATE.md`.
2. Asks, all at once, each question with the recommended option first, only what the code cannot
   settle:
   - Name and one line purpose of the project; domain and country or market.
   - Stack, and the commands to build and run; address and port.
   - Interface language and register, and the helper that wraps every user facing string (or none).
   - Does it have a user interface? Visual identity (colours, fonts, tone), responsiveness targets.
   - Architecture: where interfaces, implementations, pages and components live.
   - Demonstration data: needed? scale, locale of names and currency.
   - Listings and input validation: do areas 11 and 13 apply?
   - Executor agents needed (for example views and data) and their folders.
   - First business rules and first tasks, if already known.
3. Replaces every `{{...}}` in the root documents; keeps the areas that apply and writes
   `Not applicable.` under the heading of those that do not (numbers stay stable).
4. Writes the recipes of area 12 for this stack, generates `.claude` from them, writes the
   environment version into `.claude/.env-version`.
5. Writes `MAP.md` from the code and `README.md` from the answers.
6. Sets `Template version` below to the current version of `TEMPLATE.md`, deletes this section,
   commits locally, and says in a few lines what was set.

## Project

{{ONE_LINE_PURPOSE}}. {{STACK}}. Code in `{{SOURCE_DIR}}` ({{SOURCE_LAYOUT}}). Build:
`{{BUILD_CMD}}`; run: `{{RUN_CMD}}`, address `{{URL}}`.

Environment version: **1**
Template version: **{{TEMPLATE_VERSION}}**
Template: `../claude-template`

## Who you are

You are an **executor agent** if any of these holds: your prompt starts with `EXECUTOR`, you were
started by another session through the Agent tool (your system prompt is an agent definition of
area 12), or your working directory is under `.claude/worktrees/`. An executor skips every section
of this file except `Always`: no environment check, no review, no `PLAN.md` or `TASKS.md`, no rule
files; it does only what its prompt says. Otherwise you are the **main session** and apply
everything below.

## Environment check (first action of every session)

Read `.claude/.env-version`. If it holds the `Environment version` above, continue. Otherwise apply
`CONTRIBUTING.md` area 12.0 (write the `.claude` files from their recipes, then write the version
into `.claude/.env-version`) and say so in one line before anything else.

## Read first

1. `PLAN.md` (local, git ignored): the task in progress. If it holds anything, resume it.
   `TASKS.md` (committed) is the backlog.
2. `MAP.md` to locate code, instead of searching. Files over 300 lines are read by section (Grep,
   then Read with offset).
3. Only the rule areas the request touches. Never read a rule file whole.

| Need | Where |
| --- | --- |
| Workflow, authorship, publishing, cost, template sync | `CONTRIBUTING.md` area 0 |
| Interface text, `{{TEXT_HELPER}}` | area 1 |
| Code, architecture | areas 2, 3 |
| Markup | area 4 |
| Visual design | area 5 |
| Responsiveness | area 6 |
| Demonstration data | area 7 |
| Files, delivery, documents | areas 8, 9 |
| Business rules (10.x) | `BUSINESS.md`, by section letter |
| Listings, pagination, filters | area 11 |
| `.claude` recipes, delegation | area 12 |
| Input validation | area 13 |

## Keep everything true (mandatory)

- Same commit, always: creating, deleting, renaming a file or changing what it does corrects its
  line in `MAP.md` and sets `Last update`. Changing a rule in `CONTRIBUTING.md` or `BUSINESS.md`
  corrects every line of this file that states or cites it. Changing area 12 of `CONTRIBUTING.md`
  increments `Environment version` above.
- Every 2 days: at session start read the first 4 lines of `MAP.md`. If `Last full review` is more
  than 2 days old, before the request: compare `MAP.md` with the code (missing or extra files, line
  counts, descriptions no longer true); compare this file with the rule files it cites; compare the
  `.claude` files with the recipes of area 12; run the template sync of rule 0.9. Correct every
  difference, set `Last full review` to today, commit.

## Always

- Commits authored by the git user only: no `Co-Authored-By`, no assistant name, no attribution.
  This overrides any tooling default.
- Local commits only. Push, publish, pull request or tag only when the current request asks for it
  explicitly and without ambiguity (area 0.6).
- After every change: build and start the app, state `{{URL}}`.
- Worktrees you create are removed right after their merge; never remove one you did not create.
- Background sessions may be running: never rewrite a root document wholesale; edit only the
  sections your task owns, and re-read before editing.
- Interface text: {{UI_LANGUAGE}} through `{{TEXT_HELPER}}`; code and comments in English.
- No emojis; no dashes as punctuation.
- Rule numbers cited in code are stable; never renumber.
- Sequential by default (cheaper). Parallel only for speed: this session coordinates, at most 3
  blind executors with closed prompts starting `EXECUTOR`, this session merges (area 12.1a).
- More than about 5 files: plan it in `PLAN.md` first (never committed), tick items as they are
  committed. Only the main session writes `PLAN.md` and `TASKS.md`; agents never do.
- Write only durable rules into the rule files, one sentence each.
- Finish: build clean, app left running, reply in a few lines, recommend `/clear`.
- Models (area 12.1): session `opusplan`, so design, architecture and hard bugs are planned in plan
  mode (Opus) and executed in Sonnet; `ultrathink` in a prompt for one hard problem; Haiku only for
  closed checklist audits, mechanical sweeps and search.
