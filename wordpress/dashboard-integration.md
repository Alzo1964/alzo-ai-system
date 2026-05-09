# Dashboard Integration

## Purpose

WordPress dashboards should provide lightweight visibility into selected ALZO AI System activity. They should not replace the backend, task layer, memory system, or repository documentation.

## Vera Dashboard

The Vera dashboard should present executive and system-level information, including:

- Current strategic priorities.
- Active reports or planning cycles.
- Campaign and publishing status summaries.
- Key decisions awaiting review.
- System health indicators from approved backend endpoints.

## Mira Dashboard

The Mira dashboard should present personal continuity and reflective support, including:

- Daily check-in prompts.
- Routine reminders.
- Lightweight agenda summaries.
- Reflection notes approved for display.
- Personal continuity signals that do not expose sensitive private memory.

## Data Flow

1. Backend prepares approved dashboard payloads.
2. WordPress plugin requests data through authenticated API calls.
3. WordPress renders read-only cards, lists, or status panels.
4. Optional user actions are submitted back to the backend as structured events.

## Access Control

- Vera modules should be restricted to authorized strategic or administrative users.
- Mira modules should be private by default.
- Role-based display rules should be enforced in the plugin and backend.
- Sensitive memory, medication, or personal context should never be publicly exposed.

## Design Principles

- Use clear cards, short summaries, and direct next actions.
- Prefer read-only visibility unless write actions are explicitly required.
- Keep dashboard modules modular so they can move to a future custom interface.
