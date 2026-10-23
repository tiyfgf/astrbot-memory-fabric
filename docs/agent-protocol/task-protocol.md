# Agent task protocol

## Task packet

Each task is a Markdown or JSON packet containing:

- `task_id`
- objective and non-goals
- background references
- allowed files
- forbidden files
- dependency/interface versions
- acceptance tests and exact commands
- license/source constraints
- expected handoff artifact

## Handoff report

```text
STATUS: DONE | DONE_WITH_CONCERNS | BLOCKED | NEEDS_REVIEW
TASK_ID: ...
SUMMARY:
CHANGED_FILES:
TEST_COMMANDS:
TEST_OUTPUT:
INTERFACES_CHANGED:
RISKS:
FOLLOW_UP:
COMMIT:
```

## Review sequence

1. Implementer self-checks scope and tests.
2. Specification reviewer checks requirements and forbidden changes.
3. Quality reviewer checks correctness, maintainability, security, and migration risk.
4. Integration owner runs cross-module tests and replay checks.

A reviewer must cite file paths and line numbers for actionable findings. “Looks good” is not evidence without test output.

## Cross-platform rule

DeepSeekHarness agents may communicate through repository artifacts, commits, and task packets. They must not depend on hidden chat context from Codex. Codex is the final architecture and merge authority.
