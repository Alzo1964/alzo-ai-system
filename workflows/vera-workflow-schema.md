# Vera Workflow Schema

## Purpose

This document defines the Phase 2 workflow schema for Vera, the executive AI manager of the ALZO AI System. The workflow is designed to turn incoming requests into classified, routed, trackable, and reviewable work across studios, tasks, reports, memory, and future automation layers.

## Input Layer

The input layer captures the request and converts it into a structured intake object.

Recommended input fields:

| Field | Purpose |
| --- | --- |
| `request_id` | Stable intake identifier. |
| `request_summary` | Concise summary of the user request or system event. |
| `request_source` | User, dashboard, automation, schedule, API, or assistant. |
| `requested_outcome` | Desired result or deliverable. |
| `constraints` | Scope, file restrictions, deadlines, or policy requirements. |
| `context_links` | Related files, tasks, memory, reports, or projects. |
| `created_at` | Intake timestamp. |

## Classification Engine

The classification engine determines the nature of the request before execution begins.

Classification dimensions:

- Operating domain: Vera, Mira, studio, memory, task, report, template, database, backup, or automation.
- Work type: planning, documentation, implementation, review, routing, reporting, or archival.
- Priority: low, medium, high, or critical.
- Complexity: simple, multi-step, cross-domain, or high-risk.
- Sensitivity: public, internal, personal, sensitive, or restricted.
- Required output: file, task, report, template, decision, memory record, or recommendation.

## Routing Engine

The routing engine maps classified work to the correct repository area, studio, role, workflow, or automation path.

Routing output should include:

| Field | Purpose |
| --- | --- |
| `primary_destination` | Main repository path, studio, or system domain. |
| `supporting_destinations` | Secondary areas that may need updates. |
| `assigned_role` | Vera, Mira, studio role, or future agent. |
| `routing_reason` | Why this route was selected. |
| `approval_required` | Whether human review is needed before execution. |

## Task Generation

Vera should generate tasks when work requires lifecycle tracking, dependencies, explicit deliverables, or future review.

Task generation should define:

- Task ID and title.
- Objective and scope.
- Assigned studio and assigned role.
- Priority and status.
- Required inputs and expected outputs.
- Dependencies and related projects.
- Deadline or review date.
- Acceptance criteria.
- Related memory, report, or template records.

## Dependency Analysis

Dependency analysis identifies blockers and sequencing requirements before execution.

Dependency types:

| Type | Examples |
| --- | --- |
| Task dependency | Another task must be completed first. |
| Decision dependency | A decision or approval is required. |
| Asset dependency | A file, document, credential, or dataset is needed. |
| System dependency | Database, API, dashboard, automation, or service requirement. |
| Human dependency | Review, confirmation, ownership, or stakeholder input. |

Vera should surface dependency risk clearly and recommend the next stabilizing action.

## Execution Tracking

Execution tracking monitors progress from intake to completion.

Recommended execution fields:

- Workflow ID.
- Current state.
- Assigned role or studio.
- Started timestamp.
- Updated timestamp.
- Completed timestamp.
- Related task IDs.
- Files changed or artifacts generated.
- Blockers, warnings, or follow-up actions.

## Reporting

Vera should produce reports when information needs to be reviewed, shared, audited, or tracked over time.

Reporting outputs may include:

- Executive summary.
- Current state review.
- Decision record.
- Risk summary.
- Task completion report.
- System audit.
- Project status report.

Reports should link to relevant tasks, decisions, memory records, and source files.

## Memory Update

Vera should recommend or create memory updates when work produces durable context.

Memory update triggers:

- A significant decision was made.
- A reusable workflow or template emerged.
- A project assumption changed.
- A recurring risk or dependency was identified.
- A completed task created context useful for future work.
- A policy, schema, or operating standard changed.

Memory updates should include source path, summary, category, related entity IDs, review date, and sensitivity classification.

## Workflow States

Recommended Vera workflow states:

| State | Meaning |
| --- | --- |
| `intake` | Request captured but not yet classified. |
| `classified` | Domain, work type, and priority identified. |
| `routed` | Destination and assigned role selected. |
| `planned` | Task, dependencies, and outputs defined. |
| `in_progress` | Execution has started. |
| `blocked` | A dependency, decision, or missing input prevents progress. |
| `review` | Output is ready for validation. |
| `completed` | Work is complete and validated. |
| `archived` | Workflow retained for historical reference. |

## Studio Routing Rules

Vera routes work according to domain responsibility.

| Destination | Route Work Here When |
| --- | --- |
| `studios/campaign-studio/` | Campaign strategy, launch planning, positioning, messaging, and audience workflows. |
| `studios/software-studio/` | Architecture, implementation planning, technical documentation, automation, and database work. |
| `studios/publishing-studio/` | Editorial systems, written assets, publishing calendars, and documentation products. |
| `memory/` | Durable context, project memory, decision memory, or retrieval context. |
| `tasks/` | Work needs lifecycle tracking, ownership, dependencies, or deliverables. |
| `reports/` | Information needs review, audit, sharing, or historical summary. |
| `templates/` | A reusable format, checklist, or operating pattern is needed. |
| `backup-policy/` | Retention, restore, recoverability, or backup rules are affected. |
| `database/` | Structured data architecture, schemas, migrations, or database policy are involved. |
| `workflows/` | Workflow schemas, orchestration patterns, or process logic are involved. |

## Production Requirements

The Vera workflow schema should support future implementation through:

- Stable IDs for workflow runs and generated tasks.
- Clear state transitions.
- Audit logging for routing, approval, and completion.
- Human review gates for destructive or high-impact actions.
- Links to repository source files and database records.
- Recoverable workflow state for automation failures.
