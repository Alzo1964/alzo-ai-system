# Docker Strategy

## Purpose

Define a lightweight Docker strategy for future ALZO AI System local development.

## Docker Usage Strategy

Docker should provide repeatable local services without hiding system behavior.

Primary uses:

- Run local PostgreSQL.
- Support future API, dashboard, worker, and scheduler services.
- Provide safe reset, backup, and restore workflows for local development.

## Recommended Containers

| Container | Purpose |
| --- | --- |
| `postgres` | Local PostgreSQL database. |
| `api` | Future backend API. |
| `dashboard` | Future dashboard UI. |
| `worker` | Future automation worker. |
| `scheduler` | Future recurring job scheduler. |

## PostgreSQL Local Development Approach

- Use Docker Compose for PostgreSQL when implementation begins.
- Use named volumes for local persistence.
- Configure credentials through environment variables.
- Use synthetic seed data.
- Keep reset commands limited to local data.

## `.env` and Docker Rules

- Do not commit real `.env` files.
- Do not bake secrets into Docker images.
- Do not hardcode secrets in Compose files.
- Keep production secrets in deployment infrastructure.

## Backup-Safe Docker Rules

- Keep database dumps out of Git unless sanitized and approved.
- Make destructive commands clearly local-only.
- Do not treat Docker volumes as the only backup of important data.
- Avoid logging secrets or sensitive personal context.

## Future Deployment Readiness

Future Docker work should support health checks, graceful shutdown, repeatable builds, controlled migrations, and separate local/staging/production configuration.
