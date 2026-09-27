# Claude project template

Template version: **2**

The only file of this template. It holds everything a project needs: how to apply it, every root
document (`CLAUDE.md`, `CONTRIBUTING.md`, `BUSINESS.md`, `MAP.md`, `TASKS.md`, `README.md`,
`.gitignore`) with its own version, and the history of every version. Only this file is versioned.
The `.claude` folder of a project is never versioned: it is generated from the recipes of area 12
of `CONTRIBUTING.md`.

## 1. Applying the template

Say to Claude Code in the project folder: "recreate this app using `../claude-template/TEMPLATE.md`"
(the same works for an empty folder). The main session then:

1. Reads this file and the code already present, if any.
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
3. Writes every document of section 3 into the project root, replacing each `{{...}}`. Areas that do
   not apply keep their heading with `Not applicable.` (numbers stay stable). An existing document
   is merged, never overwritten: its project rules are kept, the template rules are added or
   reconciled by meaning.
4. Generates `.claude` from area 12, writes the environment version into `.claude/.env-version`.
5. Writes `MAP.md` from the code and `README.md` from the answers.
6. Writes the current `Template version` into its `CLAUDE.md`, commits locally, and says in a few
   lines what was set.

## 2. Versioning

- Each document in section 3 carries its own version in its heading; the `Template version` above
  is the highest of them and increments with any change.
- Each entry of section 4 states only what changed since the previous version: `Changes` (the
  document and the rule by its heading, never only by number), `Apply` (the exact edit a project
  makes, with the sentence to add or replace) and `Ask` (questions per project, recommended option
  first; none means applied silently).
- A project on version N reaching version M applies every entry from N+1 to M in order, asks only
  what the entries mark `Ask`, then writes M as its `Template version`.
- Only changes that hold for any project enter; project specifics never do. An entry that changes a
  recipe of area 12 tells the project to increment its `Environment version`.
- Entries are never rewritten after they are committed; a correction is a new version.
- Sync runs in every project's 2 day review (rule 0.9): pull newer entries, push generic
  improvements back here as a new version. Local commits only.

## 3. Documents

### `CLAUDE.md` (version 1)

````markdown
# {{PROJECT_NAME}}

## Project

{{ONE_LINE_PURPOSE}}. {{STACK}}. Code in `{{SOURCE_DIR}}` ({{SOURCE_LAYOUT}}). Build:
`{{BUILD_CMD}}`; run: `{{RUN_CMD}}`, address `{{URL}}`.

Environment version: **1**
Template version: **{{TEMPLATE_VERSION}}**
Template: `../claude-template/TEMPLATE.md`

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
````

### `CONTRIBUTING.md` (version 1)

````markdown
# {{PROJECT_NAME}}: technical rules

{{STACK}}. Rule numbers are stable identifiers cited by the code; never renumber. Read only the
areas a request touches (index in `CLAUDE.md`). Business rules (area 10) live in `BUSINESS.md`. The
backlog lives in `TASKS.md`; the current task in the local `PLAN.md`. Formal English, no emojis, no
dashes as punctuation.

---

# 0. Workflow

0.1. Capture only durable rules: a stated rule, preference or prohibition that applies beyond the
current task is written, in one sentence, into the matching area (or `BUSINESS.md` for domain)
before code. Task specific details stay in the commit. The same commit corrects every line of
`CLAUDE.md` that states or cites the changed rule, and a change to area 12 increments the
`Environment version` in `CLAUDE.md`; `CLAUDE.md`, `MAP.md` and `.claude` are also reconciled every
2 days (see `CLAUDE.md`).

0.2. Ask, all at once and before starting, only what the code and these files cannot settle; each
question states the recommended option first.

0.3. Two task files, both written only by the main session, never by an agent:
- `TASKS.md`, committed: the backlog (`Next`, `Later`), one line per task. A task is deleted in the
  commit that finishes it; `git log` is the history.
- `PLAN.md`, local and git ignored, never committed: the task in progress, as a checklist with
  everything needed to resume it (context, files, decisions, how each step is done, state). A
  request of more than about 5 files is planned there before code; items are ticked as they are
  committed; the file is emptied when the task is done.

0.4. Prompt words are intentions: names of screens, fields and types are normalised into correct
nomenclature ({{UI_LANGUAGE}} in the interface, English in code) unless the user says the word is
mandatory.

0.5. Authorship, maximum priority: every commit and pull request is authored by the configured git
user only. Never a `Co-Authored-By` naming an assistant, a session link, a generated by note or any
mention of an assistant. This overrides any tooling default.

