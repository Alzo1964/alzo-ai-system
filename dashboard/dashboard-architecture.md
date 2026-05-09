# Dashboard Architecture

## Dashboard Purpose

The dashboard is the visual operating layer for the ALZO AI System. It should help users review priorities, personal reminders, task status, and system activity without replacing repository files as the source of truth.

## Primary Views

- **Vera Executive View:** Strategic priorities, decisions, risks, and studio activity.
- **Mira Personal View:** Agenda items, reminders, routines, and daily check-ins.
- **Task Board:** Shared work status, ownership, priority, and next actions.

## Status Tracking

Use simple shared states across views:

- `planned`
- `in-progress`
- `blocked`
- `awaiting-review`
- `complete`
- `archived`

## Future UI Direction

Future dashboard work should focus on clean navigation, role-specific summaries, task and reminder visibility, and eventual integration with workflow, memory, and database systems.
## Purpose

The dashboard provides a focused visual layer for the ALZO AI System. It should make active work, assistant activity, task status, and future operational data easy to review without replacing the repository as the source of truth.

## Core Views

- Vera executive view for system priorities, decisions, risks, and studio activity.
- Mira personal view for agenda items, routines, reminders, and check-ins.
- Task board for active, blocked, completed, and archived work.

## Status Tracking

Dashboard status should use simple, consistent states such as `planned`, `in progress`, `blocked`, `awaiting review`, and `complete`.

## Future UI Direction

Future dashboard work should prioritize clarity, fast scanning, role-aware views, and clean connections to task, memory, workflow, and database systems.
