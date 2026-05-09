# Deployment Architecture

## Philosophy

Deployment should keep the ALZO AI System stable, recoverable, and easy to evolve. Infrastructure choices should protect durable context, separate environments clearly, and allow the backend, WordPress layer, and database services to scale independently over time.

## Deployment Layers

| Layer | Deployment Role |
| --- | --- |
| WordPress | Public presentation, dashboards, landing pages, and publishing surface. |
| Backend | API, assistant runtime, service layer, task execution, and memory coordination. |
| PostgreSQL | Primary structured data store for users, tasks, workflows, metadata, and audit records. |
| Backup Storage | Durable recovery target for database exports, repository snapshots, and deployment artifacts. |

## Local vs Cloud

Local deployment should support development, testing, documentation review, and safe experimentation. Cloud deployment should support production reliability, public access, backups, monitoring, and secure integrations.

## Core Principles

- Separate presentation, backend, database, and backup responsibilities.
- Keep secrets and environment variables outside versioned files.
- Use repeatable deployment steps rather than manual server drift.
- Protect database state before application changes.
- Design for future scaling without forcing premature microservice complexity.

## Future Scaling

The initial deployment can remain simple, but it should allow later separation of WordPress hosting, backend services, PostgreSQL, queue workers, vector database services, and storage-backed backups.
