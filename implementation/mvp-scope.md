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
