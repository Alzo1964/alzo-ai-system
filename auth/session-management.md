# Session Management

## Purpose

Session management controls how authenticated users remain connected to ALZO dashboards, APIs, and integrated presentation layers.

## Session Rules

- Use secure, HTTP-only cookies for browser sessions.
- Require HTTPS in production environments.
- Set reasonable expiration windows for standard and admin sessions.
- Refresh sessions only after validating account status and permissions.
- Invalidate sessions after password changes, role changes, or suspicious activity.

## Admin Sessions

Admin sessions should have shorter lifetimes and may require additional verification for sensitive actions such as role updates, integration credentials, or assistant permission changes.

## WordPress Sessions

If WordPress user integration is enabled, WordPress sessions may act as an entry point for public or editorial workflows. Private ALZO dashboard access should still require backend authorization checks before any sensitive data is shown.

## API Sessions

Future API authentication should support token-based access for trusted clients. Tokens should be scoped, revocable, time-limited where practical, and tied to integration client identities.

## Audit Events

Session creation, refresh, expiration, revocation, and failed validation should be logged with timestamp, actor, client, and request context while avoiding unnecessary sensitive data capture.
