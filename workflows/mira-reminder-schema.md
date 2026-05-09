# Mira Reminder Schema

## Purpose

This document defines the Phase 2 reminder schema for Mira, the human-centered and continuity-oriented intelligence layer of the ALZO AI System. It describes how agenda reminders, medication reminders, daily check-ins, routines, habit tracking, notification types, reminder priority, recurring schedules, missed reminder handling, and user confirmation should be structured for future implementation.

The schema is designed to support practical personal continuity without replacing medical, legal, or professional judgment. Medication-related reminders are organizational support only and should not be treated as diagnosis, treatment, or clinical instruction.

## Reminder Design Principles

1. **Human usefulness first.** Reminders should reduce cognitive load without creating unnecessary pressure or noise.
2. **Explicit consent and confirmation.** Sensitive or high-priority reminders should make acknowledgement requirements clear.
3. **Flexible recurrence.** Daily life patterns need exceptions, pauses, grace windows, and schedule changes.
4. **Respectful escalation.** Missed reminders should prompt useful follow-up without becoming punitive.
5. **Privacy by design.** Personal data should carry sensitivity, retention, and visibility rules.
6. **Operational traceability.** Reminder creation, delivery, confirmation, snoozing, and missed states should be logged.
7. **Assistant-ready structure.** Mira should be able to summarize, prioritize, and adjust reminders based on structured state.

## Reminder Categories

| Category | Purpose | Typical Owner |
| --- | --- | --- |
| `agenda` | Calendar-adjacent events, appointments, commitments, calls, errands, and deadlines. | Mira. |
| `medication` | Medication timing support, refill prompts, and acknowledgement tracking. | Mira with high sensitivity. |
| `daily_check_in` | Morning, midday, evening, or custom personal status check-ins. | Mira. |
| `routine` | Repeating life patterns such as meals, sleep preparation, cleanup, planning, and transitions. | Mira. |
| `habit` | Behavior tracking for consistency, streaks, reflection, or lightweight accountability. | Mira. |
| `custom` | User-defined reminder that does not fit another category. | Mira or user. |

## Core Reminder Record

A reminder record should include:

| Field | Purpose |
| --- | --- |
| `reminder_id` | Stable unique identifier. |
| `title` | Short reminder label. |
| `description` | Plain-language context or instruction. |
| `reminder_type` | `agenda`, `medication`, `daily_check_in`, `routine`, `habit`, or `custom`. |
| `priority` | `low`, `normal`, `high`, or `urgent`. |
| `sensitivity_level` | `public`, `internal`, `private`, or `restricted`. |
| `schedule_id` | Link to one-time or recurring schedule. |
| `notification_profile_id` | Link to channel, timing, and escalation settings. |
| `confirmation_required` | Whether acknowledgement is required. |
| `default_snooze_minutes` | Suggested snooze interval. |
| `grace_period_minutes` | Time before a due reminder becomes missed. |
| `status` | `active`, `paused`, `completed`, `cancelled`, or `archived`. |
| `created_at` / `updated_at` | Standard audit timestamps. |

## Agenda Reminders

Agenda reminders support practical commitments and time-aware planning.

### Recommended Fields

- Event title.
- Event type, such as appointment, call, deadline, errand, travel, or preparation.
- Start time and optional end time.
- Location or meeting link when relevant.
- Preparation checklist.
- Related project, task, or person.
- Travel buffer or setup buffer.
- Confirmation requirement.
- Follow-up notes after completion.

### Agenda Flow

1. Capture commitment and timing.
2. Identify preparation needs and buffer time.
3. Schedule advance notification and due notification.
4. Request confirmation when appropriate.
5. Log completion, snooze, missed state, or follow-up needs.

## Medication Reminders

Medication reminders provide organizational support for user-defined medication timing.

### Safety Boundaries

- Mira should not prescribe, alter dosage, or infer medical instructions.
- Medication details should be user-provided or sourced from a trusted user-confirmed record.
- Sensitive medication data should default to `restricted` unless the user chooses otherwise.
- Missed medication handling should encourage the user to follow their clinician, pharmacist, or medication label guidance rather than giving clinical advice.

### Recommended Fields

- Medication label or user-defined name.
- User-confirmed timing.
- Optional dose label, if the user chooses to store it.
- Refill reminder date or remaining quantity threshold.
- Confirmation required flag.
- Missed reminder grace period.
- Sensitive notes.
- Emergency escalation disabled by default unless explicitly configured by the user.

### Medication Confirmation States

| State | Meaning |
| --- | --- |
| `pending` | Reminder has been delivered but not acknowledged. |
| `confirmed` | User confirmed completion. |
| `snoozed` | User deferred the reminder. |
| `missed` | Grace period elapsed without confirmation. |
| `skipped` | User intentionally skipped the reminder. |
| `cancelled` | Reminder occurrence was cancelled. |

## Daily Check-Ins

Daily check-ins help Mira maintain personal continuity and support sustainable routines.

### Check-In Types

| Type | Purpose |
| --- | --- |
| `morning` | Set focus, agenda, energy level, and priorities. |
| `midday` | Review progress, meals, medication confirmations, and schedule changes. |
| `evening` | Reflect on completion, mood, unfinished items, and tomorrow preparation. |
| `custom` | User-defined check-in tied to a specific routine or life pattern. |

### Recommended Prompt Fields

- Energy level.
- Mood or emotional context.
- Top priorities.
- Agenda changes.
- Medication or wellness confirmations, when configured.
- Meals, hydration, movement, or rest notes, when configured.
- Open loops and tomorrow carryovers.

## Routines

Routines group multiple reminders, habits, and check-ins into a reusable sequence.

