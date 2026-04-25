---
description: Generate or expand unit tests using the project unit-test skill.
argument-hint: "<target file or symbol> [behavior/edge cases to cover]"
---

Create or update unit tests for: $ARGUMENTS

Before writing tests, read and follow:
`.cursor/skills/unit-test-skill/SKILL.md`

Requirements:
1. Follow the repository's existing test framework and local test style.
2. Start with a brief bullet list of proposed test cases.
3. Use clear arrange-act-assert structure.
4. Cover happy path, validation, edge/boundary, and error behavior when applicable.
5. Keep tests deterministic (mock time/random/network/IO as needed).
6. Add or update imports/setup so the tests are runnable.
7. After implementation, list assumptions and any remaining risk gaps.

If no target is provided, ask for the specific file, function, hook, component, store, or service to test.
