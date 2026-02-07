# My Project

## What This Is
Agent CMO (Chief Memory Officer) template folder structure that provides a standard template utilizing coding AI agents for software development.

## Tech Stack
- Java 21 + Framework Spring Boot 3.4
- Build tool: Gradle 8.x with Kotlin DSL
- MongoDB
- MySQL
- Cloud: AWS (ECS, RDS, S3, SQS, SNS, AWS Lambda Function)


## Conventions
- Leverage **pattern matching** in switch expressions
- Use **virtual threads** (Project Loom) for I/O-bound operations
- Prefer **Text Blocks** for multi-line strings (SQL, JSON templates)
- Use **Stream API** and functional patterns where appropriate


### Naming Conventions
- Controllers: `*Controller` (e.g., `UserController`)
- Services: `*Service` with interface + `*ServiceImpl`
- Repositories: `*Repository` (Spring Data interfaces)
- DTOs: `*Request`, `*Response`, `*DTO`
- Entities: Plain nouns (e.g., `User`, `Order`)
- Configuration: `*Config`

## AWS Integration Patterns
### AWS SDK Usage
- Implement proper credential chain (IAM roles over access keys)
- Handle AWS exceptions appropriately

## Observability
### Logging
- Use SLF4J with Logback
- Log at appropriate levels (ERROR, WARN, INFO, DEBUG)
- Include correlation IDs for request tracking
- Use structured logging (JSON format)

## Docker
- Create multi-stage Dockerfiles

## Performance Considerations
- Enable virtual threads: `spring.threads.virtual.enabled=true`
- Use connection pooling (HikariCP)
- Implement caching with `@Cacheable`
- Use async processing for long-running tasks
- Monitor heap usage and GC behavior