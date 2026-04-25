---
description: Update dev docs, create standard commit message, and push to develop only.
argument-hint: "[optional scope or note for commit context]"
---

Commit and push current changes to `develop`: $ARGUMENTS

Execution order (strict):
1. Trigger `/docs-dev-updates` first to update `docs/dev-updates.md` based on current changes.
2. Re-check git status/diff after docs update.
3. Generate:
   - Commit summary using repository standard (`feature: ...`, `fix: ...`, `chore: ...`, etc.)
   - Commit description (1-3 short lines describing intent/impact)
4. Show the generated commit summary and description to the user before any git write action.
5. Use the `AskQuestion` tool to confirm with the user:
   - Prompt: proceed with commit and push to `develop`?
   - Options: `Yes, proceed` and `No, cancel`
6. If user selects `No, cancel`, stop without staging/committing/pushing.
7. If user selects `Yes, proceed`, stage relevant changes.
8. Commit with summary as subject and description as body.
9. Push to `develop` branch only.

Branch safety rules:
1. If current branch is not `develop`, switch to `develop` first (or create it from current HEAD if it does not exist).
2. Do not push to `main` or any branch other than `develop`.
3. If no remote exists or `develop` has no upstream, stop and report the exact push command required.

Commit message format:
- Subject line examples:
  - `feature: Dashboard design`
  - `feature: Dashboard API implementation`
  - `chore: Add cursor command, skills, and rules guideline`
- Body:
  - concise explanation of why the change is needed
  - key scope and impact notes

If there are no changes after `/docs-dev-updates`:
- Do not create an empty commit.
- Report that nothing was committed.

User confirmation is mandatory:
- Never commit or push unless the user explicitly confirms via the question box.
