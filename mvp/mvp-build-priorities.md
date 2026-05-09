# MVP Build Priorities

## First Build Priorities

1. Establish repository-backed documentation and architecture boundaries.
2. Implement authentication, sessions, roles, and admin/user separation.
3. Build FastAPI backend API foundations for users, tasks, reminders, and dashboard payloads.
4. Add PostgreSQL persistence for core operational records.
5. Implement Vera planning and task-structuring workflow.
6. Implement Mira reminder and continuity workflow.
7. Connect WordPress as the presentation layer with minimal custom admin UI for public pages and approved dashboard summaries.
8. Add OpenAI API integration behind Vera and Mira runtime services.
9. Add Docker Compose local development for FastAPI and PostgreSQL.
10. Add backup-aware deployment practices for database and repository continuity.

## Vera MVP Role

Vera should focus on structured planning, task creation, priority summaries, campaign/publishing organization, and executive dashboard outputs. Vera should not perform unrestricted automation or publish externally without approval.

## Mira MVP Role

Mira should focus on reminder support, daily check-ins, routine continuity, and private personal notes. Mira should not expose sensitive context publicly or manage complex health workflows in the MVP.

## WordPress MVP Role

WordPress should present public content, simple landing pages, and approved dashboard summaries. It should not become the source of truth for backend memory, tasks, assistant logic, or private user data.

## Backend MVP Role

The backend should use FastAPI and provide secure APIs, runtime coordination, PostgreSQL persistence, task/reminder state, and approved data for WordPress. It should remain modular but does not need full microservice separation in the MVP.

## Priority Rule

Build vertical slices that connect user access, backend state, assistant workflow, and presentation before expanding isolated features.
