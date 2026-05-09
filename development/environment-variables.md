# Environment Variables

## Purpose

This document defines the environment variable structure and `.env` usage rules for the ALZO AI System local development environment. Environment variables should keep configuration explicit, portable, and safe while preventing secrets or machine-specific values from entering the repository.

## Environment Variable Philosophy

Environment variables should be:

- **Explicit.** Names should clearly describe what they configure.
- **Scoped.** Variables should be grouped by system domain or service.
- **Portable.** Local development, staging, and production should use the same naming conventions where practical.
- **Secret-safe.** Sensitive values should never be committed to the repository.
- **Automation-friendly.** Future agents, scripts, APIs, dashboards, and workers should be able to read configuration predictably.

## Recommended Structure

Use clear prefixes to group variables by purpose.

| Prefix | Purpose | Examples |
| --- | --- | --- |
| `ALZO_` | General ALZO system configuration. | `ALZO_ENV`, `ALZO_LOG_LEVEL` |
| `DATABASE_` | PostgreSQL connection and database settings. | `DATABASE_URL`, `DATABASE_NAME` |
| `API_` | Future API service configuration. | `API_PORT`, `API_BASE_URL` |
| `DASHBOARD_` | Future dashboard configuration. | `DASHBOARD_PORT` |
| `WORKER_` | Automation and workflow worker settings. | `WORKER_CONCURRENCY` |
| `BACKUP_` | Local backup and restore settings. | `BACKUP_LOCAL_PATH` |
| `OPENAI_` | Future AI provider configuration if needed. | `OPENAI_API_KEY` |

## Baseline Local Variables

A future local `.env` file may include values such as:

```text
ALZO_ENV=local
ALZO_LOG_LEVEL=debug

DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_NAME=alzo_ai_local
DATABASE_USER=alzo_local_user
DATABASE_PASSWORD=local-only-password
DATABASE_URL=postgresql://alzo_local_user:local-only-password@localhost:5432/alzo_ai_local

API_PORT=3000
DASHBOARD_PORT=5173
WORKER_CONCURRENCY=1

BACKUP_LOCAL_PATH=./local-backups
```

These values are examples only. Real credentials and sensitive values should remain local and untracked.

## `.env` Usage Rules

Rules for `.env` files:

- `.env` files should be local-only and untracked.
- Commit example files only when they contain safe placeholders, such as `.env.example`.
- Never commit real passwords, API keys, access tokens, private keys, or recovery codes.
- Keep local development credentials separate from staging or production credentials.
- Rotate credentials if they are accidentally committed or exposed.
- Prefer a secret manager for sensitive shared credentials.
- Keep environment variable names stable once automation depends on them.

## Sensitive Values

Sensitive values include:

- Database passwords.
- API keys.
- OAuth secrets.
- Session signing secrets.
- Private keys.
- Backup encryption keys.
- Recovery codes.
- Production service URLs when access-controlled.

Sensitive values should be stored in a local secret manager, deployment secret store, or untracked local environment file.

## PostgreSQL Variables

PostgreSQL local development should use explicit database settings.

Recommended variables:

| Variable | Purpose |
| --- | --- |
| `DATABASE_HOST` | PostgreSQL host. |
| `DATABASE_PORT` | PostgreSQL port. |
| `DATABASE_NAME` | Local database name. |
| `DATABASE_USER` | Local database user. |
| `DATABASE_PASSWORD` | Local-only database password. |
| `DATABASE_URL` | Full connection string for applications and tools. |
| `DATABASE_SSL_MODE` | SSL mode when needed for non-local environments. |

Local PostgreSQL credentials should be simple enough for development but never reused in production.

## Backup-Safe Configuration Rules

Environment configuration should support safe local work.

Rules:

- Use separate database names for local, staging, and production.
- Make destructive commands require explicit environment confirmation.
- Keep backup output paths outside source directories unless intentionally versioned.
- Do not point local tools at production databases by default.
- Prefer safe defaults that fail closed rather than connecting to sensitive systems accidentally.

## Future Deployment Readiness

Environment variables should prepare the system for future deployment by supporting:

- Environment-specific configuration: `local`, `staging`, and `production`.
- Separate database URLs for each environment.
- API and dashboard base URLs.
- Worker concurrency and queue configuration.
- Backup destinations and retention settings.
- Secrets supplied by deployment infrastructure rather than committed files.

A production deployment should validate required variables on startup and fail clearly when configuration is incomplete.
