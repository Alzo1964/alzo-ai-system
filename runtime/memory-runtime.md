# Memory Runtime

## Purpose

The memory runtime governs how assistants read, write, filter, and apply memory across ALZO workflows.

## Read Flow

1. Assistant requests memory for a defined purpose.
2. Runtime checks user identity, assistant permission, sensitivity, and domain relevance.
3. Memory service retrieves structured records from the primary datastore.
4. Optional vector retrieval returns semantic matches when enabled.
5. Runtime filters results and provides only approved context to the assistant.
6. Read event is logged for audit and continuity.

## Write Flow

1. Assistant proposes a memory update from a task, reflection, report, or user instruction.
2. Runtime classifies the update by domain, sensitivity, durability, and retention value.
3. User confirmation is required for sensitive or long-term personal memory when appropriate.
4. Memory service stores the approved record with source, timestamp, owner, and access scope.
5. Related tasks, reports, dashboards, or reminders receive references rather than duplicated private content.

## Safety Rules

- Never expose private memory to unauthorized users, assistants, dashboards, or integrations.
- Prefer summaries over raw sensitive entries when full detail is unnecessary.
- Keep Mira personal context more restrictive by default.
- Keep Vera strategic context accessible only when needed for planning or execution.
- Separate memory records from public publishing content.

## Future Vector Support

Vector search should be an optional retrieval layer behind the memory service. It should improve relevance without becoming the source of truth for memory, permissions, or retention policy.

## Future Multi-Agent Expansion

As Nova and future assistants are added, each assistant should receive scoped memory access based on role, task purpose, and sensitivity rules. Shared memory should be explicit, not assumed.
