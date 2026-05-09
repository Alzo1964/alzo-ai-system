# ALZO Memory System

## Purpose

The **ALZO Memory System** is the durable context layer for the ALZO AI System. It preserves information that should remain useful beyond a single conversation, task, planning session, project cycle, or studio output.

Memory is not a general notes folder. It is a curated source of continuity for context that helps future work become clearer, faster, safer, and more consistent.

## Directory Structure
## Overview

The **ALZO Memory System** is the durable continuity layer for the ALZO AI System. It stores structured context that should remain useful beyond a single conversation, task, studio cycle, or planning session.

Memory should help Vera, Mira, studios, tasks, templates, reports, and future automation operate with better context over time. It is not a place for raw transcripts, temporary notes, private secrets, or unmanaged information dumps.

## Memory Structure

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
| `memory/mira/` | Personal, reflective, routine, and human-context continuity for Mira. |
| `memory/projects/` | Durable context for projects, initiatives, studios, and workstreams. |
| `memory/tasks/` | Task-related continuity, recurring task patterns, and operational learnings. |
| `memory/decisions/` | Important decisions, rationale, tradeoffs, and future review context. |
| `memory/templates/` | Reusable memory record formats, schemas, and capture patterns. |
| `memory/archive/` | Superseded, inactive, or historically useful memory records. |

## What the Memory System Is

The Memory System is a curated knowledge layer for information that should influence future work. It should preserve:

- Stable preferences and operating patterns.
- Decisions and rationale that affect future execution.
- Project context that should survive beyond an individual task.
- Reusable workflow insights and lessons learned.
- Personal continuity notes that support sustainable planning.
- References that future AI agents or human operators should be able to retrieve.

A good memory record is concise, structured, easy to review, and clearly tied to a future use case.

## What Vera Stores

`memory/vera/` stores executive and system-level continuity for Vera.

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
- System architecture decisions.
- Repository organization rules and routing logic.
- Cross-studio workflow patterns.
- Risk management preferences and escalation patterns.
- Recurring planning frameworks or executive decision criteria.

Vera memory should help preserve system clarity, strategy, governance, and scalable execution.

## What Mira Stores

`memory/mira/` stores personal, reflective, and continuity-oriented context for Mira.

Mira memory may include:

- Personal routine preferences and supportive planning patterns.
- Reminder tone preferences and timing patterns.
- Daily check-in patterns that are useful over time.
- Sustainable productivity preferences.
- Wellness and recovery context that supports practical planning.
- Human-centered communication preferences.

Mira memory should remain respectful, minimal, and useful. It should support care and continuity without over-documenting personal life.

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
- Project objectives and strategic assumptions.
- Audience, product, campaign, publishing, or software context.
- Important constraints, dependencies, and risks.
- Decisions that shape future project work.
- Lessons learned from completed project cycles.
- Links to related tasks, reports, templates, or studio files.

Project memory should make it easier to restart, review, continue, or delegate work without losing context.

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
Decision memory may include:

- The decision made.
- The context that led to the decision.
- Alternatives considered.
- Tradeoffs, risks, and assumptions.
- Date and owner of the decision when known.
- Review triggers or conditions that would justify revisiting the decision.

Decision memory should be especially clear when the decision affects repository structure, automation, data models, backup policy, roles, templates, or long-term operating behavior.

## What Should NOT Be Stored

The Memory System should not store information simply because it exists. Memory should be curated and intentional.

Do **not** store:

- Passwords, API keys, tokens, private keys, or recovery codes.
- Sensitive personal identifiers or unnecessary private details.
- Raw chat transcripts without summarization or clear future value.
- Temporary scratch notes that belong in active tasks or drafts.
- Duplicated files without a clear source-of-truth note.
- Unverified claims presented as durable facts.
- Medical, legal, or financial conclusions that should come from qualified professionals.
- Content that is outdated, ambiguous, or no longer operationally useful unless archived with context.

When in doubt, summarize only the durable pattern or decision and omit unnecessary detail.

## Future Database and Vector Memory Expansion

The initial Memory System is file-based and repository-native. This keeps memory transparent, reviewable, versioned, and easy to back up.

Future expansion may add:

- PostgreSQL tables for structured memory metadata, review status, and relationships.
- Vector search for semantic retrieval across memory records, reports, tasks, and templates.
- Role-aware retrieval for Vera and Mira.
- Automated memory suggestions after major decisions or completed tasks.
- Dashboard views for memory review, stale records, and linked context.
- Governance workflows for approving, archiving, or updating memory records.

Future database or vector memory systems should preserve the repository as the human-readable source of truth unless a documented migration policy says otherwise.

## Memory Record Guidance

Recommended memory records should include:

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
Memory should make future work clearer, calmer, and easier to execute. If a record does not improve continuity, it probably does not belong in memory.
