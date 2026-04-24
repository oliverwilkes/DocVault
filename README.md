# DocVault

A centralized vault for customers to view, search, filter, and download their banking documents with read/unread tracking and new document notifications.

## Quick Start

### Clone the Repository

```bash
git clone https://github.com/oliverwilkes/DocVault.git
cd DocVault
```

### Prerequisites

- **Java 17** or higher
- **MySQL 8.0** or higher
- **Maven 3.8+**

### Database Setup

```sql
CREATE DATABASE IF NOT EXISTS docvault;
CREATE USER IF NOT EXISTS 'vault_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON docvault.* TO 'vault_user'@'localhost';
FLUSH PRIVILEGES;
```

### Environment Variables

Set these before running the application:

```bash
# Linux/Mac
export SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/docvault
export SPRING_DATASOURCE_USERNAME=vault_user
export SPRING_DATASOURCE_PASSWORD=password

# Windows PowerShell
$env:SPRING_DATASOURCE_URL="jdbc:mysql://localhost:3306/docvault"
$env:SPRING_DATASOURCE_USERNAME="vault_user"
$env:SPRING_DATASOURCE_PASSWORD="password"
```

### Start the API

```bash
.\mvnw.cmd spring-boot:run    # Windows
./mvnw spring-boot:run         # Linux/Mac
```

The API will be available at `http://localhost:8080/api/v1`

**Swagger UI:** `http://localhost:8080/swagger-ui.html`
**Health Check:** `http://localhost:8080/actuator/health`

---

## Project Structure

```
DocVault/
├── README.md                          # This file
├── CLAUDE.md                          # Claude Code project instructions
├── .gitignore                         # Git ignore rules
├── pom.xml                            # Maven configuration
├── src/
│   └── main/java/com/docvault/
│       ├── api/
│       │   ├── controller/            # REST controllers
│       │   └── dto/                   # Request/response DTOs
│       ├── config/                    # Spring configuration
│       ├── domain/
│       │   ├── model/                 # JPA entities
│       │   └── repository/            # Spring Data repositories
│       ├── exception/                 # Custom exceptions + global error handler
│       ├── service/                   # Business logic
│       └── DocvaultApplication.java   # Spring Boot entry point
├── src/test/java/com/docvault/       # Unit & integration tests
├── src/main/resources/
│   ├── application.properties         # Spring configuration
│   └── db/migration/                  # Flyway SQL migrations
└── .temn/                             # Project specifications & context
    ├── project-context.md             # Technical architecture overview
    └── specs/
        └── 01-customer-document-repository/
            ├── spec.yaml              # Feature specification
            └── spec-functional.md     # Functional requirements
```

## Specifications

### Feature: Customer Document Repository

**Status:** Specification in progress | Functional complete | Technical not started

A centralized document vault for customers (retail, business, SME) to manage banking documents.

**Phase 1 (Current Focus):**
- Document list view with filtering and search
- Individual document download
- Read/unread status tracking
- New document notifications

**Future Phases:**
- Bulk download, document sharing, printing, annotations, customer upload, retention management

📄 **Full spec:** `.temn/specs/01-customer-document-repository/`

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| **Framework** | Spring Boot 3.x |
| **Language** | Java 17 |
| **Build Tool** | Maven |
| **Database** | MySQL 8.0 |
| **ORM** | Spring Data JPA / Hibernate |
| **Migrations** | Flyway |
| **API Docs** | SpringDoc OpenAPI (Swagger UI) |
| **Testing** | JUnit 5 + Mockito |
| **Coverage** | Target: 80% |

---

## Development Workflow

### Running Tests

```bash
# Run all tests
.\mvnw.cmd test

# Run a single test class
.\mvnw.cmd test -Dtest=DocumentServiceTest

# Run integration tests only
.\mvnw.cmd verify -P integration-test

# Build without running tests
.\mvnw.cmd clean package -DskipTests
```

### Code Quality

```bash
# Check code style with Checkstyle
.\mvnw.cmd checkstyle:check
```

### API Development

