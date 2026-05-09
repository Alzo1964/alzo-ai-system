# Dashboard Structure

## Purpose

The ALZO dashboard is the future visual command center for the repository's operating system. It should make tasks, memory, studios, personal continuity, reports, backup status, and automation workflows visible without replacing the repository as the durable documentation layer.

## Product Principles

- Show the current operating state clearly.
- Make next actions, blockers, and review items easy to find.
- Separate professional studio work from personal continuity while preserving system-level visibility.
- Prioritize calm, useful interfaces over noisy metrics.
- Design modules that can be added or removed without restructuring the entire dashboard.

## Proposed Navigation

| Section | Purpose |
| --- | --- |
| Home | Current system status, priority tasks, reminders, and review prompts. |
| Vera | Strategic plans, task routing, workflow engine status, and decision records. |
| Mira | Agenda, routines, reminders, check-ins, and personal continuity signals. |
| Studios | Campaign, software, and publishing workstreams. |
| Tasks | Active, completed, archived, and template-driven task management. |
| Memory | Searchable durable context and review queue. |
| Reports | Summaries, audits, performance notes, and incident records. |
| Automation | Scheduled workflows, run logs, failures, and retry status. |
| Backup | Backup status, restore readiness, retention, and policy references. |

## Core Views

- **Today View** — priorities, reminders, active tasks, and system alerts.
- **Studio View** — domain-specific projects, deliverables, and progress.
- **Task View** — status, ownership, dependencies, outputs, and deadlines.
- **Memory View** — durable context, categories, search, and review status.
- **Automation View** — workflow runs, logs, schedules, and exceptions.
- **Continuity View** — backups, restore readiness, and critical system health.

## Data Requirements

Dashboard data should come from structured files, PostgreSQL tables, or approved APIs. It should avoid duplicating source-of-truth content unless the dashboard is explicitly presenting an indexed, cached, or summarized view.

## Future Implementation Notes

- Keep dashboard modules aligned with repository domains.
- Use role-aware views for Vera and Mira workflows.
- Make every displayed status traceable to a source file, database record, or workflow run.
- Design for graceful degradation when automation or database services are unavailable.
