# Docker Strategy

## Purpose

This document defines the Docker strategy for the ALZO AI System Phase 2 local development package. Docker should provide consistent local infrastructure for PostgreSQL and future services while keeping system behavior transparent, inspectable, and safe.

## Docker Usage Strategy

Docker should standardize local services, not obscure how the system works.

Primary uses:

- Run PostgreSQL locally with predictable configuration.
- Support future API, dashboard, workflow worker, and scheduler services.
- Provide consistent startup and shutdown behavior across machines.
- Support safe local database reset, migration, backup, and restore workflows.
- Prepare for future staging and production container patterns without requiring them immediately.

Docker should be optional for documentation-only work and required only when local services need to run.

## Recommended Container Roles

| Container | Purpose |
| --- | --- |
| `postgres` | Local PostgreSQL database for schema and application development. |
| `api` | Future backend API service. |
| `dashboard` | Future dashboard or local UI. |
| `worker` | Future workflow and automation worker. |
| `scheduler` | Future recurring job, check-in, and reminder scheduler. |
| `db-ui` | Optional local database inspection tool. |

## PostgreSQL Local Development Approach

PostgreSQL should be the first Docker-managed service introduced during implementation.

Recommended approach:

- Use Docker Compose to run PostgreSQL locally.
- Use a named Docker volume for local database persistence.
- Configure database user, password, name, and port through environment variables.
- Keep local credentials untracked and development-only.
- Use synthetic seed data for local testing.
- Mount migrations only when schema implementation exists.
- Provide reset commands that clearly affect only local development data.

Local PostgreSQL should never default to staging or production connection strings.

## Docker Compose Guidelines

A future Compose file should follow these guidelines:

- Use clear service names.
- Keep ports configurable through environment variables.
- Use health checks for PostgreSQL and future services.
- Use named volumes for persistent local data.
- Avoid hardcoded secrets.
- Avoid mounting sensitive host directories.
- Keep startup, shutdown, logs, reset, backup, and restore commands documented.

## `.env` and Docker

Docker may load local configuration from an untracked `.env` file.

Rules:

- Do not commit real `.env` files.
- Do not bake secrets into Docker images.
- Do not place secrets in Dockerfiles, Compose files, or logs.
- Use safe placeholder values in examples.
- Keep production secrets in deployment infrastructure, not local Docker files.

## Backup-Safe Docker Rules

Docker workflows should protect both repository files and local development data.

Rules:

- Destructive reset commands must identify the affected local service or volume.
- Local Docker volumes should not be treated as the only copy of important data.
- Database dumps should be written to clearly named backup paths.
- Generated dumps and temporary exports should stay out of Git unless sanitized and approved.
- Migration tests should run against local or disposable databases before shared environments.
- Container logs should not print secrets, credentials, or sensitive personal context.

## Future Deployment Readiness

The Docker strategy should support future deployment maturity while preserving local simplicity.

Future readiness goals:

- Separate local Compose files from staging or production deployment configuration.
- Keep images buildable from documented steps.
- Support health checks and graceful shutdown.
- Support controlled database migration execution.
- Allow workers and schedulers to run independently from the API.
- Support environment-specific configuration without changing source files.
- Keep backup and restore procedures documented for database services.

## Operational Commands to Define Later

When implementation begins, define exact commands for:

```text
Start local services
Stop local services
View service logs
Run database migrations
Seed local data
Reset the local database
Create a local database backup
Restore a local database backup
Run tests against Docker services
```

Commands should be safe, repeatable, and clear enough for future agents and human operators to use confidently.
