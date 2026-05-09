# Environment Variables

## Purpose

Define safe environment variable conventions for local ALZO AI System development.

## Environment Variable Structure

| Prefix | Purpose |
| --- | --- |
| `ALZO_` | General system settings. |
| `DATABASE_` | PostgreSQL configuration. |
| `API_` | Future API service settings. |
| `DASHBOARD_` | Future dashboard settings. |
| `WORKER_` | Future workflow worker settings. |
| `BACKUP_` | Local backup configuration. |

## Example Local Variables

```text
ALZO_ENV=local
ALZO_LOG_LEVEL=debug
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_NAME=alzo_ai_local
DATABASE_USER=alzo_local_user
DATABASE_PASSWORD=local-only-password
DATABASE_URL=postgresql://alzo_local_user:local-only-password@localhost:5432/alzo_ai_local
```

## `.env` Usage Rules

- Use `.env` for local-only configuration.
- Do not commit real `.env` files.
- Commit example files only if they contain safe placeholders.
- Keep local, staging, and production values separate.
- Rotate any credential that is accidentally exposed.

## Backup-Safe Configuration Rules

- Never default to production credentials.
- Keep local database names visibly local.
- Store secrets in an untracked file or secret manager.
- Avoid logging secret values.

## Future Deployment Readiness

Production services should validate required variables on startup and fail clearly when configuration is incomplete.