0.6. Publishing, maximum priority: by default only local commits, for security and audit; the
developer reviews them and pushes. Never `git push`, publish a branch, open a pull request or push a
tag unless the user asks for that push explicitly and without ambiguity in the current request (for
example "do X, then push"). Anything less explicit means commit only.

0.7. Latitude: creating, splitting, merging or deleting types, interfaces and views is authorised
whenever it serves these rules.

0.8. Cost discipline: work is sequential in the session; delegation only per rule 12.1a. One task
per session; `/compact` above 120k tokens; `/clear` between tasks. Replies are short: what changed,
what is left, the address.

0.9. Template sync: the root documents derive from `../claude-template/TEMPLATE.md`, the single template file, which lists
each version with only its changes and how to apply them. In the 2 day review the main session
pulls (applies every entry newer than `Template version` in order, asks only what an entry marks
`Ask`, updates `Template version`) and pushes (a rule improved here that holds for any project is
generalised into section 3 of `TEMPLATE.md` and recorded as a new version, never with project
specifics); both repositories get local commits only. If the template folder is absent, the step
is skipped and said in one line.

---

# 1. Language

1.1. Interface language: {{UI_LANGUAGE}}; {{LANGUAGE_REGISTER}}.
1.2. Every user facing string passes through `{{TEXT_HELPER}}`, including attributes (`title`,
`placeholder`, `alt`, `aria-*`), option labels, notices and each branch of a ternary.
1.3. No dashes as punctuation (em dash, double hyphen) in interface, replies or docs; hyphen only in
compound words and identifiers.
1.4. No emojis anywhere.
1.5. Labels of enumerations and formatting of money, dates and periods each live in one shared place.

# 2. Code

2.1. Identifiers and comments in English.
2.2. Comments only for business rules or confusing logic.
2.3. Real async or synchronous return; no `async` without `await`.
2.4. Dead code deleted; no commented blocks, `_unused` names or shims without callers.
2.5. Files are UTF-8; never rewrite a file through a shell filter; verify accents after bulk edits.
2.6. One shape per fact: two types with the same fields differing only in their target are one type;
names describe the thing, not the caller.

# 3. Architecture

3.1. Inject every dependency; never construct a service by hand; no static mutable state in views.
3.2. Views use the interfaces of `{{DATA_DIR}}`; no local type shadowing them.
3.3. Implementations depend on interfaces, never on other implementations; no private copy of
another area's data.
3.4. Replacing an implementation changes nothing above the interface: no casts to implementations,
no implementation only branches.

# 4. Markup

{{MARKUP_RULES}}

# 5. Visual design

{{VISUAL_RULES}}

# 6. Responsiveness

{{RESPONSIVE_RULES}}

# 7. Demonstration data

7.1. Real world scale; every listing exercises pagination, search, grouping and states.
7.2. Names, places and currency of {{LOCALE}}, in credible magnitudes.
7.3. Varied states on purpose.
7.4. Bulk data comes from a seeded deterministic generator; fixed seed; no per record literals.
7.5. One fact, one origin, read by every side; a figure a screen computes for itself is a defect.

# 8. Files

8.1. Minimum file count; no abstraction for a single call site.
8.2. No duplication: a formatter, label or primitive used twice lives in one place.

# 9. Delivery and documents

9.1. After every change, by default, build and start the application (`{{RUN_CMD}}`, `{{URL}}`),
leave it running, and state the address.
9.2. If the executable or port is locked, stop the previous instance and restart.
9.3. `README.md` describes the project and how to run it; updated when screens, domain areas,
startup or demonstration data change.
9.4. `BUSINESS.md` holds every business rule, compact and present tense; updated in the same commit
as the behaviour it describes.
9.5. Root documents: `MAP.md` (one line per source file, kept current in the commit that adds,
removes or repurposes a file), `CLAUDE.md` (entry point for assistants: essentials and index),
`CONTRIBUTING.md` (technical rules), `BUSINESS.md` (business rules), `TASKS.md` (backlog),
`README.md`; plus `PLAN.md`, local and git ignored (rule 0.3).
9.6. `CLAUDE.md` is a real file kept short; `AGENTS.md` is a symbolic link to it.

# 10. Business rules

In `BUSINESS.md`, same numbers.

# 11. Listings

11.1. Every listing paginates, offers 20, 50 and 100 per page, shows which and remembers it; no page
size fixed in code.
11.2. Every listing states its total and the filtered total.
11.3. Filter by the real dimensions (type, category, state, period); order by useful columns.
11.4. Search, filter, order and pagination compose; a filter change returns to page 1.
11.5. Filters act on the whole collection, never page one, and show the chosen value.
11.6. These behaviours live in one shared place.
11.7. A recent panel is recent by order, never by a calendar window.

