# ALZO AI System MVP Scope

## Purpose

Define the first usable product scope for the ALZO AI System.

## MVP Goal

Deliver a minimal operating dashboard that supports structured planning, memory metadata, task tracking, reminders, and assistant-ready workflow records.

## Included Capabilities

| Area | MVP Scope |
| --- | --- |
| Projects | Create, edit, view, prioritize, and archive project records. |
| Tasks | Create tasks, assign status, set priority, connect to projects, and track completion. |
| Decisions | Record decisions, rationale, options considered, and review dates. |
| Memory | Store memory metadata, summaries, source paths, tags, and review status. |
| Reminders | Create agenda, routine, medication-support, check-in, and habit reminders. |
| Schedules | Support one-time, daily, weekly, and simple custom recurrence rules. |
| Logs | Capture audit events, workflow state changes, and reminder events. |
| Dashboard | Show current projects, active tasks, upcoming reminders, stale memory, and recent activity. |

## Excluded from MVP

- Full vector search.
- Complex multi-agent autonomy.
- Advanced analytics.
- Native mobile applications.
- Deep WordPress automation beyond initial integration planning.
- Payment, billing, or public user management.

## MVP Priorities

1. Reliable data model.
2. Clean user interface for daily use.
3. Clear Vera task and decision workflows.
4. Clear Mira reminder and routine workflows.
5. Basic authentication and role-aware access.
6. Audit logging for important changes.

## Acceptance Criteria

- A user can manage projects, tasks, decisions, memory records, reminders, and schedules from the application.
- Records persist in PostgreSQL with audit timestamps.
- The frontend provides a usable daily operating view.
- The backend exposes stable API routes for MVP entities.
- AI orchestration can read structured records without requiring schema changes.
