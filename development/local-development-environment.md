# Local Development Environment

## Purpose

This document defines the Phase 2 local development package for the ALZO AI System. It describes how local work should be set up so future PostgreSQL services, workflow engines, dashboards, APIs, and automation workers can be developed safely and consistently.

The local environment should be repeatable, transparent, backup-safe, and production-aware without adding unnecessary complexity before implementation begins.

## Local Setup Philosophy

Local development should follow these principles:

- **Repository-first.** The repository remains the source of truth for architecture, policies, schemas, templates, and workflow documentation.
- **Repeatable setup.** A future operator, contributor, or AI agent should be able to recreate the environment from documented steps.
- **Clear separation.** Source files, generated files, local secrets, databases, and backups should remain clearly separated.
- **Safe defaults.** Local tools should default to local services and never connect to production accidentally.
- **Production awareness.** Local structure should prepare for staging and production without requiring production-grade complexity on day one.
- **Observable behavior.** Services should provide logs, status checks, and validation commands when implementation begins.

## Recommended Local Tools

| Tool | Purpose |
| --- | --- |
| Git | Version control, branch management, and recovery through history. |
| Docker Desktop or Docker Engine | Local containers for PostgreSQL and future services. |
| Docker Compose | Coordinated startup for PostgreSQL, APIs, dashboards, workers, and schedulers. |
| PostgreSQL client tools | Local database inspection, migrations, restore testing, and query validation. |
| Runtime package manager | Future dependency management for application, API, dashboard, or worker code. |
| Task runner | Consistent commands for setup, tests, migrations, and service orchestration. |
| Markdown editor | Review and maintenance of repository-native documentation. |
| Password manager or secret store | Safe handling of credentials outside the repository. |

## Recommended Local Setup Flow

When implementation begins, the local setup should follow this pattern:

```text
1. Clone the repository.
2. Review the development documentation.
3. Install required local tools.
4. Create an untracked .env file from safe example values.
5. Start Docker-managed local services.
6. Run database migrations.
7. Seed safe local development data if needed.
8. Start API, dashboard, worker, or scheduler services.
9. Run validation checks.
10. Confirm git status before committing source changes.
```

## PostgreSQL Local Development Approach

PostgreSQL should be the first local service introduced when structured state implementation begins.

Recommended approach:

- Run PostgreSQL through Docker Compose for predictable local setup.
- Use a dedicated local database such as `alzo_ai_local`.
- Store local database credentials in an untracked `.env` file or local secret manager.
- Use synthetic seed data instead of real personal, production, or sensitive data.
- Store migrations in the repository once schema implementation begins.
- Validate migrations locally before applying them to shared environments.
- Keep destructive reset commands limited to local databases and clearly labeled.

## Backup-Safe Development Rules

Local development must protect repository continuity and avoid accidental data loss.

Rules:

- Never commit secrets, API keys, tokens, passwords, private keys, or recovery codes.
- Never point local defaults at production databases, production backups, or sensitive services.
- Keep generated dumps, caches, local volumes, and temporary exports out of Git unless explicitly approved.
- Use separate local databases for experiments, migration tests, and production-like validation.
- Take local snapshots before destructive migration tests.
- Confirm `git status` before and after running automation or generation scripts.
- Prefer reversible operations and documented reset commands.

## Future Deployment Readiness

The local environment should prepare for deployment by keeping local, staging, and production concerns distinct.

Future readiness should include:

- Environment-specific configuration.
- Repeatable migrations.
- Health checks for PostgreSQL, APIs, dashboards, workers, and schedulers.
- Clear startup and shutdown commands.
- Backup and restore rehearsal for database services.
- Validation commands for tests, formatting, linting, and migrations.
- Documented secret handling for local and deployed environments.

## Validation Expectations

Future implementation should define exact commands for:

- Installing dependencies.
- Starting local services.
- Stopping local services.
- Running migrations.
- Seeding local data.
- Running tests and validation checks.
- Creating and restoring local database backups.
- Resetting local services safely.
