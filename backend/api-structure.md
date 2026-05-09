# API Structure

## Purpose

The API layer exposes controlled access to ALZO backend capabilities for WordPress, dashboards, automation tools, and future applications.

## Architecture

APIs should be organized by domain rather than implementation detail:

| Domain | Purpose |
| --- | --- |
| `/api/vera` | Strategic summaries, planning state, decisions, and executive dashboard payloads. |
| `/api/mira` | Reminders, check-ins, continuity prompts, and private personal dashboard payloads. |
| `/api/tasks` | Task creation, status updates, execution events, and review state. |
| `/api/memory` | Approved memory reads, writes, retrieval, and context references. |
| `/api/publishing` | Editorial sync, content status, metadata, and publication events. |
| `/api/campaigns` | Campaign metadata, landing page configuration, conversion events, and reporting. |

## Request Flow

1. Client authenticates with scoped credentials or a user session.
2. API validates authorization, payload shape, and rate limits.
3. Domain controller calls the appropriate service layer module.
4. Service layer reads or writes PostgreSQL and optional memory services.
5. API returns a structured response with status, data, and traceable errors.

## Security

- Require authentication for all private endpoints.
- Use role-based access for Vera, Mira, admin, and public publishing actions.
- Validate input schemas before service execution.
- Avoid returning raw memory, internal prompts, secrets, or private notes.
- Log API events with request IDs and minimal sensitive data.

## Versioning

API contracts should be versioned when public clients depend on them. Initial routes may use `/api/v1` once external integrations become stable.
