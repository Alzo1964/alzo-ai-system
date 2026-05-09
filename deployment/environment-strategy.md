# Environment Strategy

## Purpose

Environment separation protects production stability while allowing safe development, testing, and staging workflows.

## Environments

| Environment | Purpose |
| --- | --- |
| Local | Docker Compose environment for FastAPI, PostgreSQL, WordPress-adjacent integration testing, documentation review, and isolated experiments. |
| Staging | Production-like validation for integrations, migrations, releases, and user acceptance. |
| Production | Live system for public presentation, backend services, database records, and operational workflows. |

## Configuration Rules

- Use separate environment variables for each environment.
- Use Docker Compose for local development only, not as the full production operations model.
- Use separate databases for local, staging, and production.
- Keep production credentials out of local files and repository history.
- Restrict production write access to approved deployment and admin processes.
- Validate integrations in staging before production rollout.

## WordPress Separation

WordPress staging should mirror production themes, plugins, and content structures where practical. Publishing tests, dashboard modules, and campaign pages should be validated in staging before public launch.

## Backend Separation

Backend staging should validate API contracts, assistant runtime behavior, task execution, memory access, and database migrations before production deployment.

## Data Handling

Production data should not be copied into local or staging environments unless sanitized. Sensitive memory, user data, credentials, and personal continuity context should be protected by default.
