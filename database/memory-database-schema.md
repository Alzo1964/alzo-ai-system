# ALZO AI System Memory Database Schema

## Purpose

This document defines the Phase 2 relational memory database schema for the ALZO AI System. It translates the repository's human-readable operating model into a production-oriented PostgreSQL structure that can support assistant context, studio execution, project continuity, task orchestration, reminders, schedules, logging, reporting, and future semantic retrieval.

The schema is intended to be modular, AI-friendly, auditable, and scalable. It should support API access, workflow engines, dashboards, assistant memory retrieval, and future vector embedding infrastructure without replacing the repository as the governance layer for durable policies, templates, and architecture documents.

## Design Principles

1. **Stable entities before automation.** Core records should use durable identifiers and explicit relationships before automated workflows depend on them.
2. **Structured memory over transcript sprawl.** Store summaries, metadata, relationships, and lifecycle state rather than unmanaged raw conversations.
3. **Human-readable provenance.** Every durable record should indicate where it came from, who or what created it, and how it should be reviewed.
4. **Assistant-aware relationships.** Vera, Mira, and future assistants should be first-class participants in memory, decisions, tasks, and logs.
5. **Studio modularity.** Studios should be modeled as independent execution domains that can be queried, routed, reported, and expanded.
6. **Privacy and retention by design.** Sensitive records should carry classification, retention, review, and deletion guidance.
7. **Vector-ready architecture.** Semantic retrieval should be planned through explicit embedding references without coupling the core relational schema to one vector provider.

## Recommended Schema Domains

| Schema | Purpose |
| --- | --- |
| `system` | Shared enumerations, configuration references, source registries, and schema version records. |
| `assistants` | Assistant identities, capabilities, interactions, outputs, routing metadata, and feedback. |
| `studios` | Studio definitions, domains, routing rules, project associations, and performance metadata. |
| `projects` | Project records, ownership, priorities, lifecycle state, related studios, and strategic context. |
| `tasks` | Task lifecycle records, dependencies, assignments, deliverables, and review state. |
| `decisions` | Decision history, options considered, rationale, outcomes, and review checkpoints. |
| `memory` | Durable memory records, metadata, retrieval signals, source links, tags, and embedding references. |
| `schedules` | Reminders, routines, agenda items, recurrence rules, notification state, and confirmations. |
| `logs` | Audit events, operational logs, assistant actions, workflow events, errors, and health checks. |

## Core Tables

### `assistants.assistants`

Stores assistant identities and operating roles.

| Field | Type | Notes |
| --- | --- | --- |
| `assistant_id` | UUID | Primary key. |
| `name` | Text | Human-readable assistant name, such as `Vera` or `Mira`. |
| `role_type` | Text | Strategic, reflective, studio, automation, or specialist role. |
| `responsibility_summary` | Text | Concise description of operating scope. |
| `capabilities` | JSONB | Structured list of supported capabilities, limitations, and tool domains. |
| `default_routing_domains` | JSONB | Preferred studios, workflow types, or task categories. |
| `status` | Text | `active`, `paused`, `deprecated`, or `experimental`. |
| `created_at` / `updated_at` | Timestamptz | Standard audit timestamps. |

### `studios.studios`

Defines execution domains such as Campaign Studio, Software Studio, and Publishing Studio.

| Field | Type | Notes |
| --- | --- | --- |
| `studio_id` | UUID | Primary key. |
| `name` | Text | Studio name. |
| `slug` | Text | Stable lowercase identifier. |
| `purpose` | Text | Studio operating purpose. |
| `scope` | JSONB | Included responsibilities, excluded responsibilities, and handoff rules. |
| `primary_assistant_id` | UUID | Optional link to the assistant most responsible for routing or review. |
| `status` | Text | `active`, `planned`, `archived`, or `experimental`. |
| `created_at` / `updated_at` | Timestamptz | Standard audit timestamps. |

### `projects.projects`

Stores durable initiatives and connects them to studios, tasks, decisions, and memory.

