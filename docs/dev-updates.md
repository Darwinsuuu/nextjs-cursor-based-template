# DEVELOPMENT UPDATES

## Cursor Command, Rules, and Docs Scaffolding

This trigger adds new Cursor command definitions, project rule/skill guides, and documentation tracking files to standardize team workflows.


| File name                                        | Type      | Description                                                                                           | Date Added | Created By    |
| ------------------------------------------------ | --------- | ----------------------------------------------------------------------------------------------------- | ---------- | ------------- |
| `.cursor/commands/docs-dev-updates.md`           | **Added** | Added a command template for generating deduplicated development update logs from repository changes. | 2026-04-25 | darwinlabiste |
| `.cursor/commands/test-generate.md`              | **Added** | Added a command file for standardized unit test generation workflows.                                 | 2026-04-25 | darwinlabiste |
| `.cursor/commands/test-validate.md`              | **Added** | Added a command file for validating tests against recent code changes.                                | 2026-04-25 | darwinlabiste |
| `.cursor/rules/file-folder-structure-naming.mdc` | **Added** | Added a repository rule enforcing file/folder structure and kebab-case naming conventions.            | 2026-04-25 | darwinlabiste |
| `.cursor/skills/frontend-skill/SKILL.md`         | **Added** | Added a frontend implementation skill guide covering UI, responsive design, and performance patterns. | 2026-04-25 | darwinlabiste |
| `.cursor/skills/security-skill/SKILL.md`         | **Added** | Added a security-focused skill guide for safe coding and configuration practices.                     | 2026-04-25 | darwinlabiste |
| `.cursor/skills/unit-test-skill/SKILL.md`        | **Added** | Added a unit testing skill guide for deterministic and maintainable test coverage.                    | 2026-04-25 | darwinlabiste |
| `docs/dev-updates.md`                            | **Added** | Added a development update ledger file to track ongoing change summaries.                             | 2026-04-25 | darwinlabiste |
| `docs/release-updates.md`                        | **Added** | Added a release updates document to capture release-oriented notes and milestones.                    | 2026-04-25 | darwinlabiste |


---

## Develop Commit Automation Command

This trigger adds a dedicated Cursor command to enforce a consistent flow for updating development logs, generating standard commit messages, and pushing only to the develop branch.

| File name                             | Type     | Description                                                                                                 | Date Added | Created By    |
| ------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------- | ---------- | ------------- |
| `.cursor/commands/commit-develop.md`  | **Added**    | Added a command to run `/docs-dev-updates`, generate standard commit summary/description, and push to develop only. | 2026-04-25 | darwinlabiste |
| `docs/dev-updates.md`                 | **Modified** | Updated the development updates ledger to include the new develop commit automation command entry.          | 2026-04-25 | darwinlabiste |

---

