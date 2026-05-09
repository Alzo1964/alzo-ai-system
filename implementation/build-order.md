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

## Deployment Sequence

1. Local development environment.
2. Staging environment with managed PostgreSQL.
3. Internal MVP deployment.
4. Backup and restore validation.
5. AI orchestration staging.
6. WordPress integration staging.
7. Production deployment after operational review.
