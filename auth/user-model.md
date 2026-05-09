# User Model

## Purpose

The user model defines how people, administrators, assistants, and integration clients are represented inside the ALZO AI System.

## User Types

| Type | Purpose |
| --- | --- |
| Admin | Manages system configuration, users, roles, integrations, and security settings. |
| User | Accesses approved dashboards, workflows, reminders, publishing tools, or campaign views. |
| Assistant | Represents Vera, Mira, or future assistant runtimes acting under defined rules. |
| Integration Client | Represents external systems such as WordPress, automation tools, or API consumers. |

## Core Fields

- Unique user ID.
- Display name.
- Email or primary identifier.
- Role assignments.
- Account status.
- Authentication provider.
- Created, updated, and last active timestamps.

## Admin/User Separation

Admin accounts should be used only for configuration, permissions, and sensitive operations. Daily work should occur through standard user roles to reduce risk and improve audit clarity.

## Assistant Identity

Assistants should not share human user accounts. Vera, Mira, and future assistants should have distinct identities or service principals with scoped permissions, action limits, and traceable activity records.

## WordPress Integration Option

WordPress users may map to ALZO users through email, external identity ID, or a linked account table. WordPress can initiate login or dashboard access, but backend permissions should remain authoritative for private ALZO data.
