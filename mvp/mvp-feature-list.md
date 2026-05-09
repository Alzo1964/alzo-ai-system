# MVP Feature List

## Must-Have Features

- User authentication with admin and standard user separation.
- Basic role-based access for Vera, Mira, WordPress, and backend actions.
- Vera workflow for strategic planning, task creation, and executive summaries.
- Mira workflow for reminders, routines, check-ins, and private continuity notes.
- FastAPI backend API for dashboard data, tasks, reminders, and approved content sync.
- PostgreSQL storage for users, sessions, tasks, reminders, and audit events.
- WordPress presentation layer with minimal custom admin UI for public pages, approved summaries, and campaign landing pages.
- OpenAI API integration behind Vera and Mira runtime services.
- Docker Compose local development environment for FastAPI and PostgreSQL.
- Backend API for dashboard data, tasks, reminders, and approved content sync.
- PostgreSQL storage for users, sessions, tasks, reminders, and audit events.
- WordPress presentation layer for public pages, approved summaries, and campaign landing pages.
- Basic backup and deployment rules for repository and database continuity.

## Nice-to-Have Features

- Draft publishing sync from backend to WordPress.
- Campaign metadata management and conversion event capture.
- Lightweight dashboard cards for Vera and Mira status.
- Basic notification delivery for Mira reminders.
- Admin interface for integration settings.
- Initial memory tagging and retrieval filters.

## Should Not Be Built in MVP

- Full vector database implementation.
- Multi-agent task delegation beyond Vera and Mira.
- Nova runtime beyond placeholder planning.
- Complex analytics, attribution, or reporting suites.
- Billing, subscriptions, or customer account portals.
- Native mobile applications.
- Large-scale automation that bypasses user review.

## Feature Standard

Every MVP feature should be simple, traceable, secure by default, and directly tied to proving the system's core operating model.
