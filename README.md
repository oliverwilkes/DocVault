# DocVault

Specification and requirements repository for the Customer Document Repository feature.

## About This Project

This repository stores product specifications, functional requirements, and project documentation for the DocVault initiative. It's a collaborative space for the product and development teams to define features before building.

## Quick Start

### Clone the Repository

```bash
git clone https://github.com/oliverwilkes/DocVault.git
cd DocVault
```

## Project Contents

```
DocVault/
├── README.md                           # This file
├── CLAUDE.md                           # Claude Code configuration
├── .claude/settings.json               # Claude Code plugins & settings
└── .temn/
    ├── project-context.md              # Project overview
    └── specs/
        └── 01-customer-document-repository/
            ├── spec.yaml               # Feature specification
            └── spec-functional.md      # Functional requirements
```

## Specifications

### Feature: Customer Document Repository

A centralized vault for customers to view, search, filter, and download their banking documents with read/unread tracking.

**Current Status:** Specification in progress

📄 **View:** `.temn/specs/01-customer-document-repository/`

## Using Claude Code

This project is configured with Claude Code plugins for AI-assisted development and product management:

- **temenos-product-management** — Requirements, roadmaps, feature specs
- **temenos-tooling** — Skill creation and tools
- **temenos-development** — Code review, testing, architecture

Open the project in Claude Code to use these tools:

```bash
claude
```

## Contributing

### Update Specifications

1. Create a feature branch:
   ```bash
   git checkout -b feature/update-specs
   ```

2. Edit specification files in `.temn/specs/`

3. Commit and push:
   ```bash
   git add .
   git commit -m "Update [feature name] specification"
   git push origin feature/update-specs
   ```

4. Create a Pull Request on GitHub for team review

### Git Workflow

Before starting work, pull latest changes:
```bash
git pull origin master
```

Check your status:
```bash
git status
```

## Team Access

Share this repository link with colleagues:

**Repository:** https://github.com/oliverwilkes/DocVault

They can clone it and start contributing immediately. No file overwrites, full version control, complete edit history.

---

**Last Updated:** April 24, 2026
