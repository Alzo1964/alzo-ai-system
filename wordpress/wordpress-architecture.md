# WordPress Architecture

## Role

WordPress serves as the public presentation layer for the ALZO AI System. It publishes selected outputs from Vera, Mira, Publishing Studio, and Campaign Studio without becoming the system of record for strategy, memory, tasks, or backend intelligence.

## Position in the System

| Layer | Responsibility |
| --- | --- |
| ALZO backend | Intelligence, workflows, memory, reporting, task context, and API services. |
| WordPress | Public pages, editorial presentation, landing pages, minimal custom admin UI, dashboards, and audience-facing content. |
| WordPress | Public pages, editorial presentation, landing pages, dashboards, and audience-facing content. |
| Custom plugin | Secure bridge between WordPress and ALZO backend services. |

## Core Principles

- Keep WordPress focused on publishing, presentation, minimal custom admin workflows, and lightweight interaction.
- Keep WordPress focused on publishing, presentation, and lightweight interaction.
- Keep durable operating context inside the ALZO repository or backend system.
- Use APIs to sync approved content, dashboard data, and campaign assets.
- Avoid hard-coding ALZO business logic into themes.
- Preserve future migration flexibility by separating content, design, and intelligence services.

## API Connection

WordPress should communicate with the backend through authenticated REST or GraphQL endpoints. API traffic should support:

- Pulling approved dashboard summaries.
- Publishing selected editorial assets.
- Receiving campaign metadata and landing page content.
- Submitting form events, conversion signals, and user interactions.
- Displaying read-only system status where appropriate.

## Security Considerations

- Use scoped API credentials and rotate them regularly.
- Keep secrets outside theme files and versioned content.
- Validate and sanitize all inbound and outbound data.
- Limit dashboard views by role and capability.
- Log integration events without exposing private memory or personal context.

## Migration Flexibility

WordPress should remain replaceable. Content models, API contracts, and design components should be documented so the presentation layer can later move to a headless frontend, static site, or custom application without changing the ALZO backend architecture.
