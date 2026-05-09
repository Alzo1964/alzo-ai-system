# Local Development Environment

## Purpose

Define a simple, repeatable local setup for future ALZO AI System development.

## Local Setup Philosophy

- Keep the repository as the source of truth.
- Keep local secrets and generated files out of Git.
- Use safe local defaults that cannot accidentally target production.
- Prefer simple, documented setup steps over hidden machine-specific configuration.

## Recommended Local Tools

- Git
- Docker or Docker Compose
- PostgreSQL client tools
- A Markdown editor
- A password manager or local secret store
- Future runtime/package tools as implementation requires

## PostgreSQL Local Development

- Run PostgreSQL locally through Docker when database work begins.
- Use a local-only database name, user, and password.
- Store credentials in an untracked `.env` file.
- Use synthetic seed data only.
- Run migrations locally before any shared environment.

## Backup-Safe Development Rules

- Never commit secrets, API keys, database dumps, or private credentials.
- Keep local backups separate from source files.
- Do not point local tools at production databases by default.
- Confirm `git status` before and after running generation or automation scripts.

## Future Deployment Readiness

Local development should prepare for staging and production by supporting environment-specific configuration, repeatable migrations, service health checks, and documented startup/shutdown commands.
