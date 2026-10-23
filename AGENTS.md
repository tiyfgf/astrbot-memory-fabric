# Agent Working Rules

## Mission

Build an AstrBot plugin, not a replacement bot platform. Keep the runtime boundary inside AstrBot and keep deployment data in the sibling `qq-astrbot` workspace.

## Repository rules

- `main` is stable and must remain buildable.
- `integration` is the shared integration branch when it is created.
- Feature work uses a dedicated branch or worktree: `feat/<area>-<short-name>`.
- Never commit API keys, QQ credentials, runtime databases, conversation exports, or local logs.
- Do not modify the sibling deployment workspace as part of ordinary development.
- Do not change a public schema or interface without an ADR and compatibility note.

## Agent task boundaries

Every delegated task must name:

1. the goal;
2. allowed files;
3. forbidden files;
4. dependencies and interface version;
5. acceptance tests;
6. license/source constraints.

Agents must return a structured report with status, changed files, tests and output, risks, and commit id.

## Quality gates

A change is not accepted until it has:

- focused tests;
- a clean diff;
- a specification review;
- a code-quality review;
- integration verification when it crosses module boundaries.

No agent may silently broaden scope or introduce a second competing data model.

## Third-party code

Research notes may summarize external projects. Copied code belongs under `third_party/` with source URL, commit, license, and local modifications recorded in `NOTICE` or a per-component notice file. Design ideas may be reimplemented independently, but license obligations still apply to copied code.
