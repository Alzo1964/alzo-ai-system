# Custom Plugin Strategy

## Objective

The custom WordPress plugin should provide the controlled integration layer between WordPress and the ALZO AI System backend.

## Responsibilities

- Register ALZO-specific content types, blocks, shortcodes, or minimal admin pages.
- Authenticate requests to backend APIs.
- Render Vera and Mira dashboard modules inside WordPress when appropriate.
- Sync approved Publishing Studio content into WordPress drafts or published pages.
- Support campaign landing page templates and conversion tracking.
- Centralize integration settings outside the active theme.
- Provide the minimal custom admin UI required to manage ALZO integration settings and approved sync actions.

## Recommended Structure

```text
alzo-system-plugin/
  alzo-system-plugin.php
  includes/
    api-client.php
    dashboard-modules.php
    publishing-sync.php
    campaign-pages.php
    security.php
  assets/
    css/
    js/
```

## Integration Approach

The plugin should call backend APIs through a dedicated client module. The client should manage authentication, request formatting, response handling, retries, and error logging.

## Security Standards

- Store API keys in environment variables or protected WordPress options.
- Use nonces for admin actions.
- Check user capabilities before rendering private modules.
- Sanitize API responses before display.
- Escape output in templates and dashboard components.

## Theme Independence

The plugin should contain ALZO integration logic so themes remain presentation-focused. This allows the site design to change without rebuilding backend connections.

## Future Flexibility

Plugin features should be modular. If WordPress later becomes headless or is replaced, API clients, content models, and workflow assumptions should remain reusable.
