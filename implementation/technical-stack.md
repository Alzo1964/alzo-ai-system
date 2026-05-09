# Technical Stack

## Purpose

Recommend a practical stack for building the ALZO AI System as a modular, AI-ready web application.

## Recommended Technology Stack

| Layer | Recommendation | Notes |
| --- | --- | --- |
| Database | PostgreSQL | Core relational store for tasks, memory, reminders, schedules, decisions, logs, and audit state. |
| Backend | Node.js/TypeScript or Python/FastAPI | Choose based on team preference and AI workflow complexity. |
| Frontend | Next.js/TypeScript | Strong default for dashboard UI, routing, server rendering, and deployment. |
| Styling | Tailwind CSS | Fast, consistent interface development. |
| Auth | Managed authentication or framework-integrated auth | Reduces MVP security risk. |
| Jobs | Managed scheduler, queue worker, or background process | Required for reminders, recurrence, and workflow checks. |
| AI | Dedicated orchestration service | Keeps assistant routing and model calls separate from UI and database logic. |
| Hosting | Managed cloud deployment | Prefer simple operations, backups, monitoring, and environment separation. |

## Backend Options

### Option A: Node.js + TypeScript

Use when shared frontend/backend language and type contracts are valuable.

Recommended components:

- Next.js API routes or standalone Node service.
- Prisma, Drizzle, or another PostgreSQL query layer.
- Zod or equivalent runtime validation.
- Queue or scheduled worker for reminders and workflow jobs.

### Option B: Python + FastAPI

Use when AI orchestration, data processing, and service-layer logic are expected to grow quickly.

Recommended components:

- FastAPI for HTTP routes.
- SQLAlchemy or SQLModel for PostgreSQL access.
- Pydantic for validation and structured outputs.
- Worker queue for scheduled reminders and assistant workflows.

## Frontend Options

| Option | Best Use |
| --- | --- |
| Next.js dashboard | Recommended MVP and production app shell. |
| React single-page app | Useful if the backend is fully separate and server rendering is unnecessary. |
| WordPress admin extension | Later option for publishing workflows, not the core operating interface. |

## PostgreSQL Usage

PostgreSQL should store:

- Projects, tasks, dependencies, and decisions.
- Memory metadata, summaries, tags, source paths, and review state.
- Reminders, schedules, routine state, and confirmation events.
- Workflow runs, assistant actions, audit logs, and operational events.

Use JSONB for evolving metadata such as AI outputs, routing context, notification settings, and retrieval hints. Promote frequently queried fields into typed columns when usage stabilizes.

## AI Orchestration Layer

The AI orchestration layer should handle:

- Request classification.
- Vera, Mira, and studio routing.
- Context retrieval from PostgreSQL.
- Structured task, decision, report, memory, and reminder outputs.
- Human review gates before durable writes.
- Tool execution logs and workflow state transitions.

## WordPress Integration Strategy

WordPress should function as a publishing endpoint rather than the core operating system.

Recommended approach:

1. Keep operational records in PostgreSQL.
2. Use WordPress for public pages, posts, publishing presentation, and editorial delivery.
3. Connect through the WordPress REST API or a focused custom plugin.
4. Sync final content metadata, publishing status, URLs, and editorial artifacts.
5. Avoid syncing private planning, memory, reminder, or internal decision records unless explicitly required.