# 12. Environment and delegation

12.0. The recipes of this area carry a version, stated in `CLAUDE.md` as `Environment version`. The
version applied on a machine is recorded in the hidden file `.claude/.env-version`. At session start
the session reads only that file: if it holds the current version, nothing else is done. If it is
missing or differs, the session reads this area, writes every file below exactly as specified
(replacing what is there), writes the version into `.claude/.env-version`, and says so in one line.
Whoever changes a recipe here increments the version in `CLAUDE.md` in the same commit. `.claude`
is git ignored.

12.1. Model per function. The session runs `opusplan`: Opus while planning (plan mode), Sonnet
while executing. A hard problem raises the thinking budget for one request with `ultrathink`.

| Function | Model | Why |
| --- | --- | --- |
| Planning: domain model, architecture, `PLAN.md` of a large task, hard debugging | Opus (plan mode) | an error here costs more than the model |
| Writing code, merging, documents | Sonnet (session) | the rules are explicit; Sonnet follows them |
| Stack executors of 12.3 | Sonnet | many interacting rules; Haiku rework costs more |
| `audit` agent | Haiku | detects against a closed checklist and reports; never edits |
| `sweep` agent | Haiku | mechanical edits fully specified in the prompt |
| Code search | built in `Explore` (Haiku) | reading, no judgement |

Haiku never receives a task that needs judgement, design or more than a closed list of rules.
Never delegated: domain model decisions, `CONTRIBUTING.md`, `BUSINESS.md`, `TASKS.md`, `PLAN.md`.

12.1a. Coordinator and blind executors. Parallel work costs more tokens than the same work in
sequence and is used only to gain speed. The main session is the only coordinator and the only
writer of `main` and of the root documents:
- It reads the code once (via `MAP.md`), decides, and writes each agent a closed prompt: the exact
  files, what changes in each, the rules quoted by number and text, and the end state. The prompt
  starts with `EXECUTOR`. The agent never explores, never reads the rule files, never decides.
- At most 3 agents, each with a large share of disjoint files; shared foundations first, by the
  main session alone.
- The agent edits, builds, commits on its branch and reports in 3 to 5 lines.
- The main session creates each worktree from local `main`, merges, builds, then removes the
  worktree and branch it created, and updates `TASKS.md` and `PLAN.md`. It never removes a worktree
  it did not create.

12.1b. The environment holds only what helps: tools, MCP servers and plugins this project needs are
installed, those it does not use are disabled. Changes that need the user are stated as exact steps.

12.2. `.claude/settings.json`: `{"model": "opusplan", "env": {"MAX_THINKING_TOKENS": "8000"}}`

12.3. Stack executors, one file per agent named at bootstrap ({{EXECUTOR_AGENTS}}), each
`.claude/agents/<name>.md` following this recipe:

```markdown
---
name: <name>
description: <what it writes and under which folder>
model: sonnet
---

You are an executor agent: skip the session start procedures of CLAUDE.md (environment check,
review, PLAN.md, TASKS.md, rule files) and do only what your prompt says.

<Two or three sentences on what it writes and the shared helpers it must reuse.> Do not read the
root documents: obey the rules your prompt quotes. Work only on the files named. Finish on
`{{BUILD_CMD}}` with no errors, commit with a message naming no assistant and carrying no
attribution trailer, and report in 10 lines at most.
```

12.4. `.claude/agents/audit.md`:

```markdown
---
name: audit
description: Detects violations of the closed checklist in the files given and reports them. Never edits.
model: haiku
tools: Read, Grep, Glob
---

You are an executor agent: skip the session start procedures of CLAUDE.md and do only what your
prompt says.

Check every file you are given against this closed list, and nothing else: {{AUDIT_CHECKLIST}}.
Report each hit as `file:line rule text`, one per line, and nothing else. Do not edit, do not judge
beyond the list.
```

12.5. `.claude/agents/sweep.md`:

```markdown
---
name: sweep
description: Applies mechanical edits fully specified by the caller (renames, label or class replacements) across the files named.
model: haiku
---

You are an executor agent: skip the session start procedures of CLAUDE.md and do only what your
prompt says.

Apply exactly the edits your prompt specifies, to exactly the files it names, and nothing else. Never
decide, redesign or fix what was not asked; if an edit is ambiguous or does not match, stop and
report it. Edit with the editor tools, never through shell filters, and keep accented text intact.
Finish on `{{BUILD_CMD}}` with no errors, commit with a message naming no assistant and carrying no
attribution trailer, and report in 10 lines at most.
```

