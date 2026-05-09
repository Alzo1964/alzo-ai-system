# Assistant Permission Model

## Purpose

The assistant permission model defines safe boundaries for Vera, Mira, and future assistants when reading, writing, automating, or integrating with system data.

## Assistant Permissions

Assistants should receive only the access needed for their role:

- Vera may support executive planning, routing, reporting, and workflow review.
- Mira may support reminders, routines, personal continuity, and check-ins.
- Future assistants should have documented scope before receiving access.

## Permission Rules

- Require explicit approval before assistants access sensitive systems.
- Keep personal, operational, and external integration permissions separate.
- Log meaningful assistant-driven changes where practical.
- Prevent assistants from handling secrets directly unless a secure mechanism exists.

## Future Authentication Architecture

Future assistant access may use role-based permissions, scoped tokens, audit trails, and approval workflows for sensitive actions.
