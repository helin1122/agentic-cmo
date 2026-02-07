# Skill: implementer

## Purpose

Run the Implementer agent on a task. Reads architect designs and produces working Java 21 / Spring Boot 3.4 code.

## Trigger

Use when a task has `"status": "designed"` or `"status": "revision"` and needs implementation.

## Workflow

1. Accept task ID as argument (e.g., `/implementer CMO-001`)
2. Locate the task directory in `~/tasks/team-agent-cmo/active/{task_id}/`
3. Read `.claude/agents/IMPLEMENTER.md` for full agent instructions
4. Read `task.json` and all architect outputs
5. If `revision` status, also read `outputs/review.md` and `outputs/review-checklist.md`
6. Produce source code, build files, and Dockerfile in `outputs/`
7. Write `outputs/implementation-notes.md`
8. Update `task.json` status to `"implemented"`

## Inputs

- Task ID (required argument)
- `task.json` — requirements and status
- `outputs/design.md` — architecture document
- `outputs/api-contract.yaml` — OpenAPI specification
- `outputs/data-models.md` — data model definitions
- `outputs/review.md` — reviewer feedback (revision only)
- `outputs/review-checklist.md` — fix checklist (revision only)

## Outputs

- `outputs/src/` — complete Spring Boot source tree with tests
- `outputs/build.gradle.kts` — Gradle Kotlin DSL build file
- `outputs/settings.gradle.kts` — Gradle settings
- `outputs/Dockerfile` — multi-stage Docker build
- `outputs/implementation-notes.md` — decisions and notes
- Updated `task.json` with `"status": "implemented"`
