---
description: Append deduplicated added/changed/deleted file updates to docs/dev-updates.md.
argument-hint: "[optional git range, e.g. HEAD~1..HEAD]"
---

Update `docs/dev-updates.md` using the latest repository changes: $ARGUMENTS

Goal:
- Append new development updates for files that are `Added`, `Modified`, or `Deleted`.
- Add a high-level run summary for the changes detected at trigger time.
- Prevent duplicate entries from being appended.
- Keep output clean, readable markdown.

Data source rules:
1. Read existing `docs/dev-updates.md` first (create it if missing).
2. If `$ARGUMENTS` is provided, treat it as a git diff range and inspect only that range.
3. If `$ARGUMENTS` is empty, inspect current local changes (staged + unstaged + untracked) using git status/diff commands.
4. Include only real file changes. Ignore pure rename metadata unless content changed.

Output constraints (strict):
1. `docs/dev-updates.md` should only contain entries composed of:
   - per-run dynamic summary title (H2) based on detected changes
   - table rows containing:
     - file name
     - type (`Modified`, `Deleted`, `Added`) with colors
     - description
     - date added
     - created by
2. Use readable markdown formatting with proper heading hierarchy and clean spacing.
3. Add one divider (`---`) after each trigger batch (not after every row).

Required output format for each trigger:

## <Dynamic summary title based on current changes>
<1 short paragraph summarizing the overall scope of this trigger's changes.>

| File name | Type | Description | Date Added | Created By |
| --- | --- | --- | --- | --- |
| `<path/to/file>` | <colorized type> | <short human-readable summary> | <YYYY-MM-DD> | <author name> |

---

Dynamic H2 title rules:
1. Infer a concise title from the actual change set (feature area, refactor scope, docs/config/test focus).
2. Keep the title short, specific, and human-readable.
3. Avoid generic titles such as `Summary`, `Updates`, or `Changes`.
4. Example patterns:
   - `## Authentication Flow Refinements`
   - `## Dashboard UI and State Updates`
   - `## Build Config and Tooling Cleanup`

Type color rules (use HTML so color is visible in markdown renderers that support inline HTML):
- `Added` = `<span style="color:#16a34a;"><strong>Added</strong></span>`
- `Modified` = `<span style="color:#d97706;"><strong>Modified</strong></span>`
- `Deleted` = `<span style="color:#dc2626;"><strong>Deleted</strong></span>`

Created By rules:
1. If `$ARGUMENTS` is a commit/range, use the most relevant git author for each file from that range.
2. If working from local uncommitted changes, use the current git user if available.
3. If author cannot be resolved, use `Unknown`.

Deduplication rules:
1. Do not append a row if the same file name + type + date added already exists in `docs/dev-updates.md`.
2. If an existing matching entry is found, skip it silently.
3. Append only truly new entries.

Description quality rules:
1. Use concise, specific descriptions (1 sentence each).
2. Infer intent from diff/context when possible (feature, fix, refactor, docs, config, test, cleanup).
3. If context is limited, use a safe generic phrase like:
   - `File added for new feature scaffolding.`
   - `File updated to support recent feature changes.`
   - `File removed as part of cleanup/refactor.`

If there are no new changes to append:
- Do not modify `docs/dev-updates.md`.
- Report that no new updates were added.
