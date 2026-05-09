# Role Permissions

## Purpose

Role-based permissions define who can view, request, modify, publish, or administer ALZO AI System capabilities.

## Baseline Roles

| Role | Access Level |
| --- | --- |
| System Admin | Full configuration, user management, integration settings, and security controls. |
| Operator | Manages approved workflows, tasks, dashboards, and studio coordination. |
| Publisher | Creates, reviews, syncs, and publishes approved content. |
| Campaign Manager | Manages campaign metadata, landing pages, conversion events, and reporting views. |
| Viewer | Reads approved dashboards, reports, or published operational summaries. |
| Assistant Runtime | Executes scoped Vera, Mira, or future assistant actions under policy. |
| Integration Client | Uses specific API endpoints granted to an external system. |

## Assistant Access Rules

- Vera may access strategic plans, tasks, reports, and approved memory required for orchestration.
- Mira may access reminders, routines, check-ins, and private continuity context under stricter privacy controls.
- Assistants should execute only actions allowed by their assigned runtime permissions.
- Sensitive memory, user settings, and administrative controls require explicit authorization.
- Assistant actions should be logged with actor, trigger, scope, and result.

## Permission Categories

- Read dashboard data.
- Create or update tasks.
- Read or write memory.
- Publish or sync content.
- Manage campaign configuration.
- Manage users and roles.
- Manage API credentials and integrations.

## Security Considerations

Permissions should be additive, reviewed regularly, and revoked when no longer needed. Public presentation access should never imply private backend access.
