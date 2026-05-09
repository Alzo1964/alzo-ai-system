# ALZO Memory System

## Purpose

The **ALZO Memory System** is the durable context layer for the ALZO AI System. It preserves information that should remain useful beyond a single conversation, task, planning session, project cycle, or studio output.

Memory is not a general notes folder. It is a curated source of continuity for context that helps future work become clearer, faster, safer, and more consistent.

## Directory Structure

```text
memory/
├── vera/
├── mira/
├── projects/
├── tasks/
├── decisions/
├── templates/
├── archive/
├── README.md
└── memory-system.md
```

| Directory | Purpose |
| --- | --- |
| `memory/vera/` | Strategic, executive, and system-level continuity for Vera. |
| `memory/mira/` | Personal, reflective, routine, and human-centered continuity for Mira. |
| `memory/projects/` | Durable context for projects, initiatives, studios, and workstreams. |
| `memory/tasks/` | Recurring task context, task patterns, and operational learnings. |
| `memory/decisions/` | Important decisions, rationale, tradeoffs, assumptions, and review triggers. |
| `memory/templates/` | Reusable memory formats, schemas, capture prompts, and record patterns. |
| `memory/archive/` | Superseded, inactive, historical, or no-longer-current memory records. |

## What the Memory System Stores

The Memory System should store concise, structured records that improve future execution or continuity.

Appropriate memory includes:

- Stable preferences, standards, and operating patterns.
- Decisions and rationale that should be available for future review.
- Project context that should survive beyond an individual task.
- Lessons learned from completed work.
- Reusable workflow knowledge.
- Personal continuity context that supports planning, routines, reminders, or check-ins.
- References that future agents or collaborators should be able to retrieve.

A strong memory record should be specific, current, easy to scan, and tied to a clear future use.

## What Vera Stores

`memory/vera/` stores executive and system-level memory for Vera.

Vera memory may include:

- Strategic priorities and operating principles.
- Repository structure decisions and routing rules.
- System architecture context.
- Cross-studio workflow patterns.
- Risk management preferences and escalation rules.
- Planning frameworks, decision criteria, and governance standards.
- Reusable executive summaries or operating models.

Vera memory should strengthen strategic clarity, modular execution, repository quality, and long-term system coherence.

## What Mira Stores

`memory/mira/` stores personal, reflective, and continuity-oriented memory for Mira.

Mira memory may include:

- Routine preferences and supportive daily planning patterns.
- Reminder tone, cadence, and timing preferences.
- Daily check-in patterns that are useful over time.
- Sustainable productivity preferences.
- Wellness, rest, and recovery context that supports practical planning.
- Human-centered communication preferences.

Mira memory should remain respectful, minimal, and operationally useful. It should support care and continuity without over-documenting personal life.

## What Project Memory Stores

`memory/projects/` stores durable context for projects, initiatives, and studio workstreams.

Project memory may include:

- Project objectives and current strategic assumptions.
- Audience, product, campaign, software, or publishing context.
- Important constraints, dependencies, and known risks.
- Decisions that shape future project execution.
- Lessons learned from completed cycles.
- References to related tasks, reports, templates, studio files, or decision records.

Project memory should make work easier to restart, review, delegate, or continue without losing essential context.

## What Decision Memory Stores

`memory/decisions/` stores important decisions and the reasoning behind them.

Decision memory should capture:

- The decision that was made.
- The context that led to the decision.
- Alternatives considered.
- Tradeoffs, assumptions, and risks.
- Date, owner, or deciding role when known.
- Related files, tasks, projects, reports, or policies.
- Review triggers that would justify revisiting the decision.

Decision memory is especially important when choices affect repository structure, agent behavior, automation, data models, workflow routing, task templates, backup policy, or long-term operating standards.

## What Should NOT Be Stored

Memory should be intentional. Do not store information simply because it was mentioned.

Do **not** store:

- Passwords, API keys, access tokens, private keys, or recovery codes.
- Sensitive personal identifiers or unnecessary private details.
- Raw conversation transcripts without a concise durable summary.
- Temporary scratch notes that belong in active tasks, drafts, or working files.
- Duplicate documents unless they are clearly marked as snapshots or archived references.
- Unverified claims presented as durable facts.
- Medical, legal, or financial conclusions that should come from qualified professionals.
- Outdated context unless it is archived with a clear historical note.
- Information that does not improve future planning, execution, review, or continuity.

When unsure, store the durable pattern, decision, or preference instead of the full raw context.

## Future Database and Vector Memory Expansion

The initial Memory System is file-based and repository-native. This keeps memory transparent, versioned, reviewable, portable, and easy to back up.

Future expansion may include:

- PostgreSQL tables for structured memory metadata, relationships, review status, and lifecycle tracking.
- Vector search for semantic retrieval across memory records, tasks, reports, templates, and project documents.
- Role-aware retrieval for Vera, Mira, and future specialized agents.
- Automated memory suggestions after major decisions, completed tasks, or recurring workflow patterns.
- Dashboard views for memory review, stale records, linked context, and retrieval health.
- Governance workflows for approving, updating, archiving, or deleting memory records.

Any future database or vector memory layer should preserve clear source-of-truth rules. Repository-based memory remains the human-readable baseline unless a documented migration policy establishes a new authoritative store.

## Recommended Memory Record Format

```markdown
# Memory Title

## Summary

## Context

## Durable Pattern / Decision

## Applies To

## Related Files

## Last Reviewed

## Notes
```

Memory should make the ALZO AI System easier to operate over time. If a record does not improve clarity, continuity, or execution, it probably does not belong in memory.
