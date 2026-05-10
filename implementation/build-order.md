# Build Order

## Purpose

Define the recommended sequence for building the ALZO AI System MVP and production expansion layers.

## Recommended Build Order

| Step | Area | Output |
| --- | --- | --- |
| 1 | PostgreSQL foundation | Migrations for projects, tasks, decisions, memory, reminders, schedules, and logs. |
| 2 | Backend API | Validated routes, database access, authentication, and audit timestamps. |
| 3 | Core dashboard | Screens for projects, tasks, memory, reminders, schedules, and review. |
| 4 | Reminder engine | Recurrence, confirmation, snooze, missed state, and event logging. |
| 5 | Vera workflow support | Classification, routing, task generation, dependency tracking, and reports. |
| 6 | Mira workflow support | Check-ins, routines, habits, reminder priority, and confirmation flow. |
| 7 | Background jobs | Scheduled reminders, recurring tasks, stale memory review, and workflow checks. |
| 8 | AI orchestration | Structured outputs, retrieval context, review gates, and approved writes. |
| 9 | WordPress integration | Publishing handoff, content metadata sync, URL tracking, and editorial status updates. |
| 10 | Production hardening | Backups, restore validation, observability, permissions, rate limits, and deployment automation. |

## Build Principles

- Build durable records before automation.
- Keep AI writes reviewable until trust and validation are proven.
- Prioritize daily usefulness over broad feature volume.
- Keep WordPress decoupled from internal operations.
- Validate each layer before expanding the next.
# ALZO AI System Build Order

## Purpose

Define the recommended sequence for building the ALZO AI System MVP and expansion layers.

## Recommended Build Order

| Step | Build Area | Output |
| --- | --- | --- |
| 1 | Data model | PostgreSQL tables for projects, tasks, decisions, memory, reminders, schedules, and logs. |
| 2 | Backend foundation | API routes, validation, database access, authentication, and audit timestamps. |
| 3 | Core dashboard | Project, task, memory, reminder, and schedule screens. |
| 4 | Vera workflow support | Classification, routing, task generation, dependency tracking, and reporting records. |
| 5 | Mira reminder support | Reminder creation, recurrence, confirmation, missed states, and routine tracking. |
| 6 | Background jobs | Scheduled reminders, stale memory review, recurring task generation, and workflow checks. |
| 7 | AI orchestration | Assistant service layer for structured outputs, retrieval, routing, and approved writes. |
| 8 | WordPress integration | Publishing handoff, content status sync, URL storage, and editorial workflow connection. |
| 9 | Observability | Logs, health checks, error tracking, dashboard metrics, and operational alerts. |
| 10 | Production hardening | Backups, restore drills, permissions, rate limits, deployment automation, and documentation. |

## Build Principles

- Build stable records before intelligent automation.
- Keep AI-generated output reviewable before database writes.
- Prioritize daily operating usefulness over complex autonomy.
- Avoid coupling WordPress to internal planning and memory data.
- Validate each layer before expanding the next layer.

## Early Technical Milestones

1. Repository implementation plan is documented.
2. PostgreSQL schema is translated into migrations.
3. API can create and retrieve core records.
4. Dashboard can show daily operating state.
5. Reminder jobs can create and resolve occurrences.
6. Vera workflow records can track routing and task generation.
7. Mira reminder records can track confirmation and missed states.
8. AI orchestration can generate structured, reviewable outputs.

## Deployment Sequence

1. Local development environment.
2. Staging environment with managed PostgreSQL.
3. Internal MVP deployment.
4. Backup and restore validation.
5. AI orchestration staging.
6. WordPress integration staging.
7. Production deployment after operational review.
5. WordPress integration staging.
6. Production deployment after operational review.
