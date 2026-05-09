# Vera Runtime

## Purpose

The Vera runtime coordinates strategic, executive, and systems-oriented backend workflows for the ALZO AI System.

## Responsibilities

- Convert goals into plans, workflows, reports, and decisions.
- Coordinate task execution across studios and operating layers.
- Prepare executive dashboard summaries for approved clients.
- Read relevant memory and repository context through controlled services.
- Write durable decisions, status updates, and workflow outputs.

## Orchestration Flow

1. Receive a user request, scheduled trigger, or system event.
2. Classify the operating domain and required services.
3. Retrieve relevant task, memory, report, or studio context.
4. Generate a structured plan or execution payload.
5. Dispatch task actions to the service layer.
6. Persist outputs, status, audit data, and follow-up requirements.
7. Publish approved summaries to dashboards or API consumers.

## Task Execution Flow

Vera should treat tasks as traceable units with objective, context, scope, steps, deliverables, status, and notes. Task state should be stored in PostgreSQL and linked to repository files when applicable.

## Memory Interaction

Vera should request memory through a memory service rather than direct database access. The memory service should enforce privacy, relevance, retention, and audit rules before returning context or accepting updates.

## Modular Boundaries

Vera orchestration should remain separate from API controllers, database adapters, notification delivery, and presentation rendering so it can later become an independent orchestration service.