| Field | Type | Notes |
| --- | --- | --- |
| `project_id` | UUID | Primary key. |
| `name` | Text | Project title. |
| `slug` | Text | Stable identifier for APIs, dashboards, and file references. |
| `summary` | Text | Concise project context. |
| `owner` | Text | Human or responsible operating role. |
| `lead_studio_id` | UUID | Primary studio. |
| `supporting_studio_ids` | UUID[] | Optional supporting studios. |
| `status` | Text | `planned`, `active`, `blocked`, `review`, `completed`, `archived`. |
| `priority` | Text | `low`, `normal`, `high`, `critical`. |
| `strategic_context` | JSONB | Goals, constraints, assumptions, risks, and success criteria. |
| `source_paths` | JSONB | Repository files or external references. |
| `created_at` / `updated_at` / `archived_at` | Timestamptz | Lifecycle audit timestamps. |

### `tasks.tasks`

Stores operational work items with routing, dependencies, deliverables, and lifecycle state.

| Field | Type | Notes |
| --- | --- | --- |
| `task_id` | UUID | Primary key. |
| `project_id` | UUID | Optional parent project. |
| `title` | Text | Clear task title. |
| `objective` | Text | Expected outcome. |
| `description` | Text | Additional context. |
| `assigned_assistant_id` | UUID | Vera, Mira, studio assistant, or automation agent. |
| `assigned_studio_id` | UUID | Studio responsible for execution or review. |
| `status` | Text | `planned`, `active`, `blocked`, `waiting`, `review`, `completed`, `archived`. |
| `priority` | Text | `low`, `normal`, `high`, `critical`. |
| `inputs` | JSONB | Required files, data, assumptions, or approvals. |
| `deliverables` | JSONB | Expected outputs and acceptance criteria. |
| `due_at` / `started_at` / `completed_at` | Timestamptz | Scheduling and lifecycle timestamps. |
| `created_at` / `updated_at` | Timestamptz | Standard audit timestamps. |

### `tasks.task_dependencies`

Represents dependency graphs for sequencing and blocker analysis.

| Field | Type | Notes |
| --- | --- | --- |
| `dependency_id` | UUID | Primary key. |
| `task_id` | UUID | Dependent task. |
| `depends_on_task_id` | UUID | Required predecessor task. |
| `dependency_type` | Text | `blocking`, `informational`, `approval`, `data`, or `artifact`. |
| `status` | Text | `open`, `satisfied`, `waived`, or `invalid`. |
| `notes` | Text | Rationale or resolution context. |
| `created_at` / `updated_at` | Timestamptz | Standard audit timestamps. |

### `decisions.decisions`

Stores durable choices and their rationale.

| Field | Type | Notes |
| --- | --- | --- |
| `decision_id` | UUID | Primary key. |
| `project_id` | UUID | Optional project relationship. |
| `task_id` | UUID | Optional originating task. |
| `title` | Text | Decision title. |
| `decision_summary` | Text | Final decision. |
| `rationale` | Text | Why the choice was made. |
| `options_considered` | JSONB | Alternatives, tradeoffs, and rejected paths. |
| `risks` | JSONB | Known risks, mitigations, and review triggers. |
| `status` | Text | `proposed`, `approved`, `rejected`, `superseded`, `under_review`. |
| `review_at` | Timestamptz | Future review point. |
| `created_at` / `updated_at` | Timestamptz | Standard audit timestamps. |

### `memory.memory_records`

Stores durable memory metadata and retrieval state.

| Field | Type | Notes |
| --- | --- | --- |
| `memory_id` | UUID | Primary key. |
| `title` | Text | Human-readable memory title. |
| `summary` | Text | Retrieval-friendly synopsis. |
| `memory_type` | Text | `vera`, `mira`, `project`, `task`, `decision`, `studio`, `routine`, `archive`. |
| `source_type` | Text | `repository`, `assistant_interaction`, `workflow`, `manual_entry`, `external`. |
| `source_path` | Text | Repository path, URI, or source identifier. |
| `related_entity_type` | Text | Optional related domain, such as project, task, decision, reminder, or studio. |
| `related_entity_id` | UUID | Optional related record ID. |
| `tags` | Text[] | Queryable tags. |
| `retrieval_metadata` | JSONB | Keywords, summaries, confidence, recency weights, and model-facing context. |
| `sensitivity_level` | Text | `public`, `internal`, `private`, `restricted`. |
| `retention_class` | Text | `active`, `review`, `archive`, `delete_candidate`. |
| `review_status` | Text | `current`, `needs_review`, `stale`, `superseded`. |
| `last_reviewed_at` / `next_review_at` | Timestamptz | Memory lifecycle timestamps. |
| `created_at` / `updated_at` / `archived_at` | Timestamptz | Standard audit timestamps. |

