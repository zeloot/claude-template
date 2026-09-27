# Claude project template

A versioned set of root documents that make Claude Code work well on any project: a short
`CLAUDE.md` entry point, stable numbered rules in `CONTRIBUTING.md`, business rules in
`BUSINESS.md`, a code map in `MAP.md`, the backlog in `TASKS.md` and a generated `README.md`.
The `.claude` folder is never versioned: its files are generated from the recipes of area 12 of
`CONTRIBUTING.md`.

## Layout

- `TEMPLATE.md`: the current version and, for every version, only its changes and how to apply them.
- `files/`: the documents a new project starts from, with placeholders `{{...}}`.

## Starting a project

1. Copy the contents of `files/` (including `.gitignore`) into the new project folder.
2. Open Claude Code there. The first session sees the `Bootstrap` section of `CLAUDE.md`, asks all
   its questions at once, fills every placeholder, removes the areas that do not apply, generates
   `.claude` from area 12, writes `MAP.md` and `README.md` from the code, and deletes the section.

The project keeps `Template: ../claude-template`, so this folder must sit next to the projects.

## Keeping it in sync

Every 2 days, during the review of its `CLAUDE.md`, each project:
- pulls: if `TEMPLATE.md` holds a newer version, applies each pending entry in order and asks only
  what the entries mark `Ask`;
- pushes: rules the project improved that hold for any project are generalised into `files/` and
  recorded here as a new version, committed locally.

Commits here are local only; publishing is the user's decision.
