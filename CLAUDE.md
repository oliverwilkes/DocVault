# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

DOCVAULT is a Spring Boot 3.x backend API (Java 17, MySQL) with a layered architecture (Controller → Service → Repository).

## Commands

```powershell
# Start the API
.\mvnw.cmd spring-boot:run

# Run all tests
.\mvnw.cmd test

# Run a single test class
.\mvnw.cmd test -Dtest=DocumentServiceTest

# Run integration tests only
.\mvnw.cmd verify -P integration-test

# Build without tests
.\mvnw.cmd clean package -DskipTests

# Check code style
.\mvnw.cmd checkstyle:check
```

## Architecture

Layered pattern under `src/main/java/com/docvault/`:

```
api/controller/     → REST controllers (@RestController), thin — delegate immediately to service
api/dto/            → Request/response DTOs (no JPA entities in API layer)
config/             → Spring @Configuration classes (security, CORS, beans)
domain/model/       → JPA @Entity classes
domain/repository/  → Spring Data JPA repositories (interfaces only)
exception/          → Custom exceptions + @ControllerAdvice global handler
service/            → Business logic; injected via constructor, not field injection
```

Key conventions:
- API versioning: `/api/v1/...`
- Flyway migrations: `src/main/resources/db/migration/V{n}__{description}.sql`
- Unit tests: `{ClassName}Test.java` | Integration tests: `{ClassName}IT.java`
- 80% test coverage target — services and exception paths are priority

## Database Setup

```sql
CREATE DATABASE IF NOT EXISTS docvault;
CREATE USER IF NOT EXISTS 'vault_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON docvault.* TO 'vault_user'@'localhost';
FLUSH PRIVILEGES;
```

Flyway runs migrations automatically on startup.

## Environment

| Variable | Example |
|----------|---------|
| `SPRING_DATASOURCE_URL` | `jdbc:mysql://localhost:3306/docvault` |
| `SPRING_DATASOURCE_USERNAME` | `vault_user` |
| `SPRING_DATASOURCE_PASSWORD` | `password` |

## Ports

- API: `http://localhost:8080/api/v1`
- Swagger UI: `http://localhost:8080/swagger-ui.html`
- Health: `http://localhost:8080/actuator/health`

## Platform Notes

- Windows environment — use `.\mvnw.cmd` (not `./mvnw`)
- Kill stale Java processes: `netstat -ano | findstr ":8080"` then `taskkill /F /PID <pid>`
- Always use `mvn clean spring-boot:run` (not plain `mvn run`) to avoid stale bytecode
