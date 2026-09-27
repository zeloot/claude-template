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
