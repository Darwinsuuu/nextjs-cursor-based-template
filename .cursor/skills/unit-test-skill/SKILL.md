---
name: unit-test-skill
description: Generate robust unit test cases with clear arrange-act-assert structure, edge-case coverage, deterministic mocks, and maintainable assertions. Use only when the test-generate command is explicitly triggered.
---

# Unit Test Skill

## When to Apply

Apply this skill only when the `/test-generate` command is explicitly triggered from `.cursor/commands/test-generate.md`.

Do not auto-apply this skill from general requests about testing, refactoring, or code review unless `/test-generate` is invoked.

## Default Standards

1. Test behavior, not implementation details.
2. Use clear `arrange -> act -> assert` flow.
3. Keep tests deterministic (no real network/time/randomness without control).
4. Cover success, failure, and boundary scenarios.
5. Prefer small, focused test cases with one primary assertion goal each.

## Test Case Design Workflow

1. Identify the unit under test and its public contract.
2. List critical paths:
   - expected success behavior
   - invalid input and error behavior
   - boundary values and empty states
   - branching logic and fallback behavior
3. Convert each path into named test cases with explicit expectations.
4. Add setup helpers only after repeated boilerplate appears.
5. Verify assertions reflect user/business outcomes, not internal call order unless required.

## Coverage Baseline

For each unit, include tests for:
- **happy path**: valid input returns expected output
- **input validation**: invalid, nullish, malformed, or partial input
- **edge/boundary values**: empty arrays, min/max values, zero, large payloads
- **error handling**: thrown errors, rejected promises, fallback states
- **state transitions**: before/after state for reducers, stores, and hooks

## Mocking and Isolation Rules

- Mock external boundaries (HTTP, DB, filesystem, browser APIs, timers).
- Avoid mocking the unit under test itself.
- Keep mock behavior minimal and explicit per test.
- Reset/restore mocks between tests to prevent leakage.
- Freeze time and randomness when logic depends on them.

## Async Test Guidelines

- Use `async/await`; avoid unhandled promises.
- Assert both resolved values and rejection paths.
- Wait for observable outcomes, not arbitrary sleep delays.
- Use fake timers only when testing timer-based behavior directly.

## Maintainability Checklist

Before finalizing tests, verify:
- [ ] Test names describe scenario + expected outcome
- [ ] Assertions are specific and meaningful
- [ ] No hidden shared mutable state between tests
- [ ] Test data is minimal but realistic
- [ ] Flaky dependencies are mocked or controlled
- [ ] New tests would fail if the behavior regresses

## Output Expectations When Generating Tests

When asked to generate unit tests:
1. Start by listing proposed test cases (brief bullets).
2. Implement tests in the repository's existing framework and style.
3. Keep structure consistent with nearby test files.
4. Include missing imports/setup for a runnable test file.
5. Mention any assumptions or uncovered risks after implementation.
