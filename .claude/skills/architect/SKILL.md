# Skill: architect

## Purpose

Run the Architect agent on a task. Reads requirements and produces system design, API contracts, and data models.

## Trigger

Use when a task has `"status": "open"` and needs architecture and design work.

## Workflow

1. Accept task ID as argument (e.g., `/architect CMO-001`)
2. Locate the task directory in `~/tasks/team-agent-cmo/backlog/{task_id}/` or `~/tasks/team-agent-cmo/active/{task_id}/`
3. Read `.claude/agents/ARCHITECT.md` for full agent instructions
4. Read `task.json` for requirements
5. Read `CLAUDE.md` for project conventions
6. Produce design artifacts in `outputs/`
7. Update `task.json` status to `"designed"`
8. Move task from `backlog/` to `active/` if needed

## Inputs

- Task ID (required argument)
- `task.json` — requirements and acceptance criteria
- `CLAUDE.md` — tech stack and conventions

## Outputs

- `outputs/design.md` — architecture document with Mermaid diagrams
- `outputs/api-contract.yaml` — OpenAPI 3.1 specification
- `outputs/data-models.md` — entities, DTOs, and database schemas
- Updated `task.json` with `"status": "designed"`
