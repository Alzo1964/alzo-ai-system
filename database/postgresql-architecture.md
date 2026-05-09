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
