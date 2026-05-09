# ALZO AI System PostgreSQL Architecture

## Purpose

This document defines the initial PostgreSQL architecture for the ALZO AI System. It establishes how structured operational data should be stored, related, audited, backed up, and exposed to future dashboards, workflow engines, assistant services, and APIs.

The repository remains the human-readable source of truth for policies, templates, architecture notes, and operating standards. PostgreSQL is the production-oriented execution layer for data that needs relational integrity, queryability, lifecycle tracking, automation, or dashboard visibility.

## Why PostgreSQL Is Used

PostgreSQL is the preferred database because it provides a mature, reliable, and extensible foundation for structured AI system operations.

PostgreSQL supports the ALZO AI System by providing:

- **Relational integrity** for tasks, projects, decisions, reminders, memory metadata, and workflow relationships.
- **Transactional safety** for automation and assistant-driven state changes.
- **Flexible structured storage** through JSONB for evolving AI metadata and generated outputs.
- **Strong indexing and search options** for operational dashboards and retrieval workflows.
- **Mature migrations, backups, roles, permissions, and restore tooling** for production readiness.
- **Future vector search support** through extensions or integration with a dedicated vector database.

## Core Database Philosophy

The database should make the ALZO AI System easier to operate without making the system opaque.

Core principles:

1. **Repository-first governance.** Architecture, policies, templates, and source-of-truth rules are documented in the repository.
2. **Structured operational state.** PostgreSQL stores data that benefits from relationships, querying, status tracking, or automation.
3. **Domain separation.** Tables should be grouped by system domain so tasks, memory, assistants, reminders, projects, decisions, and logs remain understandable.
4. **Stable identifiers.** Durable entities should use IDs that can be referenced from Markdown files, APIs, dashboards, logs, and workflows.
5. **Auditability.** Important records should preserve creation, update, ownership, status, and review history.
6. **Privacy by design.** Sensitive personal data, secrets, and unnecessary raw transcripts should be minimized or excluded.
7. **Restore readiness.** Production data must have documented backup, restore, migration, and validation procedures.

## Operational Data Categories

The initial architecture should use schema-level separation to keep domains modular and future-friendly.

| Schema | Data Category | Primary Use |
| --- | --- | --- |
| `system` | System metadata and shared reference data | Domain registries, status values, configuration references, and version metadata. |
| `tasks` | Task lifecycle data | Assignments, statuses, dependencies, deadlines, inputs, outputs, and completion history. |
| `memory` | Memory metadata and retrieval state | Memory categories, source paths, tags, review status, and future embedding references. |
| `assistants` | Assistant interaction records | Vera/Mira interactions, routing, output summaries, artifacts, feedback, and review status. |
| `schedules` | Schedules and reminders | Agenda items, reminders, recurrence rules, delivery state, and reminder history. |
| `projects` | Project operating records | Ownership, status, strategic importance, dependencies, related studios, and project links. |
| `decisions` | Decision history | Options considered, rationale, selected decisions, risks, outcomes, and review dates. |
| `automation` | Workflow execution state | Jobs, workflow runs, retries, queues, approvals, and execution outcomes. |
| `logs` | Audit, health, and error logs | Operational visibility, debugging, incident analysis, and compliance support. |

## Task Storage

Task storage should support orchestration, accountability, prioritization, and review.

Recommended task data:

- `task_id`, title, description, objective, priority, and status.
- Created by, assigned role, assigned studio, owner, and related project.
- Required inputs, expected outputs, dependencies, and acceptance criteria.
- Deadline, created timestamp, updated timestamp, started timestamp, and completed timestamp.
- Links to repository task files, reports, memory records, templates, or external references.
- Review notes, blockers, and archived status when the task is no longer active.

Recommended relationships:

- Tasks may belong to projects.
- Tasks may depend on other tasks, decisions, files, approvals, or external systems.
- Tasks may produce reports, templates, memory records, or implementation artifacts.

## Memory Storage

Memory storage should index durable context without turning PostgreSQL into an unmanaged notes dump.

Recommended memory data:

- `memory_id`, title, summary, category, tags, and source path.
- Category values such as `vera`, `mira`, `project`, `task`, `decision`, `template`, or `archive`.
- Related task, project, decision, report, or assistant interaction IDs.
- Review status, last reviewed date, next review date, and archival state.
- Sensitivity level, retention class, and source-of-truth designation.
- Optional embedding ID or vector index reference for semantic retrieval.

The full memory narrative may remain in repository Markdown files. PostgreSQL should store metadata, relationships, lifecycle fields, and retrieval indexes unless a future migration explicitly makes database content authoritative.

## Assistant Interaction Storage

Assistant interaction storage should preserve useful operational traceability while avoiding unnecessary raw transcript storage.

Recommended assistant interaction data:

- `interaction_id`, assistant role, model/service metadata when relevant, and created timestamp.
- Request summary, routed domain, workflow type, and priority.
- Output summary, generated artifact paths, and related entity IDs.
- Review status, user feedback, quality signals, and follow-up requirements.
- Safety flags, privacy classification, or approval requirements when applicable.

Storage rules:

- Prefer summaries over raw conversation content.
- Do not store secrets, credentials, or unnecessary sensitive personal details.
- Link interactions to durable outputs such as tasks, memory records, reports, or decisions.
- Preserve enough metadata for Vera to audit routing and workflow quality.

## Schedules and Reminders

