# Task Execution Runtime

## Purpose

The task execution runtime governs how ALZO tasks move from request to completion, review, archive, or follow-up.

## Lifecycle

| Stage | Description |
| --- | --- |
| Intake | Receive request, trigger, or assistant-generated task candidate. |
| Classification | Determine domain, owner, scope, urgency, and sensitivity. |
| Planning | Define objective, context, steps, deliverables, and acceptance criteria. |
| Execution | Perform approved actions through assistant runtime or service layer. |
| Validation | Inspect outputs, check constraints, and confirm completion criteria. |
| Persistence | Save status, outputs, memory references, logs, or repository updates. |
| Review | Present summary, decisions, blockers, or next steps to the user or dashboard. |
| Closure | Mark complete, archive, or create follow-up tasks. |

## Execution Rules

- Keep each task focused on a clear objective.
- Preserve enough context for future audit and continuity.
- Route strategic and system tasks to Vera by default.
- Route personal reminder or routine tasks to Mira by default.
- Require permission before changing external systems or publishing content.
- Record failures, blockers, skipped steps, and follow-up needs.

## Runtime Safety

Task execution should validate role permissions, assistant access, data sensitivity, and external side effects before acting. Destructive operations, credential changes, and public publishing should require explicit authorization.

## Future Multi-Agent Support

Complex tasks may later be decomposed into subtasks owned by different assistants. The runtime should track parent task, subtask owner, handoff status, and final consolidation responsibility.
