# Vera Workflow Schema

## Purpose

This document defines the Phase 2 workflow schema for Vera, the strategic and systems-oriented intelligence layer of the ALZO AI System. The schema describes how Vera should receive inputs, classify intent, route work, generate tasks, analyze dependencies, track execution, report progress, and update durable memory.

The workflow is designed for modular execution across studios, future automation services, dashboards, APIs, and assistant orchestration layers.

## Workflow Objectives

Vera workflows should:

- Convert ambiguous goals into structured plans, tasks, decisions, and reports.
- Route work to the correct studio or operating domain.
- Preserve context through explicit inputs, assumptions, dependencies, and outputs.
- Track execution state in a way that can support dashboards and automation.
- Identify reusable templates, memory updates, and system improvements.
- Maintain auditability for strategic decisions and operational changes.

## 1. Input Layer

The input layer captures a request and normalizes it into a structured work packet.

### Accepted Inputs

| Input Type | Examples | Handling |
| --- | --- | --- |
| Direct user request | Strategy request, planning request, architecture request | Parse objective, constraints, desired output, and urgency. |
| Repository change request | Create documents, update templates, modify workflows | Identify allowed paths, protected paths, expected files, and validation needs. |
| Studio request | Campaign, software, or publishing execution | Route to the appropriate studio workflow. |
| Memory signal | Durable context, decision, recurring pattern | Determine whether a memory record or decision entry is required. |
| Report request | Status summary, review packet, executive brief | Define audience, period, source data, and format. |
| Automation event | Scheduled review, stale task, blocked dependency | Convert system event into a review or execution task. |

### Normalized Input Packet

A Vera workflow should produce a normalized input packet with:

- `request_id`
- `request_summary`
- `request_source`
- `request_type`
- `requested_output`
- `constraints`
- `allowed_paths`
- `protected_paths`
- `deadline_or_urgency`
- `known_context`
- `assumptions`
- `required_review_level`

## 2. Classification Engine

The classification engine determines the work domain, intent, risk level, and required output type.

### Classification Dimensions

| Dimension | Values |
| --- | --- |
| `domain` | `vera`, `mira`, `campaign_studio`, `software_studio`, `publishing_studio`, `database`, `workflow`, `memory`, `tasks`, `backup_policy`, `reports`, `templates`. |
| `intent` | `plan`, `execute`, `document`, `review`, `decide`, `summarize`, `archive`, `automate`, `escalate`. |
| `complexity` | `simple`, `moderate`, `complex`, `multi_phase`. |
| `risk_level` | `low`, `medium`, `high`, `restricted`. |
| `durability` | `temporary`, `task`, `template`, `memory`, `decision`, `report`, `architecture`. |
| `human_review` | `not_required`, `recommended`, `required`, `blocked_until_review`. |

### Classification Outputs

The engine should return:

- Primary domain and secondary domains.
- Recommended assistant or studio owner.
- Required artifacts.
- Required checks or validation steps.
- Whether the work creates durable system knowledge.
- Whether protected areas are affected.

## 3. Routing Engine

The routing engine assigns the work to Vera, Mira, a studio, or a future automation service.

### Routing Rules

| Condition | Route |
| --- | --- |
| Strategic planning, system design, task decomposition, decision modeling | Vera. |
| Personal continuity, reminders, routines, check-ins, medication structures | Mira. |
| Campaign strategy, positioning, audience, launch, performance creative | Campaign Studio. |
| Product architecture, implementation plans, technical documentation, automation | Software Studio. |
| Editorial systems, publishing calendars, written assets, knowledge packaging | Publishing Studio. |
| Database schemas, relational modeling, indexing, migrations | Software Studio with Vera oversight. |
| Cross-studio operating model or architecture | Vera as lead with studio-specific inputs. |
| Sensitive personal reminder or routine | Mira as lead with privacy review. |

### Routing Packet

The routing engine should produce:

- `owner_type`
- `owner_id`
- `supporting_owners`
- `studio_id`
- `handoff_notes`
- `routing_confidence`
- `routing_reason`
- `review_requirements`

## 4. Task Generation

Vera converts classified work into actionable tasks when execution requires multiple steps, durable tracking, dependencies, or review.

### Task Generation Criteria

Create a task when:

- The work has multiple deliverables or phases.
- The work changes architecture, templates, workflows, reports, or memory.
- The work has dependencies, blockers, approvals, or deadlines.
- The outcome should be reviewed, archived, reused, or reported later.

### Task Record Structure

A generated task should include:

- Title.
- Objective.
- Context.
- Scope boundaries.
- Required inputs.
- Steps.
- Deliverables.
- Dependencies.
- Acceptance criteria.
- Owner and studio route.
- Status.
- Review notes.
- Memory or decision update requirements.

## 5. Dependency Analysis

Dependency analysis identifies sequencing, blockers, required context, and handoff requirements before execution.

