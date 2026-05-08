# Vera Workflow Engine

## Purpose

The Vera Workflow Engine is the future strategic orchestration layer for converting goals, requests, and repository signals into structured plans, task records, studio routing, risk reviews, and decision-ready outputs.

## Core Functions

- Classify incoming requests by domain, urgency, complexity, and expected output.
- Route work to the correct studio, role, task area, memory record, template, or report.
- Create or update task records using the master task template.
- Identify dependencies, risks, assumptions, and open questions.
- Convert repeated work into reusable templates, checklists, or workflows.
- Produce executive-ready summaries for review and decision-making.

## Workflow Lifecycle

| Stage | Purpose |
| --- | --- |
| Intake | Capture request, objective, context, constraints, and desired output. |
| Classification | Determine domain, assigned studio, role, priority, and workflow type. |
| Planning | Define scope, steps, dependencies, deliverables, and acceptance criteria. |
| Execution Routing | Send work to the correct file, studio, task record, or automation path. |
| Review | Validate output quality, risks, formatting, and repository placement. |
| Continuity | Update memory, reports, templates, or completed tasks when durable value exists. |

## Routing Rules

- Campaign work routes to `studios/campaign-studio/`.
- Software architecture and automation work routes to `studios/software-studio/`.
- Publishing and editorial work routes to `studios/publishing-studio/`.
- Personal planning and routines route to `personal/` or Mira-owned workflows.
- Durable decisions route to `memory/` or `reports/`.
- Reusable formats route to `templates/` or `tasks/templates/`.
- Backup and recovery work routes to `backup-policy/`.

## Future Engine Requirements

A production Vera Workflow Engine should support:

- Structured task creation.
- Dependency graph tracking.
- Workflow status updates.
- Report generation.
- Memory update recommendations.
- Dashboard integration.
- Human approval gates for high-impact changes.
