# ALZO AI System Technical Stack

## Purpose

Recommend a practical technology stack for building the ALZO AI System as a scalable, AI-ready application.

## Recommended Stack

| Layer | Recommendation | Rationale |
| --- | --- | --- |
| Database | PostgreSQL | Reliable relational core for projects, tasks, decisions, memory, reminders, schedules, and logs. |
| Backend | Node.js with TypeScript, or Python with FastAPI | Strong API ergonomics, mature ecosystem, and good AI integration support. |
| Frontend | Next.js with TypeScript | Production-ready React framework with routing, server rendering, and strong deployment options. |
| Styling | Tailwind CSS | Fast interface development with consistent design primitives. |
| Authentication | Managed auth or framework-integrated auth | Reduces security burden during MVP. |
| AI orchestration | Service layer around assistant routing, retrieval, tools, and structured outputs | Keeps AI logic separate from UI and database concerns. |
| Hosting | Managed cloud platform | Simplifies deployment, scaling, environment management, and observability. |

## Backend Options

### Option A: Node.js + TypeScript

Best when the frontend and backend should share language, types, and developer workflow.

Recommended components:

- Next.js API routes or standalone Node service.
- Prisma, Drizzle, or equivalent PostgreSQL ORM/query layer.
- Zod or similar validation for request and response contracts.
- Background jobs for reminders, notifications, and workflow runs.

### Option B: Python + FastAPI

Best when AI orchestration, data processing, and backend services are expected to become more complex.

Recommended components:

- FastAPI for API routes.
- SQLAlchemy or SQLModel for PostgreSQL access.
- Pydantic for structured validation.
- Worker queue for scheduled jobs and assistant workflows.

## Frontend Options

| Option | Use When |
| --- | --- |
| Next.js dashboard | Best default for MVP and production web app. |
| Lightweight React app | Useful if backend is fully separate and server rendering is unnecessary. |
| WordPress admin extension | Useful later for publishing-specific workflows, not recommended as the core app shell. |

## PostgreSQL Usage

PostgreSQL should store:

- Projects, tasks, task dependencies, and decisions.
- Memory metadata, source paths, tags, and review state.
- Reminders, schedules, routine state, and confirmation events.
- Workflow runs, assistant actions, audit logs, and system events.

Use JSONB for evolving assistant metadata, workflow payloads, notification settings, and retrieval hints. Promote frequently queried JSONB fields into typed columns when usage stabilizes.

## AI Orchestration Layer

The AI layer should be implemented as a dedicated service boundary responsible for:

- Classifying user requests.
- Routing work to Vera, Mira, or studio workflows.
- Retrieving relevant structured memory.
- Producing structured task, decision, reminder, and report outputs.
- Writing approved updates back to PostgreSQL.
- Logging assistant actions and workflow transitions.

## WordPress Integration Strategy

WordPress should be treated as a publishing endpoint, not the core operating database.

Recommended integration path:

1. Keep ALZO operational data in PostgreSQL.
2. Use WordPress for public content, editorial publishing, and site presentation.
3. Connect via WordPress REST API or custom plugin only after publishing workflows are stable.
4. Sync final publishing artifacts, status, URLs, and metadata rather than raw internal planning records.
5. Preserve ALZO as the source of truth for strategy, tasks, decisions, and memory.
