# Backend Architecture

## Philosophy

The backend is the operational intelligence layer of the ALZO AI System. It should coordinate workflows, persist durable context, expose secure APIs, and keep presentation channels independent from core logic.

## Responsibilities

- Orchestrate Vera and Mira runtime activity.
- Manage task execution, memory interaction, and service coordination.
- Provide authenticated APIs for WordPress, dashboards, and future clients.
- Store structured operational data in PostgreSQL.
- Preserve modular boundaries so services can later separate cleanly.

## Core Principles

- Keep business logic out of presentation layers.
- Design small services around clear responsibilities.
- Treat memory, tasks, reports, and studio workflows as durable system assets.
- Prefer explicit interfaces over implicit coupling.
- Support gradual migration toward microservices without requiring early complexity.

## Runtime Model

The backend should operate as a modular application with separate runtime modules for orchestration, reminders, task execution, memory access, and external integrations. Shared services should provide logging, authentication, configuration, persistence, and API clients.

## Data Foundation

PostgreSQL should serve as the primary relational database for users, tasks, workflow state, publishing records, campaign metadata, dashboard payloads, and audit trails.

Future vector database support should be added behind a memory service interface so semantic search, embeddings, and retrieval workflows can evolve without changing application clients.

## Future Separation

The backend should begin as a coherent modular system and allow future extraction into independent services, such as orchestration, memory, publishing sync, campaign tracking, and notification delivery.