Schedules and reminders support Mira's continuity layer and future operational scheduling.

Recommended reminder data:

- `reminder_id`, reminder type, title, description, owner, and assigned role.
- Scheduled date, scheduled time, timezone, recurrence rule, and reminder window.
- Status values such as `planned`, `sent`, `acknowledged`, `rescheduled`, `skipped`, or `archived`.
- Related routine, agenda item, task, memory record, project, or assistant interaction.
- Delivery channel metadata when notification delivery is implemented.
- Created timestamp, updated timestamp, and acknowledgement timestamp when available.

Medication-related reminder records should remain organizational support only. They should not be treated as clinical instructions, diagnosis, or treatment guidance.

## Project Storage

Project storage should connect initiatives to the tasks, decisions, memory records, studios, and reports that define their operating context.

Recommended project data:

- `project_id`, project name, owner, assigned studio, and purpose.
- Strategic importance, current status, phase, priority, and primary focus.
- Related systems, related studios, dependencies, risks, and active tasks.
- Links to project memory files, reports, decision records, templates, and artifacts.
- Created timestamp, updated timestamp, review cadence, and archived timestamp.

Project records should make it possible to understand current state, historical context, and next actions without reconstructing the project from scattered notes.
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

Recommended decision data:

- `decision_id`, title, decision date, owner, authority, and final status.
- Context, problem statement, constraints, and assumptions.
- Options considered, advantages, tradeoffs, and reasons for rejection or selection.
- Selected decision and reason for decision.
- Expected outcome, success signals, and review date.
- Related project, tasks, risks, reports, memory records, and source files.
- Review outcome, supersession status, or reversal notes when the decision changes.

Decision records should be queryable by project, owner, system area, date, status, and review date so the system can preserve rationale and avoid repeating resolved debates.

## Logging Strategy

Logging should provide operational visibility, auditability, and failure recovery without storing unnecessary sensitive content.

| Log Type | Purpose | Example Events |
| --- | --- | --- |
| Audit logs | Track important data changes. | Task status updates, decision approvals, memory archival. |
| Workflow logs | Track automation and assistant workflow execution. | Workflow started, workflow completed, retry scheduled. |
| Error logs | Capture failures and recovery signals. | API failure, migration error, reminder delivery failure. |
| Access logs | Track access to sensitive operational areas when authentication exists. | User sign-in, permission denial, protected record access. |
| Health logs | Monitor service health. | Database connectivity, queue depth, scheduler status. |

Log records should include timestamp, severity, source service, event type, related entity IDs, and safe troubleshooting context. Logs should never store secrets, raw credentials, or avoidable personal details.

## Future Vector Database Integration

Vector search may be added when semantic retrieval becomes important for memory, reports, project context, decisions, and assistant workflows.

Recommended approach:

- PostgreSQL remains the primary relational state store.
- Vector indexes store embeddings and retrieval metadata for approved source content.
- Each vector record references a stable source entity ID, source path, content hash, and indexing timestamp.
- Retrieval results must point back to source records so agents can inspect and cite the original context.
- Sensitive or excluded content should not be embedded unless privacy, retention, and access controls explicitly allow it.

Implementation options may include PostgreSQL vector extensions or a dedicated vector database if scale, retrieval latency, or operational requirements justify separation.

## Scalability Principles

The database should scale through clear domain design before adding unnecessary infrastructure complexity.

Scalability principles:

- Start with explicit schemas, stable IDs, and migration discipline.
- Use indexes based on actual query patterns and dashboard needs.
- Separate high-volume logs from core operational tables when volume increases.
- Archive inactive records instead of deleting useful history.
- Keep workflow state inspectable and recoverable.
- Use JSONB for flexible metadata, but keep critical lifecycle fields relational.
- Design APIs and dashboard views around domain boundaries rather than generic catch-all records.

## Backup Integration

PostgreSQL must integrate with the ALZO AI System backup policy before it stores production-critical data.

Backup requirements:

- Automated backups for critical operational databases.
- Encrypted backup storage for personal, private, or non-public data.
- Documented restore procedures for every production database.
- Restore validation after major schema migrations or automation changes.
- Retention rules based on criticality, sensitivity, and operational value.
- Repository-stored migration files when implementation begins.

Backups should preserve both schema and data. Restore readiness should be treated as a production requirement, not a maintenance afterthought.
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

- Domain-specific endpoints for tasks, memory, assistants, schedules, projects, decisions, automation, and logs.
- Authentication and authorization before sensitive or personal data access.
- Validation against repository-defined schemas and templates.
- Human approval gates for destructive, sensitive, or high-impact actions.
- Idempotent operations for workflow calls that may be retried.
- Audit logging for create, update, archive, restore, and approval actions.
- Clear error responses that help operators and agents recover safely.

The API should make ALZO system state accessible and actionable while preserving source-of-truth rules, review gates, and production-grade operational control.
- Domain-specific endpoints for tasks, memory, projects, decisions, reminders, logs, and workflow runs.
- Authentication and authorization before accessing sensitive or personal data.
- Read/write boundaries that prevent uncontrolled assistant changes.
- Validation against repository-defined schemas and templates.
- Idempotent workflow operations where repeated calls could occur.
- Audit logging for create, update, archive, and restore operations.
- Clear error responses that support recovery and debugging.

The API should make system state accessible and actionable while preserving source-of-truth rules, human review gates, and production-grade operational control.
