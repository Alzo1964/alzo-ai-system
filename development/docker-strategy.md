# Docker Strategy

## Purpose

This document defines the Docker strategy for Phase 2 local development of the ALZO AI System. Docker should provide repeatable local services for PostgreSQL, future APIs, dashboards, workers, and automation without making the repository dependent on opaque or fragile machine-specific setup.

## Docker Usage Strategy

Docker should be used to standardize infrastructure services, not to hide system behavior.

Primary uses:

- Run PostgreSQL locally with consistent configuration.
- Provide future service containers for APIs, dashboards, workflow workers, and schedulers.
- Keep local service startup predictable across machines.
- Support safe reset and rebuild workflows for development databases.
- Prepare for future staging and production deployment patterns.

Docker should remain optional for documentation-only work and required only when services need to run locally.

## Recommended Container Roles

| Container | Purpose |
| --- | --- |
| `postgres` | Local PostgreSQL database for development and schema testing. |
| `api` | Future backend API service. |
| `dashboard` | Future web dashboard or local UI. |
| `worker` | Future automation or workflow worker. |
| `scheduler` | Future recurring job and reminder scheduler. |
| `adminer` / `db-ui` | Optional local database inspection tool. |

## PostgreSQL Local Development Approach

PostgreSQL should be the first Docker-managed service when implementation begins.

Recommended PostgreSQL strategy:

- Use a named Docker volume for local database persistence.
- Use environment variables for database user, password, database name, and port.
- Keep local credentials untracked and development-only.
- Mount migrations only when implementation exists.
- Use synthetic seed data for local testing.
- Provide a safe reset command that affects only the local development database.

Local PostgreSQL should be isolated from staging and production. No local container should default to a production connection string.

## Docker Compose Guidelines

A future `docker-compose.yml` should be designed for clarity.

Guidelines:

- Keep service names simple and domain-specific.
- Use environment variables rather than hardcoded secrets.
- Use health checks for PostgreSQL and future API services.
- Use named volumes for persistent local service data.
- Avoid mounting sensitive host directories unless necessary.
- Keep ports configurable through environment variables.
- Document startup, shutdown, reset, and backup commands.

## `.env` and Docker

Docker should load local configuration from an untracked `.env` file when needed.

Rules:

- Do not commit real `.env` files.
- Do not bake secrets into Docker images.
- Do not place secrets in Dockerfiles, compose files, or logs.
- Use safe placeholder values in examples.
- Keep production secrets in deployment infrastructure, not local Docker configuration.

## Backup-Safe Docker Rules

Docker workflows should protect local and repository data.

Rules:

- Destructive database reset commands should clearly state they affect local data only.
- Local database volumes should not be treated as the only copy of important data.
- Backups created from containers should be written to clearly named local backup paths.
- Generated dumps should be excluded from Git unless explicitly sanitized and approved.
- Migration tests should run against local or disposable databases before shared environments.
- Container logs should not include secrets or sensitive personal context.

## Future Deployment Readiness

The Docker strategy should prepare the ALZO AI System for later deployment while preserving local simplicity.

Future readiness goals:

- Separate local Docker Compose from staging or production deployment configuration.
- Keep images buildable from documented steps.
- Support health checks and graceful shutdown.
- Support database migration execution as a controlled step.
- Support worker and scheduler services independently from the API.
- Support environment-specific configuration without changing source files.
- Keep backup and restore workflows documented for database services.

## Operational Commands to Define Later

When implementation begins, the development package should define exact commands for:

```text
Start local services
Stop local services
View service logs
Run migrations
Seed local data
Reset local database
Create local database backup
Restore local database backup
Run tests against Docker services
```

These commands should be safe, repeatable, and clear enough for future agents and human operators to use confidently.
