---
paths:
  - "output/**/*"
---
# Output Standards

## The Core Rule
Nothing enters output/ without Maya's explicit approval. If it's in output/, Maya has signed off on it. This is the project's fundamental trust invariant.

## Knowledge Layer (output/knowledge/)
- Markdown prose for humans. Explains rationale, captures nuance, documents "why."
- Each file has a clear scope — don't let files bleed into each other's territory.
- identities.md: Steph/Maya/Lingua Ink identity map and routing rules
- clients.md: Client profiles, relationships, contexts
- conventions.md: Naming rules, formatting preferences, patterns
- rhythms.md: Weekly/monthly cadences and recurring patterns
- tools.md: Tool inventory with configs and access details
- policies.md: Automation safety boundaries, privacy rules, identity protection, client confidentiality, safe experimentation boundaries for SL testing

## Data Layer (output/data/)
- YAML/JSON for machines. Exact IDs, mappings, values that SL loads directly as configuration.
- Must be parseable and loadable — validate syntax before committing.
- Cross-file consistency is required (validated in Phase 5):
  - Client names in client-registry.yaml must match Project options in clickup-fields.yaml
  - Email addresses in email-identities.yaml must match calendar addresses in calendar-map.yaml
  - Any mismatches go in gaps.md

## Domain Plans (output/domain-plans/)
- Skeletons during Phases 1–4: Purpose + Inputs + System Overview only.
- Finalized in Phase 5 only, when all upstream knowledge has been reviewed.
- Every plan follows the template in output/domain-plans/_template.md
- Finalized plans must include implementation-level detail: API endpoints, field UUIDs, exact rules, specific values. Not prose descriptions of "how things generally work."

## Agent Designs (output/agent-designs/)
- These are prototypes — initial designs that SL will refine during implementation.
- Label them clearly as prototypes. Do not imply they are final.
- Follow the subagent format: YAML frontmatter (role, model, tools, maxTurns) → personality → checklist → reporting format.

## Minimum-Required-Review Summary
- When presenting output for Maya's review, include a summary of the 3–5 most critical items to confirm.
- This helps Maya prioritize when time is short.
