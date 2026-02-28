# Domain Plan: ClickUp Automation

## Purpose
Automate task creation, field population, and status management in Maya's ClickUp Master Task List. Reduces manual data entry while preserving the meticulous custom-field tagging that makes ClickUp function as external memory.

## Inputs
- knowledge/conventions.md — ClickUp naming conventions, status flow, Approach field semantics
- knowledge/tools.md — ClickUp architecture (workspace/space/list IDs), usage patterns
- data/clickup-fields.yaml — All 6 custom fields with complete option IDs, status definitions
- data/client-registry.yaml — Project field values mapped to client names

## System Overview
Maya manages a single Master Task List (ID `901318968458`) in Space "Task Dashboard" (ID `90139879792`), Workspace `90132317650`. She uses ClickUp almost daily.

**Task creation:** Manual. Task names start with a lowercase verb, kept short and actionable. Due dates are always set. Descriptions are optional (used for meeting notes, zoom links, addresses).

**Custom fields:** All 6 fields are populated on every task — Project (16 options mapping to clients/business lines), Effort (Tiny through Very Big), Revenue (None through Direct High), Scope (Internal/External), Approach (Dread through Excited), Readiness (Prepared/Upskilling). The Approach field is an emotional energy metric tied to the Zeigarnik effect — it's structural, not decorative.

**Status flow:** Not Started → Begun → Complete is typical. On Hold and Waiting are parking states. Scratch is for abandoned tasks. Maya's one inconsistency: sometimes a few days pass before she marks tasks complete.

**Checklists:** Not used. **Labels/tags:** Not used.

**Key constraint:** The Approach field requires Maya's subjective input — it cannot be inferred or automated.
