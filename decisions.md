# Decisions

Architecture Decision Records for Seamless Bootstrap. Captures what was decided, why, and what was rejected — so we don't relitigate at every review gate.

---

## ADR 001: Extraction/Output Split

**Status:** Accepted  
**Date:** February 27, 2026  
**Context:** SB produces intermediate extraction work and polished deliverables. Should they share a directory?  
**Decision:** Separate `extraction/` and `output/` directories. Extraction is messy intermediate work; output is Maya-approved.  
**Rationale:** Maya needs a clear trust boundary. If it's in `output/`, she signed off on it. Mixing draft and approved content erodes that signal.  
**Alternatives rejected:** Single directory with status tags on files — harder to scan, easy to miss a draft.  
**Consequences:** Slightly more directory structure, but review gates have a clean boundary.

---

## ADR 002: Auto Memory Disabled

**Status:** Accepted  
**Date:** February 27, 2026  
**Context:** Claude Code supports auto memory that persists across sessions. Helpful for continuity but introduces untraceable facts.  
**Decision:** Disable auto memory for SB. Maintain continuity through `current-phase.md`, `pending-questions.md`, and `maya-corrections.md`.  
**Rationale:** SB is an extraction project where traceability is the whole point. Every fact in output must be sourceable to a committed file. Auto memory makes that unenforceable — Claude Code can't prove where a fact came from.  
**Alternatives rejected:** "Speed-first with mitigation" — leave auto memory on but require traceability before promoting to output. Rejected because the enforcement problem is real: Claude Code might incorrectly populate source fields from memory.  
**Consequences:** Sessions start clean. Slightly more overhead maintaining state files. Worth it for auditability.

---

## ADR 003: Source Precedence Order

**Status:** Accepted  
**Date:** February 27, 2026  
**Context:** Sources will conflict. Need a deterministic resolution hierarchy.  
**Decision:** Seven-level hierarchy: (1) maya-corrections.md, (2) operator corrections in review, (3) operator notes, (4) system snapshots, (5) signed contracts/dated docs, (6) website copy, (7) undated notes/drafts.  
**Rationale:** Maya's explicit corrections are the highest authority. System snapshots represent how things actually work. Website copy is authoritative for brand but unreliable for operations. Undated material is useful but unverifiable.  
**Alternatives rejected:** "Ask Maya every time" — doesn't scale, creates bottleneck. Flat precedence (all sources equal) — forces escalation on every conflict.  
**Consequences:** Most conflicts resolve by rule. Only genuinely ambiguous cases escalate to Maya via [CONFLICT] tag.

---

## ADR 004: Domain Plan Skeleton Strategy

**Status:** Accepted  
**Date:** February 27, 2026  
**Context:** Domain plans drafted after Phase 1 would need rewriting when later phases reveal new context (e.g., email triage depends on identity boundaries from Phase 3).  
**Decision:** Domain plans are skeletons during Phases 1–4 (Purpose + Inputs + System Overview only). Finalized in Phase 5 when all upstream knowledge has been reviewed.  
**Rationale:** Prevents rewrite churn. Cross-phase dependencies mean early-drafted plans are guaranteed to be incomplete.  
**Alternatives rejected:** Full draft after each phase, revise as needed — predictable rework with no upside. Defer entirely to SL — loses the benefit of writing plans while extraction knowledge is fresh.  
**Consequences:** Phase 5 is heavier. Skeletons serve as structural placeholders that accumulate inputs across phases.

---

## ADR 005: Data Layer Format

**Status:** Accepted  
**Date:** February 27, 2026  
**Context:** SL needs machine-readable configuration (IDs, mappings, routing rules). Should this live in Markdown tables or separate data files?  
**Decision:** Separate YAML/JSON files in `output/data/`. Cross-validated for consistency in Phase 5.  
**Rationale:** SL loads these directly as config. Markdown tables require re-parsing prose to extract constants — fragile and hallucination-prone. YAML is loadable, diffable, and unambiguous.  
**Alternatives rejected:** Embed data in knowledge layer Markdown — requires SL to parse prose for values. JSON only — YAML is more human-readable for review.  
**Consequences:** Five data files to maintain. Cross-validation step in Phase 5 ensures consistency. Knowledge layer prose explains rationale; data layer provides exact values.
