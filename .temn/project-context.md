# Project Context

Generated: 2026-04-24
Mode: New Project (user-configured)
Confidence: 10/10

## Project Identity

- **Name:** DOCVAULT
- **Type:** Backend API
- **Domain:** General (TBD)
- **Root:** C:\DOCVAULT

## Tech Stack

### Backend
- **Framework:** Spring Boot 3.x
- **Language:** Java 17
- **Build Tool:** Maven
- **Database:** MySQL
- **ORM:** Spring Data JPA / Hibernate
- **Migrations:** Flyway
- **API Docs:** SpringDoc OpenAPI (Swagger UI)

### Testing
- **Framework:** JUnit 5 + Mockito
- **Coverage Target:** 80%
- **Integration Tests:** Spring Boot Test + Testcontainers (MySQL)

### Quality
- **Code Style:** Google Java Format / Checkstyle
- **Static Analysis:** SpotBugs / PMD (optional)

## Architecture

- **Pattern:** Layered
- **Structure:**
  ```
  src/main/java/com/docvault/
  ├── api/
  │   ├── controller/     # REST controllers
  │   └── dto/            # Request/response DTOs
  ├── config/             # Spring configuration classes
  ├── domain/
  │   ├── model/          # JPA entities
  │   └── repository/     # Spring Data repositories
  ├── exception/          # Custom exceptions + global handler
  ├── service/            # Business logic
  └── DocvaultApplication.java
  ```

## Conventions

- **File Naming:** PascalCase for Java classes; kebab-case for SQL migrations
- **Package Naming:** Feature-based packages under `com.docvault`
- **API Versioning:** URI versioning (`/api/v1/...`)
- **Migration Naming:** `V{n}__{description}.sql`
- **Test Naming:** `{ClassName}Test.java` (unit), `{ClassName}IT.java` (integration)

## Port Assignments

| Service | Port |
|---------|------|
| Backend (Spring Boot) | 8080 |
| Swagger UI | 8080/swagger-ui.html |

## Environment Variables

| Variable | Description |
|----------|-------------|
| `SPRING_DATASOURCE_URL` | MySQL JDBC URL |
| `SPRING_DATASOURCE_USERNAME` | DB username |
| `SPRING_DATASOURCE_PASSWORD` | DB password |

## Status

- Initialization: Complete
- Codebase: Greenfield (not yet scaffolded)
