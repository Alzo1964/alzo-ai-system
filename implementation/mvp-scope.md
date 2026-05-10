# MVP Scope

## Purpose

Define the first usable ALZO AI System product scope.

## MVP Goal

Deliver a lightweight operating dashboard that supports structured work, memory metadata, reminders, and assistant-ready records.

## Included

| Area | Scope |
| --- | --- |
| Projects | Create, edit, prioritize, review, and archive project records. |
| Tasks | Track status, priority, ownership, due dates, and project relationships. |
| Decisions | Capture decisions, rationale, options considered, risks, and review dates. |
| Memory | Store summaries, source paths, tags, relationships, and review state. |
| Reminders | Support agenda reminders, routines, check-ins, medication-support reminders, and habits. |
| Schedules | Support one-time, daily, weekly, and simple custom recurrence. |
| Logs | Record audit events, workflow events, reminder events, and assistant actions. |
| Dashboard | Show active work, upcoming reminders, recent decisions, and stale memory. |

## Excluded

- Full semantic/vector search.
- Fully autonomous multi-agent execution.
- Advanced analytics and forecasting.
- Native mobile apps.
- Deep WordPress automation.
- Public user, billing, or marketplace features.

## MVP Priorities

1. Reliable data persistence.
2. Clear daily operating view.
3. Minimal friction for project, task, memory, and reminder management.
4. Safe review flow for AI-generated updates.
5. Basic authentication and role-aware access.
6. Auditability for important changes.

## Acceptance Criteria

- Core records persist in PostgreSQL.
- Backend routes expose stable CRUD operations for MVP entities.
- Frontend screens support daily planning and review.
- AI orchestration can read structured context without schema changes.
- Deployment can run in staging with documented environment configuration.
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