### `memory.memory_links`

Connects memory records to multiple system entities without overloading one foreign key.

| Field | Type | Notes |
| --- | --- | --- |
| `memory_link_id` | UUID | Primary key. |
| `memory_id` | UUID | Related memory record. |
| `entity_type` | Text | `assistant`, `studio`, `project`, `task`, `decision`, `reminder`, `schedule`, or `log`. |
| `entity_id` | UUID | Related record ID. |
| `relationship_type` | Text | `source`, `supports`, `updates`, `supersedes`, `references`, or `generated_by`. |
| `created_at` | Timestamptz | Link creation timestamp. |

### `schedules.reminders`

Stores reminder intent, priority, delivery channels, and confirmation state.

| Field | Type | Notes |
| --- | --- | --- |
| `reminder_id` | UUID | Primary key. |
| `title` | Text | Reminder label. |
| `reminder_type` | Text | `agenda`, `medication`, `check_in`, `routine`, `habit`, or `custom`. |
| `description` | Text | Plain-language reminder context. |
| `assigned_assistant_id` | UUID | Usually Mira for personal continuity reminders. |
| `priority` | Text | `low`, `normal`, `high`, `urgent`. |
| `schedule_id` | UUID | Optional recurring schedule relationship. |
| `notification_config` | JSONB | Channels, timing offsets, escalation preferences, and quiet hours. |
| `confirmation_required` | Boolean | Whether user acknowledgement is required. |
| `status` | Text | `active`, `paused`, `completed`, `cancelled`, `archived`. |
| `created_at` / `updated_at` | Timestamptz | Standard audit timestamps. |

### `schedules.schedules`

Stores reusable recurrence rules and schedule windows.

| Field | Type | Notes |
| --- | --- | --- |
| `schedule_id` | UUID | Primary key. |
| `name` | Text | Schedule label. |
| `schedule_type` | Text | `one_time`, `daily`, `weekly`, `monthly`, `custom_rrule`. |
| `timezone` | Text | IANA timezone identifier. |
| `starts_at` / `ends_at` | Timestamptz | Schedule boundary. |
| `recurrence_rule` | Text | RFC 5545-style recurrence rule when needed. |
| `recurrence_metadata` | JSONB | Human-readable pattern, exceptions, skip dates, and grace windows. |
| `status` | Text | `active`, `paused`, `expired`, `archived`. |
| `created_at` / `updated_at` | Timestamptz | Standard audit timestamps. |

### `logs.logs`

Stores operational and audit events across assistants, workflows, and system services.

| Field | Type | Notes |
| --- | --- | --- |
| `log_id` | UUID | Primary key. |
| `event_type` | Text | `audit`, `workflow`, `assistant_action`, `reminder_delivery`, `error`, `health`. |
| `severity` | Text | `debug`, `info`, `warning`, `error`, `critical`. |
| `actor_type` | Text | `user`, `assistant`, `system`, `automation`, or `external_service`. |
| `actor_id` | UUID | Optional actor identifier. |
| `entity_type` | Text | Affected record type. |
| `entity_id` | UUID | Affected record ID. |
| `message` | Text | Concise event summary. |
| `payload` | JSONB | Structured event details, request IDs, error metadata, or state transition data. |
| `created_at` | Timestamptz | Immutable event timestamp. |

## JSONB Usage

JSONB should be used for structured data that is valuable to preserve but may evolve faster than the relational schema.

Appropriate JSONB fields include:

