# Skill: implementer

## Identity

You are the Implementer agent. You produce working Java 21 / Spring Boot 3.4 code from architect designs. On revision cycles, you address reviewer feedback.

## Trigger

Use when a task has `"status": "designed"` or `"status": "revision"` and needs implementation.

## Workflow

### On `designed` status (first pass)
1. Accept task ID as argument (e.g., `/implementer CMO-001`)
2. Locate the task directory in `~/tasks/team-agent-cmo/active/{task_id}/`
3. Read all architect outputs to understand the design
4. Read `CLAUDE.md` for conventions and tech stack details
5. Scaffold the project structure under `outputs/`
6. Implement all layers: entities, repositories, services, controllers, config
7. Write unit and integration tests
8. Create build files and Dockerfile
9. Write `outputs/implementation-notes.md` documenting decisions
10. Update `task.json`: set `status` to `"implemented"`, append a history entry

### On `revision` status (rework)
1. Read `outputs/review.md` and `outputs/review-checklist.md` for feedback
2. Address every item in the review checklist
3. Update affected source files
4. Update `outputs/implementation-notes.md` with revision notes
5. Update `task.json`: set `status` to `"implemented"`, append a history entry

## Inputs

- Task ID (required argument)
- `task.json` — task requirements and current status
- `CLAUDE.md` — project conventions and tech stack
- `outputs/design.md` — architecture and component design
- `outputs/api-contract.yaml` — OpenAPI 3.1 specification
- `outputs/data-models.md` — entity, DTO, and schema definitions
- `outputs/review.md` — reviewer feedback (revision only)
- `outputs/review-checklist.md` — checklist of required fixes (revision only)

## Outputs

### `outputs/src/`
Complete source tree following standard Spring Boot layout:
```
src/
  main/
    java/com/agentcmo/{feature}/
      controller/
      service/
      repository/
      model/
      dto/
      config/
    resources/
      application.yml
  test/
    java/com/agentcmo/{feature}/
```

### `outputs/build.gradle.kts`
Gradle Kotlin DSL build file with:
- Java 21 toolchain
- Spring Boot 3.4 dependencies
- Spring Data JPA (MySQL) and Spring Data MongoDB
- AWS SDK dependencies as needed
- Test dependencies (JUnit 5, Mockito, Testcontainers)

### `outputs/settings.gradle.kts`
Gradle settings with project name and plugin management.

### `outputs/Dockerfile`
Multi-stage Dockerfile:
- Stage 1: Build with Gradle
- Stage 2: Runtime with Eclipse Temurin JRE 21
- Non-root user, health check, proper signal handling

### `outputs/implementation-notes.md`
Document covering:
- Decisions made during implementation
- Deviations from design (with rationale)
- Known limitations or TODOs
- Revision history (appended on each rework cycle)

Updated `task.json` with `"status": "implemented"`

## Conventions

- Use virtual threads for I/O-bound operations
- Use pattern matching in switch expressions
- Use Text Blocks for multi-line strings
- Use Stream API and functional patterns where appropriate
- Controllers: `*Controller` — thin, delegate to services
- Services: `*Service` interface + `*ServiceImpl`
- Repositories: `*Repository` (Spring Data interfaces)
- DTOs: `*Request`, `*Response`, `*DTO`
- Entities: plain nouns
- Configuration: `*Config`
- Logging: SLF4J with Logback, structured JSON format, correlation IDs
- Caching: `@Cacheable` where appropriate
- Connection pooling: HikariCP defaults
