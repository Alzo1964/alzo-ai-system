# Backup Deployment Rules

## Purpose

Deployment should be backup-aware so releases, migrations, and infrastructure changes do not risk permanent loss of ALZO system context.

## Backup Principles

- Back up PostgreSQL before schema migrations or major application releases.
- Preserve repository history through commits before deployment changes.
- Keep WordPress files, uploads, plugin configuration, and database state recoverable.
- Store backups outside the primary application host when possible.
- Test restore procedures periodically, not only backup creation.

## Pre-Deployment Checklist

- Confirm current environment and target release.
- Confirm recent database backup exists.
- Confirm deployment artifact or commit is traceable.
- Confirm rollback path is documented.
- Confirm credentials and environment variables are available in the target environment.

## WordPress Backup Rules

WordPress deployments should protect uploads, plugin settings, theme assets, and content database state. Plugin updates and landing page launches should have a clear rollback path.

## Backend Backup Rules

Backend deployments should protect PostgreSQL data, migration history, runtime configuration, API secrets, and task or memory records. Failed deployments should not leave partial migrations without a recovery plan.

## Future Automation

Backup verification, release tagging, database snapshots, and rollback checks should eventually become automated deployment gates.
