# PostgreSQL Architecture

## Purpose

This document defines the initial PostgreSQL architecture for the ALZO AI System. PostgreSQL is the preferred relational data layer for structured operational state, task orchestration, memory metadata, assistant interactions, reminders, project records, decision history, logs, and future API-backed workflows.

The repository remains the human-readable source of truth for architecture, policies, templates, and durable documentation. PostgreSQL should support execution, retrieval, automation, and dashboard visibility without replacing repository governance.

## Why PostgreSQL Is Used

PostgreSQL is used because it provides a stable, production-ready foundation for structured data that must be reliable, queryable, auditable, and connected across system domains.

PostgreSQL is appropriate for the ALZO AI System because it supports:

- Strong relational modeling for tasks, projects, memory, decisions, reminders, and logs.
- Transactional integrity for workflow state and assistant-driven operations.
- Flexible JSON storage for AI metadata, structured outputs, and evolving schemas.
- Mature indexing, querying, migrations, backup tooling, and hosting options.
- Future extension paths for vector search, full-text search, analytics, and API services.

## Core Database Philosophy

The database should be modular, explainable, and aligned with the repository structure.

Core principles:

- **Repository-first governance.** Source-of-truth policies, schemas, and templates should remain documented in the repository.
- **Structured state for automation.** PostgreSQL should store operational state that benefits from querying, relationships, status tracking, or history.
- **Clear domain boundaries.** Data should be grouped by system area so Vera, Mira, studios, tasks, memory, and automation remain understandable.
- **Stable identifiers.** Durable records should use stable IDs that can be referenced across files, APIs, logs, and dashboards.
- **Auditability by default.** Important records should preserve timestamps, owners, status changes, and decision context.
- **Production recoverability.** Backup, restore, encryption, and migration paths must be defined before production reliance.

## Operational Data Categories

Recommended schema domains:

| Schema | Purpose |
| --- | --- |
| `system` | Shared configuration references, domain registries, status values, and system metadata. |
| `tasks` | Task records, lifecycle state, assignments, dependencies, and expected outputs. |
| `memory` | Memory records, metadata, categories, review status, and retrieval indexes. |
| `assistants` | Assistant interactions, role routing, prompt metadata, outputs, and review signals. |
| `schedules` | Reminders, recurrence rules, agenda items, and notification state. |
| `projects` | Project records, ownership, status, milestones, and related studio context. |
| `decisions` | Decision records, rationale, options considered, risks, review dates, and final status. |
| `automation` | Workflow runs, jobs, queues, retries, and execution results. |
| `logs` | Operational events, errors, audit trails, and system health signals. |

## Task Storage

Task storage should support lifecycle tracking, orchestration, review, and future dashboard views.

Recommended task records should include:

- Stable `task_id`.
- Title, description, objective, and priority.
- Status such as `planned`, `active`, `blocked`, `review`, `completed`, or `archived`.
- Assigned role, assigned studio, owner, and related project.
- Required inputs, expected outputs, dependencies, and acceptance criteria.
- Deadline, created timestamp, updated timestamp, and completion timestamp.
- Links to repository task files, reports, templates, memory records, or external references.

Task tables should allow dependency graphs so Vera can identify blockers, sequencing issues, and work that should become reusable templates or durable memory.

## Memory Storage

Memory storage should preserve structured metadata for durable context while keeping the repository memory records human-readable.

Recommended memory records should include:

- Stable `memory_id`.
- Memory category such as `vera`, `mira`, `project`, `task`, `decision`, `template`, or `archive`.
- Title, summary, source path, tags, and related entities.
- Review status, last reviewed date, and next review date.
- Sensitivity classification and retention status.
- Optional embedding reference for future vector retrieval.

The database should index memory metadata and retrieval signals. The full narrative memory record may remain in Markdown unless a later migration defines PostgreSQL as the authoritative content store.

## Assistant Interaction Storage

Assistant interaction storage should support traceability, improvement, routing, and audit without becoming an unmanaged transcript dump.

Recommended assistant interaction records should include:

- Stable interaction ID.
- Assistant or role involved, such as Vera, Mira, or a future specialized agent.
- Request category, routed domain, and workflow type.
- Input summary rather than raw sensitive content when possible.
- Output summary, generated artifact paths, and follow-up actions.
- Review status, user feedback, and quality signals.
- Created timestamp, model or service metadata when relevant, and related task or project IDs.

Sensitive content should be minimized, summarized, or excluded according to repository memory and backup policies.

## Schedules and Reminders

Schedules and reminders should support Mira's personal continuity layer and any future operational scheduling needs.

