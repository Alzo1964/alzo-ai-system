# Environment Variables

## Purpose

This document defines the environment variable structure for the ALZO AI System local development environment. Environment variables should make configuration explicit while keeping secrets, machine-specific values, and environment-specific settings out of committed source files.

## Environment Variable Philosophy

Environment variables should be:

- **Readable.** Names should clearly communicate the service or setting they control.
- **Scoped.** Variables should use consistent prefixes by domain or service.
- **Portable.** Local, staging, and production environments should share naming conventions where practical.
- **Secret-safe.** Sensitive values should never be committed to the repository.
- **Automation-friendly.** Future scripts, APIs, dashboards, workers, and agents should read configuration predictably.

## Environment Variable Structure

Recommended prefixes:

| Prefix | Purpose | Example Variables |
| --- | --- | --- |
| `ALZO_` | General ALZO system settings. | `ALZO_ENV`, `ALZO_LOG_LEVEL` |
| `DATABASE_` | PostgreSQL connection settings. | `DATABASE_URL`, `DATABASE_HOST` |
| `API_` | Future API service settings. | `API_PORT`, `API_BASE_URL` |
| `DASHBOARD_` | Future dashboard settings. | `DASHBOARD_PORT`, `DASHBOARD_BASE_URL` |
| `WORKER_` | Future workflow worker settings. | `WORKER_CONCURRENCY`, `WORKER_QUEUE_NAME` |
| `SCHEDULER_` | Future scheduled job settings. | `SCHEDULER_ENABLED`, `SCHEDULER_TIMEZONE` |
| `BACKUP_` | Local backup settings. | `BACKUP_LOCAL_PATH`, `BACKUP_RETENTION_DAYS` |
| `OPENAI_` | Future AI provider settings if needed. | `OPENAI_API_KEY` |

## Baseline Local Variables

A future local `.env` file may include values like:

```text
ALZO_ENV=local
ALZO_LOG_LEVEL=debug

DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_NAME=alzo_ai_local
DATABASE_USER=alzo_local_user
DATABASE_PASSWORD=local-only-password
DATABASE_URL=postgresql://alzo_local_user:local-only-password@localhost:5432/alzo_ai_local
DATABASE_SSL_MODE=disable

API_PORT=3000
DASHBOARD_PORT=5173
WORKER_CONCURRENCY=1
SCHEDULER_ENABLED=true
SCHEDULER_TIMEZONE=Etc/UTC

BACKUP_LOCAL_PATH=./local-backups
BACKUP_RETENTION_DAYS=7
```

These values are examples only. Real secrets and local credentials should remain untracked.

## `.env` Usage Rules

Rules for `.env` files:

- Use `.env` for local-only configuration.
- Do not commit real `.env` files.
- Commit example files only if they contain safe placeholders, such as `.env.example`.
- Keep local, staging, and production values separate.
- Do not reuse local credentials in staging or production.
- Rotate credentials immediately if they are accidentally committed or exposed.
- Prefer a password manager or deployment secret store for shared secrets.

## Sensitive Values

Sensitive values include:

- Database passwords.
- API keys and provider tokens.
- OAuth secrets.
- Session signing secrets.
- Private keys.
- Backup encryption keys.
- Recovery codes.
- Production service URLs when access-controlled.

Sensitive values should live in an untracked local `.env`, password manager, or deployment secret store.

## PostgreSQL Variables

Recommended PostgreSQL variables:

| Variable | Purpose |
| --- | --- |
| `DATABASE_HOST` | PostgreSQL host. |
| `DATABASE_PORT` | PostgreSQL port. |
| `DATABASE_NAME` | Database name for the current environment. |
| `DATABASE_USER` | Database user. |
| `DATABASE_PASSWORD` | Database password. |
| `DATABASE_URL` | Full connection string for application services. |
| `DATABASE_SSL_MODE` | SSL behavior for non-local environments. |

Local PostgreSQL variables should point only to the local development database by default.

## Backup-Safe Development Rules

Environment configuration should reduce risk during development.

Rules:

- Keep local database names visibly local.
- Make destructive commands require explicit environment confirmation.
- Keep backup paths separate from source directories unless intentionally versioned.
- Never default to production credentials or production URLs.
- Fail closed when required configuration is missing.
- Log configuration errors without printing secret values.

## Future Deployment Readiness

Environment variables should prepare the system for later deployment by supporting:

- Separate `local`, `staging`, and `production` environments.
- Environment-specific database URLs.
- API, dashboard, worker, and scheduler configuration.
- Backup destinations and retention settings.
- Secret injection from deployment infrastructure.
- Startup validation for required variables.

Production services should fail clearly when required variables are missing while avoiding disclosure of sensitive values.