### Routine Structure
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
| `name` | Routine label. |
| `routine_type` | `morning`, `work_block`, `transition`, `evening`, `weekly`, or `custom`. |
| `steps` | Ordered JSONB list of actions, reminders, or prompts. |
| `schedule_id` | Recurrence or trigger schedule. |
| `flexibility` | `strict`, `standard`, or `flexible`. |
| `status` | `active`, `paused`, `archived`. |

### Routine Execution States

- `not_started`
- `in_progress`
- `partially_completed`
- `completed`
- `skipped`
- `missed`

## Habit Tracking

Habit tracking should support consistency without creating unnecessary shame or over-optimization.

### Recommended Fields

- Habit name.
- Reason or intention.
- Target cadence.
- Minimum viable completion definition.
- Tracking unit, such as yes/no, count, duration, or note.
- Streak status, if helpful.
- Reflection notes.
- Pause and reset rules.

### Habit Review Metrics

- Completion rate by week or month.
- Current streak and longest streak, when enabled.
- Missed occurrence patterns.
- User-noted obstacles.
- Suggested adjustment, pause, or simplification.

## Notification Types

| Notification Type | Purpose |
| --- | --- |
| `advance_notice` | Heads-up before a due time. |
| `due_now` | Reminder is due. |
| `confirmation_request` | User acknowledgement is required. |
| `snooze_follow_up` | Snoozed reminder is due again. |
| `missed_notice` | Grace period elapsed without confirmation. |
| `daily_digest` | Summary of upcoming or unresolved reminders. |
| `weekly_review` | Pattern review for routines, habits, and recurring commitments. |

## Reminder Priority

| Priority | Meaning | Behavior |
| --- | --- | --- |
| `low` | Useful but optional. | May appear in digests only. |
| `normal` | Standard reminder. | Send configured notifications without escalation. |
| `high` | Important to acknowledge. | Require confirmation or follow-up notice when configured. |
| `urgent` | Time-sensitive and user-designated as critical. | Use stronger notification profile and explicit missed handling. |

Priority should be user-configurable and should not be inferred in a way that creates unsafe or excessive escalation.

## Recurring Schedules

Recurring schedules should support standard recurrence and real-life exceptions.

### Schedule Fields

- `schedule_id`.
- `schedule_type`: `one_time`, `daily`, `weekly`, `monthly`, `custom_rrule`, or `event_triggered`.
- Timezone.
- Start date and optional end date.
- Time of day or event trigger.
- Recurrence rule.
- Exception dates.
- Skip windows.
- Quiet hours.
- Grace period.
- Pause state.

### Recurrence Rules

Use a structured recurrence rule format that can map to RFC 5545-style recurrence when implementation begins. Store human-readable recurrence metadata alongside machine-readable rules so Mira can explain the schedule clearly.

## Missed Reminder Handling

Missed reminder handling should be supportive, practical, and configurable.

### Missed Flow

1. Reminder occurrence is delivered.
2. If confirmation is required, wait through the grace period.
3. If no confirmation is received, mark occurrence as `missed`.
4. Send a missed notice only if the notification profile allows it.
5. Offer user actions: confirm completed, snooze, skip, reschedule, pause, or edit.
6. Log missed occurrence and update habit, routine, or reminder history.
7. Surface repeated missed patterns during daily or weekly review instead of escalating indefinitely.

### Missed Reminder States

| State | Meaning |
| --- | --- |
| `delivered` | Notification was sent. |
| `pending_confirmation` | Waiting for acknowledgement. |
| `snoozed` | Temporarily deferred. |
| `missed` | Grace period elapsed. |
| `resolved_late` | User confirmed after missed state. |
| `skipped` | User intentionally skipped. |
| `rescheduled` | User moved the occurrence. |

## User Confirmation Flow

User confirmation should be simple, explicit, and logged.

### Confirmation Actions

| Action | Result |
| --- | --- |
| `confirm` | Mark occurrence complete. |
| `snooze` | Create a follow-up notification at the selected interval. |
| `skip` | Mark occurrence intentionally skipped. |
| `reschedule` | Move one occurrence or the recurring schedule. |
| `pause` | Temporarily disable future notifications. |
| `edit` | Update reminder content, timing, priority, or notification profile. |
| `cancel` | Cancel the occurrence or reminder. |

### Confirmation Event Record

Each interaction should create a reminder event with:

- `event_id`.
- `reminder_id`.
- `occurrence_id`.
- `event_type`.
- `user_action`.
- `previous_state`.
- `new_state`.
- `timestamp`.
- `note`, if provided.
- `source_channel`.

## Notification Profiles

Notification profiles define channels, timing, and escalation behavior.

| Field | Purpose |
| --- | --- |
| `notification_profile_id` | Stable profile identifier. |
| `name` | Profile label. |
| `channels` | App, email, SMS, calendar, voice, or future channel list. |
| `advance_offsets` | Minutes, hours, or days before due time. |
| `quiet_hours` | Times when non-urgent notifications should be suppressed. |
| `escalation_enabled` | Whether follow-up notifications are allowed. |
| `max_follow_ups` | Maximum missed or snooze follow-ups. |
| `digest_inclusion` | Whether unresolved reminders appear in daily or weekly digests. |

## Review and Adjustment

Mira should periodically review reminder effectiveness.

Review should identify:

- Reminders that are repeatedly missed.
- Habits that may need a lower minimum viable target.
- Routines that are too rigid or too vague.
- Medication reminder settings that need user confirmation.
- Agenda reminders that require better preparation buffers.
- Notification profiles that are too noisy or too quiet.

Recommended review cadence:

- Daily for unresolved high-priority reminders.
- Weekly for routines and habits.
- Monthly for inactive, stale, or low-value reminders.
- Immediately when the user reports that a reminder is wrong, stressful, unsafe, or no longer useful.
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
