# Mira Reminder Schema

## Purpose

This document defines the Phase 2 reminder schema for Mira, the personal AI assistant of the ALZO AI System. The schema supports agenda reminders, medication reminder structure, daily check-ins, routines, habit tracking, recurring schedules, missed reminder handling, and user confirmation flows.

The reminder system should remain calm, respectful, privacy-aware, and supportive. It should reduce cognitive load without creating pressure or aggressive productivity loops.

## Agenda Reminders

Agenda reminders support time-bound commitments, appointments, priorities, and personal planning.

Recommended fields:

| Field | Purpose |
| --- | --- |
| `agenda_item_id` | Stable agenda reminder identifier. |
| `title` | Short reminder title. |
| `description` | Optional context. |
| `scheduled_at` | Date and time of the agenda item. |
| `timezone` | Timezone for reminder delivery. |
| `priority` | Low, normal, high, or urgent. |
| `status` | Planned, sent, acknowledged, rescheduled, missed, skipped, or archived. |
| `confirmation_required` | Whether user acknowledgement is needed. |

## Medication Reminders

Medication reminders provide organizational support only. They are not medical advice, clinical guidance, or treatment recommendations.

Recommended fields:

| Field | Purpose |
| --- | --- |
| `medication_reminder_id` | Stable medication reminder identifier. |
| `label` | User-safe reminder label. |
| `scheduled_at` | Reminder time. |
| `timezone` | Timezone for reminder delivery. |
| `recurrence_rule` | Recurrence pattern when applicable. |
| `status` | Planned, sent, acknowledged, rescheduled, missed, skipped, or archived. |
| `notes` | Non-clinical continuity notes. |

Medication reminder content should avoid dosage interpretation or clinical decision-making unless the user-provided source is explicitly being logged for organizational reference.

## Daily Check-Ins

Daily check-ins support personal continuity, reflection, and planning.

Recommended check-in fields:

- Check-in ID.
- Date and time.
- Mood or emotional tone.
- Energy level.
- Sleep context.
- Stress level.
- Primary focus for the day.
- Support needed.
- Optional reflection notes.
- Follow-up reminders or parked items.

Check-ins should remain lightweight and should not become a burdensome tracking system.

## Routines

Routine records support repeatable personal rhythms.

Routine types may include:

- Morning routine.
- Evening routine.
- Reset routine.
- Meal, hydration, or movement routine.
- Weekly review routine.
- Recovery or low-energy routine.

Recommended fields:

| Field | Purpose |
| --- | --- |
| `routine_id` | Stable routine identifier. |
| `name` | Routine name. |
| `routine_type` | Morning, evening, reset, weekly, recovery, or custom. |
| `steps` | Structured list of routine steps. |
| `preferred_time_window` | Optional delivery or action window. |
| `status` | Active, paused, archived, or needs-review. |
| `metadata` | Support cues, tone preferences, and context. |

## Habit Tracking

Habit tracking should be supportive, non-punitive, and minimal.

Recommended habit fields:

- Habit ID.
- Habit name.
- Purpose.
- Frequency target.
- Check-in method.
- Completion status.
- Streak or trend metadata when useful.
- Notes about friction, support, or adjustments.

Habit records should support pattern recognition without framing missed habits as failure.

## Notification Types

Mira reminders may use different notification types depending on urgency and context.

| Type | Purpose |
| --- | --- |
| `gentle_cue` | Low-pressure reminder or supportive prompt. |
| `agenda_alert` | Time-bound appointment or commitment reminder. |
| `routine_prompt` | Cue to start or continue a routine. |
| `check_in_prompt` | Daily or periodic reflection prompt. |
| `follow_up` | Reminder for a deferred item or next action. |
| `recovery_prompt` | Rest, reset, or lower-intensity support cue. |
| `confirmation_request` | Reminder requiring acknowledgement. |

## Reminder Priority

Priority should guide visibility and timing without creating unnecessary urgency.

| Priority | Meaning |
| --- | --- |
| `low` | Helpful but optional cue. |
| `normal` | Standard reminder. |
| `high` | Important reminder with meaningful consequence if missed. |
| `urgent` | Time-sensitive reminder that should be surfaced clearly. |

Urgency should be used sparingly and only when the situation justifies it.

## Recurring Schedules

Recurring schedules define when reminders or routines repeat.

Recommended recurrence fields:

- Schedule ID.
- Related reminder, routine, or habit ID.
- Start date.
- End date, if applicable.
- Timezone.
- Recurrence rule.
- Next run time.
- Last run time.
- Pause or skip rules.
- Status.

Recurring schedules should be easy to pause, modify, or archive when they no longer fit the user's life.

## Missed Reminder Handling

Missed reminders should be handled calmly and practically.

Recommended flow:

1. Mark the reminder as `missed` after the defined response window passes.
2. Avoid repeated pressure or guilt-based escalation.
3. Offer a simple choice: acknowledge late, reschedule, skip, or park for later.
4. If the reminder is recurring, preserve the next scheduled occurrence unless the user changes it.
5. Log missed status for pattern review only when useful.

Missed reminder analysis should focus on making the system easier to follow, not judging the user.

## User Confirmation Flow

User confirmation supports accountability and reminder state accuracy.

Recommended confirmation states:

| State | Meaning |
| --- | --- |
| `sent` | Reminder was delivered or surfaced. |
| `acknowledged` | User confirmed the reminder. |
| `completed` | User confirmed the related action was completed. |
| `rescheduled` | User moved the reminder to another time. |
| `skipped` | User intentionally skipped it. |
| `parked` | User deferred it without choosing a specific time. |
| `missed` | Reminder window passed without confirmation. |

Confirmation prompts should be short, respectful, and easy to answer.

## Production Requirements

A production reminder schema should support:

- Stable IDs for reminders, routines, habits, and schedules.
- Timezone-aware scheduling.
- Recurrence rules and pause/resume behavior.
- Privacy-aware storage and minimal sensitive detail.
- Audit logs for changes to reminder timing or status.
- Dashboard visibility for today's reminders and parked items.
- Graceful degradation when notification delivery is unavailable.
