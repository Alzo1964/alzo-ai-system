# Local Development Environment

## Purpose

This document defines the Phase 2 local development environment for the ALZO AI System. The goal is to create a repeatable, backup-safe, production-aware setup that supports future PostgreSQL development, workflow automation, dashboards, APIs, and AI-assisted operating layers.

The local environment should make the system easy to inspect, run, test, and extend without requiring fragile manual setup or undocumented machine-specific configuration.

## Local Setup Philosophy

The ALZO AI System local development environment should follow these principles:

- **Repository-first setup.** Local tooling should support the repository structure without replacing it as the source of truth.
- **Repeatability.** A future contributor or agent should be able to reproduce the environment from documented steps.
- **Separation of configuration and code.** Local secrets, machine-specific values, and credentials should stay outside committed files.
- **Production awareness.** Local development should mirror production architecture where practical without overcomplicating early development.
- **Backup safety.** Local testing should not overwrite, delete, or corrupt source-of-truth documents, backups, or production-like data.
- **Incremental complexity.** Add services such as PostgreSQL, workers, dashboards, and APIs only when the workflow requires them.

## Recommended Local Tools

| Tool | Purpose |
| --- | --- |
| Git | Version control, local history, and branch management. |
| Docker / Docker Compose | Local service orchestration for PostgreSQL and future workers or APIs. |
| PostgreSQL client | Database inspection, migration validation, and local query testing. |
| Runtime package manager | Dependency installation for future application code. |
| Task runner | Consistent commands for setup, validation, testing, and service startup. |
| Markdown editor | Documentation review and source-of-truth editing. |
| Secret manager | Safe storage for credentials outside the repository. |

## Recommended Local Setup Flow

A mature local setup should support this sequence:

```text
1. Clone the repository.
2. Review documentation and development requirements.
3. Copy the example environment file when one exists.
4. Add local-only values to an untracked .env file.
5. Start Docker-managed local services.
6. Run database migrations when implementation exists.
7. Start application, dashboard, API, or worker processes.
8. Run validation checks.
9. Commit only intentional source changes.
```

## PostgreSQL Local Development Approach

PostgreSQL should run locally through Docker or a clearly documented local installation.

Recommended approach:

- Use Docker Compose for a consistent PostgreSQL service when application development begins.
- Keep local database credentials in `.env` or a local secret manager, not in committed files.
- Use a dedicated local database name for ALZO development.
- Store schema migrations in the repository once implementation begins.
- Use seed data that is safe, synthetic, and non-sensitive.
- Avoid importing production or sensitive personal data into local development unless a documented security process exists.
- Validate migrations locally before applying them to shared or production-like environments.

## Backup-Safe Development Rules

Local development must protect repository continuity and future recoverability.

Rules:

- Do not store secrets, tokens, private keys, or recovery codes in committed files.
- Do not use local scripts that delete repository content without explicit review.
- Do not overwrite source-of-truth Markdown files with generated output unless the change is intentional and reviewed.
- Keep generated files, caches, local databases, and temporary exports out of Git unless explicitly approved.
- Use separate local databases for experiments and production-like validation.
- Take a local snapshot before high-risk migrations or destructive tests.
- Confirm `git status` before and after local automation runs.

## Future Deployment Readiness

The local development environment should prepare the system for future deployment without forcing deployment complexity too early.

Deployment-ready local development should eventually support:

- Documented startup and shutdown commands.
- Environment-specific configuration separation.
- Repeatable database migrations.
- Health checks for API, dashboard, workers, and PostgreSQL.
- Automated validation commands.
- Safe secrets handling.
- Backup and restore rehearsal for local databases.
- Clear distinction between local, staging, and production settings.

## Validation Expectations

When implementation begins, the local development package should define exact commands for:

- Installing dependencies.
- Starting local services.
- Running database migrations.
- Running tests.
- Checking formatting and linting.
- Starting dashboards, APIs, and workflow workers.
- Stopping and resetting local services safely.
