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

Use when shared frontend/backend language and type contracts are valuable.
Best when the frontend and backend should share language, types, and developer workflow.

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
