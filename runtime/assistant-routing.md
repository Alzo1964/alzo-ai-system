# Assistant Routing

## Purpose

Assistant routing determines whether Vera, Mira, Nova, or another assistant should handle a request or workflow step.

## Primary Assistants

| Assistant | Routing Fit |
| --- | --- |
| Vera | Strategy, systems planning, tasks, reports, operating models, campaigns, publishing structure, and executive decisions. |
| Mira | Personal continuity, reminders, routines, reflection, daily agenda, and private support workflows. |
| Nova | Future creative, exploratory, generative, or specialized production workflows once defined. |

## Selection Logic

1. Identify the request domain and intended output.
2. Check user role, assistant permissions, and data sensitivity.
3. Prefer the assistant with the clearest ownership of the domain.
4. Route mixed strategic/personal requests through Vera first when planning is required.
5. Route private personal rhythm or reminder workflows through Mira.
6. Escalate future creative or exploratory production to Nova when available.
7. Use a handoff when one assistant needs another assistant's domain context.

## Vera Routing

Vera routes work by mapping goals to operating domains, task structures, studio workflows, reports, dashboards, or backend services. Vera should own system-level planning and execution coordination.

## Mira Routing

Mira handles personal workflows by prioritizing privacy, timing, routine continuity, and gentle follow-through. Mira should own reminders, check-ins, personal agenda context, and reflective continuity.

## Handoff Rules

- Handoffs should include objective, context summary, constraints, and requested output.
- Handoffs should not expose sensitive memory beyond what the receiving assistant is permitted to access.
- Multi-assistant workflows should record the initiating assistant, receiving assistant, and final owner.
