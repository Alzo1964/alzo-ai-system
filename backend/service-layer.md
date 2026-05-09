# Service Layer

## Purpose

The service layer contains backend business logic for the ALZO AI System. It sits between API controllers, runtime orchestration, databases, and external integrations.

## Service Modules

| Service | Responsibility |
| --- | --- |
| Task Service | Create, update, execute, and review tasks. |
| Memory Service | Govern memory reads, writes, retrieval, privacy, and retention. |
| Dashboard Service | Prepare Vera and Mira dashboard payloads. |
| Publishing Service | Sync approved editorial content and publication metadata. |
| Campaign Service | Manage campaign metadata, landing page configuration, and conversion events. |
| Reminder Service | Schedule and track Mira reminders, routines, and check-ins. |
| Notification Service | Deliver approved messages through email, dashboard, or future channels. |
| Auth Service | Manage identity, roles, permissions, tokens, and access checks. |

## Task Execution Flow

1. Runtime or API submits a task request.
2. Task Service validates objective, scope, owner, and status.
3. Supporting services retrieve memory, campaign, publishing, or dashboard context.
4. Execution result is persisted in PostgreSQL.
5. Follow-up events are emitted for dashboards, notifications, or reports.

## Memory Interaction Flow

1. Runtime requests context from Memory Service.
2. Memory Service checks authorization, sensitivity, and relevance.
3. PostgreSQL returns structured memory records.
4. Optional vector search returns semantic matches when enabled.
5. Memory Service returns filtered context and records an audit event.

## Database Strategy

PostgreSQL is the primary system database for structured operational records, relationships, statuses, and audit trails. Vector database support should be introduced as an optional retrieval layer behind Memory Service, not as a replacement for relational state.

## Microservice Readiness

Services should communicate through clear interfaces, typed payloads, and event-friendly boundaries. Future extraction should be possible without rewriting domain logic or changing public API contracts.
