# PostgreSQL Architecture

## Purpose

PostgreSQL is the preferred future relational database layer for structured ALZO AI System data, including task orchestration, memory indexes, workflow runs, reminders, reports, dashboards, and automation logs.

## Architecture Principles

- Keep repository documentation as the human-readable source of truth for schemas and operating decisions.
- Use PostgreSQL for structured, queryable, transactional data that benefits from integrity constraints.
- Separate personal, studio, task, memory, and automation data through clear schemas or table groups.
- Prefer explicit migrations over manual database changes.
- Design for backup, restore, auditability, and future AI workflow orchestration from the beginning.

## Proposed Schema Domains

| Domain | Purpose |
| --- | --- |
| `system` | System metadata, configuration references, and versioned operating records. |
| `memory` | Durable memory records, categories, review dates, and retrieval metadata. |
| `tasks` | Task records, statuses, dependencies, assignments, deadlines, and outputs. |
| `studios` | Studio projects, deliverables, campaign/software/publishing workstreams. |
| `personal` | Agenda items, routines, check-ins, medication continuity references, and reminders. |
| `automation` | Workflow runs, schedules, logs, retries, and execution results. |
| `reports` | Report metadata, generated summaries, review cycles, and decision records. |

## Baseline Table Concepts

- `tasks.tasks` — canonical structured task records.
- `tasks.task_dependencies` — dependency graph between tasks, decisions, projects, and external blockers.
- `memory.records` — durable memory entries with category, scope, and review metadata.
- `automation.workflow_runs` — execution history for automated workflows.
- `personal.reminders` — reminder records for Mira-managed personal continuity.
- `reports.report_index` — searchable index of generated reports and decision summaries.

## Data Integrity Requirements

- Use stable IDs for tasks, memory records, reminders, workflows, and reports.
- Track `created_at`, `updated_at`, and where useful, `archived_at` timestamps.
- Prefer enumerated status values for lifecycle fields.
- Use foreign keys where relationships are stable and operationally important.
- Keep sensitive values out of application tables unless encryption and access controls are defined.

## Backup and Restore Requirements

PostgreSQL must follow the repository backup policy before production use:

- Daily backups for critical orchestration or memory data.
- Schema migrations stored in the repository.
- Restore procedure documented before production reliance.
- Encrypted storage for backups containing personal or non-public operational data.
