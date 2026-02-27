# Seamless Bootstrap — CLAUDE.md

## Quick Reference
- **Repo:** seamless-bootstrap (private)
- **Purpose:** Extract and organize Maya Bairey's institutional knowledge into structured deliverables for the Seamless (SL) automation project
- **Owner:** Maya Bairey (stephbairey/seamless-bootstrap)
- **Current phase:** See `current-phase.md`
- **Auto memory:** DISABLED. All state lives in committed files.

## Session Start Checklist
1. Read `current-phase.md` for active phase and status
2. Read `pending-questions.md` for outstanding items
3. Read `maya-corrections.md` for known source errors
4. Read the relevant Phase section in `plan.md` — only the current phase, not the whole file

## Project Structure
```
sources/                    # Raw inputs (Maya populates)
  drive-files/              # Google Drive exports
  website-exports/          # linguaink.com, bairey.com
  local-docs/               # Contracts, plans, style notes
  system-snapshots/         # Live config exports (Gmail XML, n8n JSON, ClickUp JSON, .ics)
  operator-notes/           # Maya's in-head knowledge, committed as source
  prior-work/               # Audit doc, brand inventory, prior Claude work

extraction/                 # Intermediate work (Claude Code writes here)
  manifest.md               # Phase 0 source catalog
  technical-systems/        # Phase 1
  business-operations/      # Phase 2
  brand-identity/           # Phase 3
  content-marketing/        # Phase 4
  fact-index.md             # Phase 5 global fact index

output/                     # Polished deliverables (Maya-approved only)
  knowledge/                # Markdown prose reference docs
  data/                     # YAML/JSON machine-readable config
  domain-plans/             # Automation domain instructions (skeletons until Phase 5)
  agent-designs/            # Prototype designs for SL agents
  seamless-claude-md-draft.md
  HANDOFF.md
  gaps.md

.claude/agents/             # SB operational subagents
.claude/rules/              # Path-scoped extraction/output/source rules
```

## Glossary
- **SB** — Seamless Bootstrap (this project). Extraction and organization only.
- **SL** — Seamless (the automation project). Consumes SB output. Empty until SB completes.
- **Maya** — The operator's name. Always use this.
- **Steph/Stephanie** — Maya's legal name. Use only when documenting identity routing.
- **Lingua Ink Media** — Maya's business entity for creative services.
- **ARC/TDA** — Tomahawk Destiny Association. Organizational commitment.
- **PRG** — Portland Raging Grannies. Maya creates/distributes newsletter.
- **IRG** — International Raging Grannies.
- **Zeigarnik effect** — Unfinished tasks create cognitive burden. Maya's task management accounts for this.
- **Sailor's Code** — Maya's novel in progress.

## Always
- Read session start checklist before beginning work
- Check `maya-corrections.md` before trusting any source
- Mark uncertainty: `[VERIFY: specific question for Maya]`
- Mark gaps: `[UNKNOWN: what's missing and why it matters]`
- Mark minor inconsistencies: `[DISCREPANCY: detail]`
- Cite source files for every extracted fact
- Use "Maya" as the operator's name
- Generate `questions.md` in each phase directory consolidating all [VERIFY] and [UNKNOWN] items
- Update `current-phase.md` at end of each session
- Present extraction alongside proposed output for Maya to review in one pass
- For extraction rules and fact record format, see `.claude/rules/extraction-protocol.md`
- For output quality requirements, see `.claude/rules/output-standards.md`
- For source precedence and conflict resolution, see `.claude/rules/source-handling.md`

## Never
- Fabricate details not found in source material
- Use pattern-matching to fill gaps unless Maya explicitly asks
- Flatten emotional/psychological dimensions of Maya's systems — these are structural, not decorative
- Proceed past a review gate without Maya's approval
- Use "Steph" except when documenting identity routing
- Assume a file is current without checking the approved manifest
- Write automation logic — SB produces documents and data files, not code
- Read the entire plan.md every session — read only the current phase section

## Phases
```
Pre-Phase:  Maya completes system export checklist (with sanitization)
Phase 0:    Source triage + Inventory → manifest.md
Phase 1:    Technical Systems → extraction/technical-systems/
Phase 2:    Business Operations → extraction/business-operations/
Phase 3:    Brand Identity → extraction/brand-identity/ (Voice Analyzer subagent)
Phase 4:    Content & Marketing → extraction/content-marketing/
Phase 5:    Synthesis → finalize domain plans, cross-validate data, fact index, handoff simulation, HANDOFF.md
```
After completing a phase: commit, update `current-phase.md`, report to Maya, wait for approval.

## Compaction Instructions
When context is compacted, always preserve:
- Current phase number and status
- Files modified this session
- Pending questions for Maya
- Manifest approval status
- Which output/ files are approved vs. draft
- Any unresolved [CONFLICT] items
- Reference: "Source precedence and rules in .claude/rules/"