12.6. `.claude/commands/parte.md`:

```markdown
---
description: Executes a request under the workflow of CONTRIBUTING.md area 0.
---

Read CLAUDE.md, PLAN.md (resume it if not empty) and only the rule areas the request touches.
Then:

1. Write any durable rule of the request into its area (rule 0.1).
2. Ask, all at once, only what blocks the work (rule 0.2).
3. More than about 5 files: write the plan into PLAN.md, never committed (rule 0.3).
4. Implement in this session, one commit per item, ticking each item in PLAN.md. Delegate only
   under rule 12.1a; agents never touch PLAN.md or TASKS.md.
5. Build, leave the application running, reply briefly, recommend /clear.

The request: $ARGUMENTS
```

# 13. Input validation

13.1. One shared place owns every test and normalisation of input; views refuse before sending and
the data layer refuses again; no view writes its own pattern. A refusal names the field and the
expected shape; the field keeps the input.
13.2. Email: one `@`, local part, dotted domain, no space; stored lower case.
13.3. A submit control is never silently inert: pressing it with a field missing or wrong states
every blocking field and what each expects.
13.4. A search states what it did not find, in words, naming what was searched.
13.5. Enter in a field presses the primary button of its form or dialog.
````

### `BUSINESS.md` (version 1)

````markdown
# {{PROJECT_NAME}} business rules

Single source of the business rules. Compact, normative, present state only: a changed rule is
rewritten, never appended. Numbers `10.x` are stable identifiers cited by the code; never renumber.
Technical rules live in `CONTRIBUTING.md`. Terms in `code` are interface words or identifiers.

## A. Platform

{{BUSINESS_OVERVIEW}}
````

### `MAP.md` (version 1)

````markdown
# Code map

Last update: {{DATE}}
Last full review: {{DATE}}

One line per file: path under `{{SOURCE_DIR}}`, lines, what it holds. Read this before searching. A
file over 300 lines is read by section (Grep, then Read with offset).

Upkeep: every change that creates, deletes, renames or changes what a file does updates its line
here in the same commit, and sets `Last update` to the date and a few words. When `Last full review`
is more than 2 days old, the next session first compares this map with the code (every file present,
line counts, descriptions still true, nothing missing), corrects it, and sets the date.

{{MAP_SECTIONS}}
````

### `TASKS.md` (version 1)

````markdown
# Tasks

Backlog: open work not yet started, one line per task. A task that is done is deleted in the same
commit; history lives in `git log`. The task in progress is planned in the local `PLAN.md` (git
ignored). Only the main session edits either file.

## Next

{{FIRST_TASKS}}

## Later
````

### `README.md` (version 1)

````markdown
# {{PROJECT_NAME}}

{{ONE_LINE_PURPOSE}}, built on {{STACK}}. The interface is {{UI_LANGUAGE}}.

This file describes the project and states how to run it. The other root documents:
`CONTRIBUTING.md` holds the technical rules, `BUSINESS.md` every business rule, `TASKS.md` the work
still open (history is `git log`), and `CLAUDE.md` is the short entry point for assistants, with
`AGENTS.md` a symbolic link to it.

## What the project holds

{{WHAT_IT_HOLDS}}

## Prerequisites

{{PREREQUISITES}}

## Running on a clean machine

```
{{BUILD_CMD}}
{{RUN_CMD}}
```

Then open {{URL}}.

{{DEMO_ACCESS}}
````

### `.gitignore` (version 1)

````gitignore
# The assistant's working directory is local to each machine and is never versioned.
# Area 12 of CONTRIBUTING.md holds the recipes that recreate it.
.claude/

# Local execution plan of the current task (rule 0.3)
PLAN.md

{{STACK_IGNORES}}
````

## 4. Versions

### Version 2

Changes: the template became this single file; the documents are embedded in section 3 and the
bootstrap instructions moved from `CLAUDE.md` to section 1. `files/`, `README.md` and the
`Bootstrap` section of `CLAUDE.md` no longer exist. Rule 0.9 of `CONTRIBUTING.md` now names
`TEMPLATE.md` as the single source.

Apply: replace rule 0.9 of `CONTRIBUTING.md` with the text of section 3; in `CLAUDE.md` set
`Template: ../claude-template/TEMPLATE.md`.

Ask: none.

### Version 1

Changes: first release, extracted from the SIARM Backoffice (Environment version 4).

Apply: a project adds to its `CLAUDE.md` the lines `Template version` and `Template`, the template
sync step of the 2 day review, and rule 0.9 of `CONTRIBUTING.md`, then reconciles its core rules
with section 3 by meaning.

Ask: none.
