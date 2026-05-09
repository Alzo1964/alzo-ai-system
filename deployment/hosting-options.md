# Hosting Options

## Purpose

Hosting decisions should balance reliability, cost, operational complexity, security, and future flexibility for the ALZO AI System.

## WordPress Hosting Strategy

WordPress may be hosted on:

- Managed WordPress hosting for easier updates, backups, caching, and SSL.
- VPS or container hosting when deeper control is required.
- Headless or static-compatible hosting in the future if WordPress becomes a content source rather than the main presentation layer.

WordPress should not host private backend intelligence, assistant memory, or core system logic.

## Backend Hosting Strategy

The backend should run as a FastAPI Python service packaged with Docker. It may be hosted on:
The backend may be hosted on:

- A managed application platform for simple deployment and scaling.
- Containers on a VPS or cloud service for stronger control.
- Serverless functions for narrow event-driven workloads.
- Dedicated services later if orchestration, memory, publishing, or campaign processing need independent scaling.

## PostgreSQL Hosting Options

PostgreSQL may run through:

- Managed cloud PostgreSQL for production reliability, backups, monitoring, and upgrades.
- Containerized PostgreSQL for local development through Docker Compose or controlled environments.
- Containerized PostgreSQL for local development or controlled environments.
- VPS-hosted PostgreSQL only when operational maintenance is acceptable.

Production PostgreSQL should use automated backups, restricted network access, and monitored storage growth.

## Selection Guidance

Start with managed services where they reduce operational risk. Move to more customized hosting only when control, cost, compliance, or scaling needs justify the added responsibility.
