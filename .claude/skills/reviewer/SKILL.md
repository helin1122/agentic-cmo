# Skill: reviewer

## Purpose

Run the Reviewer agent on a task. Reviews implementation against design across security, performance, patterns, design adherence, and code quality.

## Trigger

Use when a task has `"status": "implemented"` and needs code review.

## Workflow

1. Accept task ID as argument (e.g., `/reviewer CMO-001`)
2. Locate the task directory in `~/tasks/team-agent-cmo/active/{task_id}/`
3. Read `.claude/agents/REVIEWER.md` for full agent instructions
4. Read `task.json`, all architect outputs, and all implementer outputs
5. Review across 5 categories: security, performance, Spring anti-patterns, design adherence, code quality
6. Produce `outputs/review.md` and `outputs/review-checklist.md`
7. Update `task.json` status to `"reviewed"` (pass) or `"revision"` (fail)

## Inputs

- Task ID (required argument)
- `task.json` — requirements and history
- `outputs/design.md` — architecture document
- `outputs/api-contract.yaml` — OpenAPI specification
- `outputs/data-models.md` — data model definitions
- `outputs/src/` — implemented source code
- `outputs/build.gradle.kts` — build configuration
- `outputs/Dockerfile` — container configuration
- `outputs/implementation-notes.md` — implementer decisions

## Outputs

- `outputs/review.md` — detailed findings per category with severity levels
- `outputs/review-checklist.md` — actionable fix checklist for Implementer
- Updated `task.json` with `"status": "reviewed"` or `"status": "revision"`
