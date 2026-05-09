# Mira Reminder Engine

## Purpose

The Mira Reminder Engine is the future personal continuity layer for calm, respectful reminders, routine support, agenda awareness, medication structure support, and daily check-in prompts.

The engine should reduce cognitive load without creating pressure, shame, or aggressive productivity loops.

## Core Functions

- Track reminders for agenda items, routines, check-ins, and personal continuity needs.
- Distinguish urgent, important, optional, recurring, and parked items.
- Support medication-related structure through reminders and logs without giving medical advice.
- Adapt reminder tone to be calm, humane, and practical.
- Help reschedule or simplify reminders when the day changes.
- Preserve useful patterns for future planning and reflection.

## Reminder Types

| Type | Purpose |
| --- | --- |
| Agenda reminder | Time-bound commitments, appointments, and near-term priorities. |
| Routine reminder | Recurring personal rhythms such as morning, evening, reset, or maintenance routines. |
| Medication structure reminder | Supportive timing and logging cues for medication-related continuity. |
| Check-in reminder | Prompts for mood, energy, stress, sleep, or daily reflection. |
| Follow-up reminder | Deferred tasks, unfinished items, or decisions that need review. |
| Recovery reminder | Gentle cues for rest, hydration, reset, or lower-intensity planning. |

## Reminder Behavior Rules

- Use supportive cues instead of commands.
- Keep reminders concise and context-aware.
- Avoid escalating pressure when a reminder is delayed.
- Offer reschedule, simplify, or park options when appropriate.
- Keep sensitive personal data private and minimal.
- Treat health-related reminders as organizational support, not diagnosis or treatment guidance.

## Future Data Requirements

A production reminder engine should support:

- Stable reminder IDs.
- Recurrence rules.
- Time zone handling.
- Status values such as planned, sent, acknowledged, rescheduled, skipped, and archived.
- Optional links to tasks, routines, check-ins, or memory records.
- Audit-friendly logs for reminder changes and delivery outcomes.

## Dashboard Integration

The reminder engine should eventually feed the Mira dashboard view with:

- Today's reminders.
- Upcoming agenda items.
- Routine status.
- Check-in prompts.
- Deferred or parked items.
- Gentle continuity notes.
