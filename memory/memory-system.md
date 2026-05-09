# ALZO Memory System

## Purpose

The ALZO Memory System preserves durable context that should remain useful beyond a single task, conversation, project, or studio cycle. It is the continuity layer for decisions, preferences, reusable knowledge, operational patterns, and long-term system learning.

## Core Responsibilities

- Capture decisions that affect future work.
- Preserve reusable context for Vera, Mira, studios, tasks, templates, and reports.
- Separate durable memory from temporary notes, drafts, and active task details.
- Make future retrieval predictable through clear naming, metadata, and placement.
- Support future database-backed memory without breaking the current file-based repository model.

## Memory Categories

| Category | Purpose | Example |
| --- | --- | --- |
| System memory | Durable operating decisions and standards. | Repository structure decisions, naming rules, routing logic. |
| Project memory | Context tied to a specific initiative. | Product assumptions, campaign audience decisions, publishing direction. |
| Personal continuity | Useful personal patterns and preferences. | Routine context, daily rhythm observations, reminder preferences. |
| Reference memory | Stable information used across workflows. | Definitions, frameworks, reusable constraints. |
| Decision memory | Key choices and rationale. | Why a workflow, tool, or structure was selected. |

## Storage Model

The first version of the Memory System is file-based and repository-native. Future versions may use PostgreSQL or a vector search layer, but repository documents remain the baseline source of truth for durable operating context.

Recommended memory record structure:

```markdown
# Memory Title

## Summary

## Context

## Decision / Pattern

## Applies To

## Last Reviewed

## Notes
```

## Governance Rules

- Store only context that has durable future value.
- Avoid saving sensitive data, raw credentials, or unnecessary personal details.
- Prefer concise summaries over unfiltered transcripts.
- Link memory records to tasks, reports, templates, or studio files when relevant.
- Review memory periodically to archive outdated, duplicated, or superseded context.

## Future Automation Path

The Memory System should be designed so future AI agents can:

1. Search memory by topic, domain, role, project, and date.
2. Retrieve relevant context before planning or execution.
3. Propose updates when a durable decision is made.
4. Distinguish confirmed memory from temporary notes.
5. Sync structured records into PostgreSQL or another approved data store.
