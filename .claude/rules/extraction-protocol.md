---
paths:
  - "extraction/**/*"
---
# Extraction Protocol

## Fact Record Format
Every extracted rule, convention, or configuration item follows this structure:

- **Claim:** What is true (the extracted fact or rule)
- **Source:** File path, exported config file, "operator note [date]", or "audit report"
- **Confidence:** CONFIRMED / LIKELY / UNCERTAIN
- **Impact:** Which SL automation or domain plan uses this
- **Last verified:** Date of source or date Maya confirmed during review
- **Volatility:** *(optional)* STABLE / VOLATILE / UNKNOWN — annotate when a fact is known to change

## Tagging Rules
- `[VERIFY: specific question]` — Attached to UNCERTAIN facts. Must include a question Maya can answer yes/no or with a specific value.
- `[UNKNOWN: what's missing]` — Something that should exist but wasn't found in source material. Explain why it matters.
- `[DISCREPANCY: detail]` — Minor inconsistency between sources that doesn't affect automation (e.g., formatting differences). Document both values.
- `[CONFLICT: source A says X, source B says Y]` — Material disagreement between sources. Cannot be resolved by extraction — escalates to Maya.

## Citation Rules
- Every claim must cite a specific source. "Somewhere in Drive" is not a citation.
- Acceptable source references: file path in sources/, "audit report §[section]", "operator note [date]", "maya-corrections.md [date]"
- If a fact comes from combining multiple sources, cite all of them.
- If a fact cannot be sourced, it must be tagged [VERIFY] or [UNKNOWN].

## Phase 3 Voice Extraction
- Every voice or tone rule must be backed by at least three examples from source material.
- Rules with fewer than three examples: mark [LIKELY] with a note explaining thin evidence.
- The Voice Analyzer subagent handles initial analysis; main thread synthesizes.

## Questions File
- At the end of each phase's extraction, generate `questions.md` in the phase directory.
- Consolidate all [VERIFY] and [UNKNOWN] items with enough context for Maya to answer without re-reading extraction files.
- Group by topic, not by source file.