### Dependency Types

| Type | Description |
| --- | --- |
| `context` | Required background, source files, project state, or memory records. |
| `artifact` | Required documents, templates, schemas, reports, or code files. |
| `decision` | Required strategic, technical, or editorial choice. |
| `approval` | Required human review or permission before continuing. |
| `external` | Required third-party data, service access, calendar, API, or account. |
| `sequence` | Work that must be completed before another task can begin. |

### Dependency Outputs

Vera should produce:

- Dependency list.
- Blocker list.
- Risk notes.
- Required decisions.
- Suggested sequence.
- Handoff points.
- Validation requirements.

## 6. Execution Tracking

Execution tracking records current state, progress, decisions, blockers, and outputs.

### Execution Fields

| Field | Purpose |
| --- | --- |
| `workflow_run_id` | Unique execution identifier. |
| `workflow_type` | Plan, document, implementation, review, report, or memory update. |
| `current_state` | Current workflow state. |
| `owner` | Responsible assistant, studio, or system service. |
| `started_at` | Execution start time. |
| `updated_at` | Latest progress update. |
| `completed_at` | Completion time, if finished. |
| `artifacts` | Files, reports, tasks, decisions, or memory records produced. |
| `blockers` | Current unresolved blockers. |
| `validation_results` | Checks performed and results. |

## 7. Reporting

Vera reporting converts execution state into decision-ready summaries.

### Report Types

| Report Type | Purpose |
| --- | --- |
| `executive_summary` | Concise outcome, status, risks, and next steps. |
| `task_status` | Active task progress, blockers, owners, and deadlines. |
| `dependency_report` | Sequencing, blockers, required decisions, and unresolved inputs. |
| `studio_report` | Work grouped by Campaign, Software, Publishing, or future studios. |
| `decision_report` | Decisions made, pending decisions, rationale, and review dates. |
| `memory_report` | New, stale, updated, or superseded memory records. |
| `architecture_report` | Durable architecture changes and implementation implications. |

### Reporting Standards

Reports should include:

- Objective.
- Current status.
- Completed work.
- Open risks or blockers.
- Decisions made.
- Required next actions.
- Related tasks, files, memory records, or reports.
- Review date or escalation owner when needed.

## 8. Memory Update

Vera should evaluate whether each workflow creates durable knowledge.

### Memory Update Triggers

Create or update memory when:

- A strategic decision affects future work.
- A recurring workflow pattern emerges.
- A project changes scope, priority, owner, or operating context.
- A task produces reusable architecture, templates, or reports.
- A prior assumption is corrected or superseded.
- A handoff requires future continuity.

### Memory Update Packet

A memory update should include:

- `memory_type`
- `title`
- `summary`
- `source_path`
- `related_entities`
- `tags`
- `sensitivity_level`
- `retention_class`
- `review_status`
- `next_review_at`

## 9. Workflow States

Vera workflows should use explicit states that can be stored, queried, and reported.

| State | Meaning |
| --- | --- |
| `received` | Input captured but not yet classified. |
| `classified` | Domain, intent, risk, and output type identified. |
| `routed` | Owner, studio, or assistant route assigned. |
| `planned` | Steps, dependencies, and deliverables defined. |
| `blocked` | Required input, decision, approval, or dependency is missing. |
| `in_progress` | Execution is underway. |
| `review` | Output is ready for validation or human review. |
| `completed` | Deliverables are complete and validated. |
| `memory_updated` | Durable memory, decision, or report updates are complete. |
| `archived` | Workflow is closed and retained for reference. |
| `cancelled` | Workflow ended without completion. |

## 10. Studio Routing Rules

### Campaign Studio

Route to Campaign Studio when the request involves:

- Campaign strategy or launch planning.
- Audience definition, positioning, messaging, or offer structure.
- Channel planning, creative direction, conversion paths, or performance review.
- Campaign retrospectives or reusable launch playbooks.

### Software Studio

Route to Software Studio when the request involves:

- Technical architecture, implementation plans, automation, data models, or APIs.
- Database schemas, workflow engines, dashboard support, or integration design.
- Technical documentation, migration plans, acceptance criteria, or validation strategy.

### Publishing Studio

Route to Publishing Studio when the request involves:

- Editorial assets, publishing calendars, content systems, documentation products, or knowledge packaging.
- Draft management, review workflows, final asset preparation, or content operations.

### Vera-Led Cross-Studio Work

Vera should remain the lead when:

- Multiple studios are involved.
- The task changes the operating model.
- Durable architecture or governance is created.
- There are strategic tradeoffs, dependencies, or future system implications.

## Output Contract

Every Vera workflow should produce one or more of the following:

- A completed response or decision-ready recommendation.
- A task record or task file.
- A workflow status update.
- A report.
- A decision record.
- A memory update packet.
- A routed handoff packet.
- A validation summary.
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
