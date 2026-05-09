# Memory Database Schema

## Purpose

This document defines the Phase 2 relational schema direction for the ALZO AI System memory and operating database. The schema is designed to support structured memory, assistant workflows, studio operations, projects, tasks, decisions, reminders, schedules, logs, future dashboard views, and future vector retrieval.

The schema should remain modular, AI-friendly, auditable, and production-oriented. Repository Markdown files continue to provide human-readable governance and templates, while PostgreSQL stores structured state, relationships, lifecycle fields, and retrieval metadata.

## Schema Philosophy

Core principles:

- **Domain clarity.** Store each major operating area in a dedicated table or schema boundary.
- **Stable identity.** Every durable entity should have a stable ID for cross-reference by files, APIs, dashboards, logs, and agents.
- **Auditability.** Important records should include ownership, status, timestamps, source references, and review fields.
- **AI-friendly metadata.** Tables should support summaries, tags, JSONB metadata, source paths, and future retrieval links.
- **Human source of truth.** PostgreSQL supports operations; repository documents preserve policy, templates, and architectural intent unless a future migration says otherwise.

## Assistants

The `assistants` table stores AI role definitions and operational metadata for Vera, Mira, and future specialized agents.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `assistant_id` | UUID / text | Stable assistant identifier. |
| `name` | text | Assistant name, such as Vera or Mira. |
| `role_type` | text | Strategic, personal, studio, automation, or specialized role. |
| `scope` | text | Primary operating scope or domain. |
| `status` | text | Active, paused, deprecated, or archived. |
| `metadata` | JSONB | Model references, routing notes, capabilities, or configuration metadata. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |

## Studios

The `studios` table stores structured information about ALZO studio domains.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `studio_id` | UUID / text | Stable studio identifier. |
| `name` | text | Studio name. |
| `path` | text | Repository path for the studio. |
| `description` | text | Studio purpose and responsibility summary. |
| `status` | text | Active, inactive, planned, or archived. |
| `metadata` | JSONB | Routing rules, supported outputs, owners, or tags. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |

## Projects

The `projects` table stores project-level operating records.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `project_id` | UUID / text | Stable project identifier. |
| `name` | text | Project name. |
| `owner` | text | Accountable person, role, or agent. |
| `studio_id` | UUID / text | Related studio when applicable. |
| `purpose` | text | Project purpose. |
| `strategic_importance` | text | Why the project matters. |
| `status` | text | Planned, active, blocked, paused, completed, or archived. |
| `priority` | text | Low, medium, high, or critical. |
| `metadata` | JSONB | Related systems, milestones, tags, or dashboard configuration. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |
| `archived_at` | timestamp | Archive time, if applicable. |

## Tasks

The `tasks` table stores actionable work items and lifecycle state.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `task_id` | UUID / text | Stable task identifier. |
| `project_id` | UUID / text | Related project, if applicable. |
| `assigned_studio_id` | UUID / text | Studio responsible for execution. |
| `assigned_assistant_id` | UUID / text | Vera, Mira, or future agent. |
| `title` | text | Task title. |
| `objective` | text | Desired outcome. |
| `status` | text | Planned, active, blocked, review, completed, or archived. |
| `priority` | text | Low, medium, high, or critical. |
| `deadline_at` | timestamp | Deadline when applicable. |
| `metadata` | JSONB | Required inputs, expected outputs, acceptance criteria, and tags. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |
| `completed_at` | timestamp | Completion time, if applicable. |

## Decisions

The `decisions` table stores decision records and rationale so Vera can track why choices were made.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `decision_id` | UUID / text | Stable decision identifier. |
| `project_id` | UUID / text | Related project, if applicable. |
| `owner` | text | Decision owner or authority. |
| `title` | text | Decision title. |
| `context` | text | Situation or problem that required the decision. |
| `selected_decision` | text | Final selected decision. |
| `reason_for_decision` | text | Rationale and tradeoff explanation. |
| `expected_outcome` | text | Expected result or success signal. |
| `status` | text | Proposed, approved, active, superseded, reversed, or archived. |
| `review_at` | timestamp | Planned review date. |
| `metadata` | JSONB | Options considered, risks, related files, and notes. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |

## Memory Records

The `memory_records` table stores structured metadata for durable context.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `memory_id` | UUID / text | Stable memory identifier. |
| `category` | text | Vera, Mira, project, task, decision, template, or archive. |
| `title` | text | Memory title. |
| `summary` | text | Concise durable summary. |
| `source_path` | text | Repository source path when applicable. |
| `source_type` | text | Markdown, report, task, interaction, generated output, or external reference. |
| `sensitivity` | text | Public, internal, personal, sensitive, or restricted. |
| `review_status` | text | Current, needs-review, stale, archived, or superseded. |
| `tags` | text[] / JSONB | Retrieval tags. |
| `metadata` | JSONB | Related entities, provenance, review notes, and retrieval hints. |
| `embedding_ref` | text | Future vector embedding reference. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |
| `last_reviewed_at` | timestamp | Last review date. |
| `archived_at` | timestamp | Archive time, if applicable. |