Recommended reminder records should include:

- Stable reminder ID.
- Reminder type such as agenda, routine, medication structure, check-in, follow-up, or recovery cue.
- Title, description, owner, and related role.
- Scheduled date, scheduled time, timezone, and recurrence rule.
- Status such as `planned`, `sent`, `acknowledged`, `rescheduled`, `skipped`, or `archived`.
- Related task, routine, project, or memory record.
- Delivery channel metadata when implemented.

Medication-related reminders must remain organizational support and should not be treated as medical advice or clinical decision-making.

## Project Storage

Project storage should connect studios, tasks, decisions, memory, and reports into coherent operational records.

Recommended project records should include:

- Stable project ID.
- Project name, owner, assigned studio, purpose, and strategic importance.
- Current status, phase, priority, and primary focus.
- Related systems, related studios, active tasks, dependencies, and risks.
- Links to project memory files, reports, templates, and decision records.
- Created timestamp, updated timestamp, archived timestamp, and review cadence.

Project tables should make it possible to see current work, historical context, and future actions without relying on scattered notes.

## Decision Storage

Decision storage should help Vera track why decisions were made, not only what was decided.

Recommended decision records should include:

- Stable decision ID.
- Decision title, date, owner, authority, and final status.
- Context and problem statement.
- Options considered and tradeoffs.
- Selected decision and reason for decision.
- Expected outcome and success signals.
- Related project, tasks, risks, reports, and memory files.
- Review date and review outcome.

Decision records should be queryable by project, system area, date, owner, and status so the system can audit rationale and avoid repeating unresolved debates.

## Logging Strategy

Logging should provide operational visibility without collecting unnecessary sensitive content.

Logging categories:

| Log Type | Purpose |
| --- | --- |
| Audit logs | Record important changes to tasks, projects, decisions, reminders, and memory metadata. |
| Workflow logs | Track automation runs, assistant workflow execution, retries, and outcomes. |
| Error logs | Capture failures, exceptions, validation issues, and recovery actions. |
| Access logs | Track access to sensitive operational areas when authentication exists. |
| Health logs | Monitor service status, database connectivity, queue health, and scheduled job status. |

Logs should include timestamps, severity, source, event type, related entity IDs, and enough context to troubleshoot safely. Logs should not store secrets, raw credentials, or unnecessary personal details.

## Future Vector Database Integration

Vector search may be introduced when semantic retrieval becomes useful for memory, reports, decisions, tasks, and project context.

Recommended integration model:

- PostgreSQL remains the primary relational state store.
- Vector indexes store embeddings and retrieval metadata for approved content.
- Each embedding record references a stable source entity, source path, content hash, and last indexed timestamp.
- Retrieval results should identify source records clearly so future agents can cite or inspect the original context.
- Sensitive or excluded content should not be embedded unless privacy and retention rules explicitly allow it.

Potential options include PostgreSQL extensions for vector search or a separate vector database if scale, performance, or retrieval requirements justify it.

## Scalability Principles

The database architecture should support growth without forcing early complexity.

Scalability principles:

- Start with clear schemas and stable IDs before adding advanced automation.
- Use migrations for all schema changes.
- Add indexes based on actual query patterns.
- Separate operational tables from logs and analytics when volume increases.
- Archive inactive records without deleting useful history.
- Keep workflow state inspectable and recoverable.
- Design APIs and dashboards around domain boundaries rather than one large generic table.

## Backup Integration

PostgreSQL must integrate with the ALZO AI System backup policy before it is used for production-critical data.

Backup requirements:

- Automated backups for critical operational data.
- Encrypted backup storage for personal, private, or non-public data.
- Documented restore procedures for every production database.
- Periodic restore validation after schema changes or migration events.
- Retention rules based on data criticality, sensitivity, and operational value.
- Migration files stored in the repository when implementation begins.

Database backups should preserve both schema and data. Restore readiness should be treated as part of production quality, not as an afterthought.

## Future API Architecture

A future API layer should expose PostgreSQL-backed data to dashboards, automation workers, assistant workflows, and approved external tools.

API architecture should support:

- Domain-specific endpoints for tasks, memory, projects, decisions, reminders, logs, and workflow runs.
- Authentication and authorization before accessing sensitive or personal data.
- Read/write boundaries that prevent uncontrolled assistant changes.
- Validation against repository-defined schemas and templates.
- Idempotent workflow operations where repeated calls could occur.
- Audit logging for create, update, archive, and restore operations.
- Clear error responses that support recovery and debugging.

The API should make system state accessible and actionable while preserving source-of-truth rules, human review gates, and production-grade operational control.