- Assistant capabilities, routing metadata, and tool constraints.
- Studio scopes, exclusions, and handoff rules.
- Project goals, risks, assumptions, and success criteria.
- Task inputs, deliverables, acceptance criteria, and generated output references.
- Decision options, tradeoffs, risks, and review triggers.
- Memory retrieval metadata, AI summaries, confidence signals, and semantic keywords.
- Reminder notification preferences, escalation rules, quiet hours, and channel settings.
- Log payloads, workflow event details, and integration response metadata.

JSONB should not be used to avoid modeling stable relationships. If a field becomes frequently queried, filtered, joined, or constrained, it should be promoted to a typed column or supporting table.

## Indexing Principles

Indexes should be designed around operational queries, assistant retrieval, dashboards, and lifecycle maintenance.

Recommended index patterns:

- Primary key indexes on all UUID identifiers.
- Unique indexes on stable slugs such as project and studio slugs.
- Foreign key indexes for project, task, decision, studio, assistant, reminder, and schedule relationships.
- Composite indexes for common dashboard filters such as `(status, priority)`, `(assigned_studio_id, status)`, and `(next_review_at, review_status)`.
- GIN indexes for JSONB fields that support flexible filtering, especially retrieval metadata and notification configuration.
- GIN or trigram indexes for tags, titles, and summaries when full-text search becomes operationally important.
- Partial indexes for active records, upcoming reminders, open tasks, stale memories, unresolved dependencies, and unreviewed decisions.
- Time-based indexes for logs and event tables, with partitioning considered as volume grows.

Index additions should be justified by real query patterns, dashboard needs, workflow latency requirements, or retrieval quality requirements.

## Audit Fields

Production tables should use a consistent audit field pattern unless a table is intentionally append-only.

Recommended standard fields:

- `created_at`: when the record was created.
- `created_by_type`: `user`, `assistant`, `system`, `automation`, or `migration`.
- `created_by_id`: optional actor identifier.
- `updated_at`: last material update timestamp.
- `updated_by_type`: actor type responsible for the latest change.
- `updated_by_id`: optional actor identifier.
- `status`: current lifecycle state.
- `archived_at`: when the record was archived, if applicable.
- `version`: integer or semantic version for optimistic concurrency and audit review.

Append-only event tables may use `created_at`, actor fields, immutable payloads, and correlation IDs instead of mutable update fields.

## Future Vector Embedding Connection

The relational memory schema should prepare for semantic retrieval while keeping vector infrastructure replaceable.

Recommended approach:

1. Store canonical memory metadata in `memory.memory_records`.
2. Add `memory.memory_embeddings` when semantic retrieval is ready.
3. Keep embedding provider details and vector IDs separate from core memory records.
4. Support re-embedding without rewriting memory provenance or lifecycle history.
5. Allow either PostgreSQL vector extensions or an external vector service to serve retrieval workloads.

Proposed future table:

| Field | Type | Notes |
| --- | --- | --- |
| `embedding_id` | UUID | Primary key. |
| `memory_id` | UUID | Related memory record. |
| `embedding_provider` | Text | Provider or internal service name. |
| `embedding_model` | Text | Model used to generate the vector. |
| `embedding_vector_ref` | Text | External vector ID or internal vector reference. |
| `source_text_hash` | Text | Hash used to detect stale embeddings. |
| `embedding_metadata` | JSONB | Chunking strategy, dimensions, confidence, and refresh notes. |
| `status` | Text | `active`, `stale`, `failed`, `archived`. |
| `created_at` / `updated_at` | Timestamptz | Embedding lifecycle timestamps. |

## Implementation Sequence

1. Create schema domains and shared status enumerations.
2. Create assistants and studios tables as routing foundations.
3. Add projects, tasks, dependencies, and decisions.
4. Add memory records and memory links.
5. Add reminders, schedules, and reminder event logging.
6. Add logs and audit event capture.
7. Add indexes based on initial workflow, dashboard, and retrieval queries.
8. Add future embedding support only after memory review, privacy, and retrieval rules are stable.
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
