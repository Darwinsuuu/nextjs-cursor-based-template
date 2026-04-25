---
description: Run unit tests and prompt next action if tests fail.
argument-hint: "[optional test target, e.g. src/foo/bar.test.ts or npm test -- foo]"
---

Run unit tests for: $ARGUMENTS

Execution rules:
1. If `$ARGUMENTS` is provided, use it to scope the run (single file/test pattern/package command override).
2. If `$ARGUMENTS` is empty, run the repository's default unit test command.
3. Show a concise result summary (pass/fail, failing suites/tests, and key error message).

If tests pass:
- Report success and stop.

If tests fail:
1. Explain clearly why the test run failed using the test output (assertion mismatch, thrown error, timeout, mock/setup issue, import/build issue, etc.).
2. Use a question box via the `AskQuestion` tool with this exact intent:
   - Ask what to do next.
   - Option A: update unit test
   - Option B: update logic code
3. Wait for the user's choice before making code changes.

If no unit-test command can be identified from project scripts/tools, ask for the exact command to run.