## Reminders

The `reminders` table stores individual reminder records for Mira and future operational reminders.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `reminder_id` | UUID / text | Stable reminder identifier. |
| `assistant_id` | UUID / text | Mira or responsible assistant. |
| `title` | text | Reminder title. |
| `reminder_type` | text | Agenda, medication, routine, check-in, follow-up, or recovery. |
| `priority` | text | Low, normal, high, or urgent. |
| `scheduled_at` | timestamp | Scheduled delivery time. |
| `status` | text | Planned, sent, acknowledged, missed, rescheduled, skipped, or archived. |
| `metadata` | JSONB | Tone, channel, recurrence, confirmation, and related context. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |
| `acknowledged_at` | timestamp | User confirmation time, if applicable. |

## Schedules

The `schedules` table stores recurrence and time-based execution rules.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `schedule_id` | UUID / text | Stable schedule identifier. |
| `name` | text | Schedule name. |
| `schedule_type` | text | Reminder, workflow, report, backup, routine, or check-in. |
| `timezone` | text | Timezone for execution. |
| `recurrence_rule` | text / JSONB | Recurrence definition. |
| `next_run_at` | timestamp | Next expected run. |
| `last_run_at` | timestamp | Previous run. |
| `status` | text | Active, paused, completed, failed, or archived. |
| `metadata` | JSONB | Execution window, owner, retry policy, or related entity IDs. |
| `created_at` | timestamp | Record creation time. |
| `updated_at` | timestamp | Last update time. |

## Logs

The `logs` table stores operational events, audit records, workflow outcomes, and system health signals.

Recommended fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `log_id` | UUID / text | Stable log identifier. |
| `log_type` | text | Audit, workflow, error, access, health, or system. |
| `severity` | text | Debug, info, warning, error, or critical. |
| `source` | text | Service, assistant, workflow, or API source. |
| `event_type` | text | Event category. |
| `message` | text | Safe human-readable event summary. |
| `related_entity_type` | text | Task, memory, decision, reminder, project, or workflow. |
| `related_entity_id` | text | Related entity identifier. |
| `metadata` | JSONB | Safe diagnostic details. |
| `created_at` | timestamp | Event time. |

## JSONB Usage

JSONB should support flexible metadata without replacing relational fields that need filtering, joining, or lifecycle control.

Use JSONB for:

- AI-generated metadata and confidence scores.
- Flexible assistant output summaries.
- Options considered for decisions.
- Required inputs and expected outputs for tasks.
- Reminder tone, channel, and recurrence details.
- Retrieval hints, tags, and source references.
- Integration payloads from future APIs or automation workers.

Do not hide critical status, ownership, timestamps, or relationships only inside JSONB. Those fields should remain explicit columns.

## Indexing Principles

Indexes should support dashboard queries, workflow orchestration, retrieval, and audits.

Recommended indexes:

- Primary keys on all stable IDs.
- Foreign-key indexes for project, task, assistant, decision, and memory relationships.
- Status and priority indexes for active operational views.
- Timestamp indexes for review dates, schedules, deadlines, and logs.
- Tag or JSONB GIN indexes only where query patterns justify them.
- Future vector indexes for approved embedded content.

Indexes should be added based on actual access patterns rather than speculative complexity.

## Audit Fields

Most operational tables should include standard audit fields:

| Field | Purpose |
| --- | --- |
| `created_at` | Record creation timestamp. |
| `updated_at` | Last update timestamp. |
| `created_by` | Person, role, assistant, or system that created the record. |
| `updated_by` | Person, role, assistant, or system that last updated the record. |
| `source_path` | Repository source file when applicable. |
| `archived_at` | Archive timestamp when a record leaves active use. |
| `version` | Optional optimistic locking or schema version indicator. |

High-impact changes should also write audit log records.

## Future Vector Embedding Connection

The schema should prepare for vector retrieval without requiring it in the first implementation.

Future vector connections should include:

- A stable embedding reference from `memory_records` or other source tables.
- Source entity ID, source type, source path, and content hash.
- Embedding model metadata and indexing timestamp.
- Retrieval access rules that respect sensitivity and retention policy.
- Re-indexing strategy when source content changes.

PostgreSQL may use vector extensions or connect to a separate vector database. In either model, source records must remain inspectable and traceable.