- **REST endpoints:** `/api/v1/...`
- **DTOs:** Use separate request/response classes in `api/dto/`
- **Controllers:** Thin layer, delegate to services
- **Services:** Contain business logic, injected via constructor
- **Repositories:** Spring Data JPA interfaces only

---

## Git Workflow

### Before You Start

Ensure git is configured:

```bash
git config --local user.name "Your Name"
git config --local user.email "your.email@temenos.com"
```

### Creating a Feature Branch

```bash
# Create and switch to a new feature branch
git checkout -b feature/document-filtering

# Make changes, then commit
git add .
git commit -m "Add document filtering by document type"

# Push your branch
git push origin feature/document-filtering
```

### Merging Changes

1. Push your branch to GitHub
2. Create a Pull Request on GitHub
3. Request team review
4. Once approved, merge to `master`
5. Delete the feature branch

### Pulling Latest Changes

Before starting work, always pull the latest:

```bash
git pull origin master
```

---

## Claude Code Integration

This project includes **Claude Code** plugins for AI-assisted development:

### Installed Plugins

- **temenos-product-management** — Requirements, roadmaps, specifications
- **temenos-tooling** — Skill creation and customization
- **temenos-development** — Development workflows, code review, testing

### Using Claude Code

Open the project in Claude Code:

```bash
# From project root
claude
```

Available commands:
- `/temn-open-pr` — Create pull requests with quality analysis
- `/temn-review-pr` — Review existing PRs
- `/temn-dev` — Generic development assistance
- `/temn-test` — Generate test suites
- `/temn-requirements` — Manage feature requirements

See `CLAUDE.md` for detailed project conventions.

---

## Common Tasks

### View Git Log

```bash
git log --oneline -10
```

### Check Branch Status

```bash
git status
```

### Switch Branches

```bash
git checkout master
git checkout feature/my-feature
```

### Discard Local Changes

```bash
git checkout -- .
```

### Delete a Local Branch

```bash
git branch -d feature/my-feature
```

---

## Troubleshooting

### Maven Build Issues

**Problem:** Build fails with "stale bytecode"
**Solution:**
```bash
.\mvnw.cmd clean spring-boot:run
```

### Port 8080 Already in Use

**Problem:** "Address already in use"
**Solution (Windows):**
```powershell
netstat -ano | findstr ":8080"
taskkill /F /PID <pid>
```

**Solution (Linux/Mac):**
```bash
lsof -i :8080
kill -9 <pid>
```

### Database Connection Failed

**Problem:** "Cannot connect to MySQL"
**Checklist:**
- MySQL service is running
- Database `docvault` exists
- User `vault_user` has correct password
- Environment variables are set correctly

---

## Contributing

### Code Style

- Follow [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
- Run `mvn checkstyle:check` before committing
- Use meaningful variable names

### Testing

- Write unit tests for services (target 80% coverage)
- Write integration tests for API endpoints
- Test both happy path and error cases
- Naming: `{ClassName}Test.java` (unit), `{ClassName}IT.java` (integration)

### Commits

- Write clear, descriptive commit messages
- Reference feature IDs when relevant: `feat: Add document list filtering [#01]`
- Keep commits atomic (one logical change per commit)

---

## Architecture

### Layered Architecture

```
API Layer (Controllers)
    ↓
Service Layer (Business Logic)
    ↓
Repository Layer (Data Access)
    ↓
Database (MySQL)
```

### Key Principles

- **Controllers** are thin — delegate to services immediately
- **Services** contain business logic and handle transactions
- **Repositories** expose only interfaces; Spring Data JPA provides implementations
- **DTOs** isolate API contract from internal domain models
- **Exceptions** handled globally via `@ControllerAdvice`

---

## Resources

- **Spring Boot Docs:** https://spring.io/projects/spring-boot
- **Spring Data JPA:** https://spring.io/projects/spring-data-jpa
- **Flyway Migrations:** https://flywaydb.org/documentation
- **Maven:** https://maven.apache.org/

---

## Contact & Support

For questions or issues:
- **Owner:** Oliver Wilkes (owilkes@temenos.com)
- **Repository:** https://github.com/oliverwilkes/DocVault
- **Issues:** Create a GitHub issue with a clear description

---

**Last Updated:** April 24, 2026
