# Seamless Bootstrap (SB) — Project Plan

**Version:** 1.2 — Final  
**Date:** February 27, 2026  
**Author:** Claude (with Maya Bairey)  
**Purpose:** Comprehensive reference for the Seamless Bootstrap project. Claude Code reads the relevant section at the start of each phase — not the entire file every session.

---

## 1. What This Project Is

Seamless Bootstrap (SB) is an extraction and organization project. It takes Maya's scattered institutional knowledge — spread across Drive files, website copy, local documents, contracts, style notes, and our prior conversations — and produces a structured knowledge base that the main Seamless project can build on.

**SB is not an automation project.** It doesn't build workflows, connect APIs, or write production code. It reads source material, organizes what it finds, identifies gaps, and produces clean reference documents. The automation happens later, in the Seamless (SL) repo, using SB's output as its foundation.

**Why this exists:** Without SB, the Seamless project would require Claude Code to make assumptions about how Maya works — her naming conventions, her client relationships, her identity routing, her emotional relationship to task categories, her file organization logic. Those assumptions would be wrong in specific, hard-to-detect ways. SB forces the assumptions into the open where Maya can correct them before they get baked into automation.

### Relationship to Seamless (SL)

SB produces four categories of deliverables that SL consumes:

1. **Draft CLAUDE.md** — The always-loaded navigation document for SL's Claude Code sessions.
2. **Domain plans** — Deep-reference files for each automation domain. Built as skeletons during Phases 1–4, finalized in Phase 5.
3. **Knowledge layer** — Structured Markdown reference documents (conventions, identities, rhythms, clients, tools, policies).
4. **Data layer** — Machine-readable YAML/JSON configuration files that SL loads directly.

---

## 2. Repositories

**seamless-bootstrap** (`stephbairey/seamless-bootstrap`) — Private. This project.  
**seamless** (`stephbairey/seamless`) — Private. The main automation project. Empty until SB is complete.

---

## 3. Source Material

Maya populates the `sources/` directory with files from six locations. Phase 0 includes a triage step where Claude Code catalogs raw file locations before Maya decides what to copy in.

### 3a. Drive Files
From the Lingua Ink, Maya, and Maya-bak Google Drive folders. Expected contents include client contracts, style guides, project files, branding documents, pricing sheets, and organizational documents for ARC/PRG/IRG.

### 3b. Website Exports
Content from linguaink.com and bairey.com — services pages, about pages, blog posts, portfolio samples. These represent the public-facing articulation of brand identity, voice, and positioning.

### 3c. Local Documents
Contracts, plans, style notes, and other files Maya has locally that aren't in Drive. These often contain the most operationally specific information — pricing decisions, workflow documentation, client agreements.

### 3d. System Snapshots
Live configuration exports from Maya's active systems. Highest-fidelity source material for Phase 1.

**Pre-Phase Export Checklist:**

| System | Export Method | File Format | Destination |
|--------|-------------|-------------|-------------|
| Gmail filters | Gmail Settings → Filters → Export | XML | `sources/system-snapshots/gmail-filters.xml` |
| Google Calendar (linguainkmedia) | Calendar Settings → Export | .ics | `sources/system-snapshots/cal-linguaink.ics` |
| Google Calendar (stephbairey) | Calendar Settings → Export | .ics | `sources/system-snapshots/cal-steph.ics` |
| Google Calendar (mjbairey) | Calendar Settings → Export | .ics | `sources/system-snapshots/cal-mj.ics` |
| n8n workflows | n8n → Export Workflow | JSON | `sources/system-snapshots/n8n-workflows.json` |
| ClickUp custom fields | ClickUp API → Get Fields | JSON | `sources/system-snapshots/clickup-fields.json` |
| File routing matrix | Manual export from spreadsheet | CSV | `sources/system-snapshots/routing-matrix.csv` |
| WordPress configs (linguaink.com) | WP admin or export | varies | `sources/system-snapshots/wp-linguaink/` |
| WordPress configs (bairey.com) | WP admin or export | varies | `sources/system-snapshots/wp-bairey/` |

Maya completes this checklist before Phase 0 begins. Not every snapshot is needed immediately, but all must exist before Phase 1 starts.

**Sanitization requirement:** Before committing snapshots, Maya reviews each export for API keys, passwords, tokens, or private data. Redact or replace with placeholders.

### 3e. Operator Notes
Structured notes from Maya capturing knowledge that lives in her head. First-class source type, citable in fact records.

**Suggested template:**

```markdown
# Operator Note: [Topic]
**Date:** [DATE]

## Facts
- [Concrete statements about how things work]

## Examples
- [Specific instances that illustrate the facts]

## Uncertainties
- [Things Maya is unsure about or that may have changed]
```

The template is a guide, not a requirement — any format works. The key requirement is that notes are committed to the repo.

### 3f. Prior Work (Claude-produced)
Documents from our existing conversations that already contain structured analysis:

- **How Maya Works** (audit report, Feb 27 2026) — Comprehensive system analysis. Most information-dense source we have.
- **Brand inventory and office process work** from prior sessions. Multiple rich sources!
- **Let's Meet CLAUDE.md and plan.md** — Structural templates for SB's deliverables.

**Accuracy warning:** Handoff documents and audit reports from Claude conversations may contain errors, especially specific values, dates, or technical details. These are high-value starting points, not ground truth. Errors discovered during extraction go in `maya-corrections.md`.

---

## 4. What We Already Know

From the audit and our conversations, we have confirmed knowledge about Maya's systems. This is what SB starts with — everything else gets extracted from source material.

### 4a. ClickUp Architecture

**Structure:** Single workspace → Task Dashboard (space) → Master Task List (list). All tasks live in one flat list. No folders, no sublists.

**Statuses:** `not started`, `begun`, `complete`, `scratch` (deferred/someday/maybe).

**Custom Fields (all required, all dropdown):**

| Field | Options | What It Captures |
|-------|---------|-----------------|
| **Project** | Lingua Ink Books, Lingua Ink Media, Dalton Law, Lynn Haller, Tomahawk Destiny, Lingua Ink Courses, Lingua Ink Cohorts, Daniela Morescalchi, Sulima Malzin, Carolyn Martin, Maya Bairey, Personal, Raging Grannies, Free Cohort, Job Search, Devon Ervin | Which client/context a task belongs to |
| **Effort** | Tiny, Small, Medium, Big, Very Big | Cognitive/time cost |
| **Revenue** | None, Indirect, Passive, Direct Low, Direct High | Financial relationship |
| **Scope** | Internal, External | Whether the task faces outward |
| **Approach** | Dread, Reluctant, Indifferent, Interested, Excited | Maya's emotional relationship to the task |
| **Readiness** | Prepared, Upskilling | Whether Maya has the skills or needs to learn |

**Task naming conventions:**
- Action items: verb-first, lowercase ("create PRG newsletter", "rewrite about page with Devon's story")
- Meetings: proper names retained ("Maya:Devon", "Lynn:Maya", "Steph: Sulima", "HoD meeting")
- Meeting format uses colon separator, sometimes with spaces inconsistently
- Events/appointments: proper case ("Social Sauna", "Story Lounge", "Writing Cohort")

**Due dates** are essential — tasks without due dates don't appear in workflow views. Time estimates are tracked in milliseconds (e.g., 10800000 = 3 hours).

**Custom IDs:** Prefixed `LIM-` followed by sequential number (e.g., LIM-1157).

**API details for SL:**
- Workspace ID: `90132317650`
- Space ID: `90139879792`
- List ID: `901318968458`
- Custom field UUIDs documented in audit report

### 4b. Calendar Architecture

**Three calendars, one primary:**
- `linguainkmedia@gmail.com` — Primary, owner. Business calendar.
- `stephbairey@gmail.com` — Personal calendar, writer access.
- `mjbairey@gmail.com` — Additional personal, writer access.

**Recurring rhythms observed:**
- Tuesday: HoD (Hallway of Doorkbos book meeting/Lynn) meeting, 1–2pm
- Thursday: Steph:Sulima 9–10am, PRG newsletter work 10–11am, Writing Cohort noon–2pm
- Friday: Story Lounge 9–10am
- Sunday: Writing Cohort noon–2pm (with post-meeting critique rotation)
- First of quarter: Royalty reports

**Meeting naming conventions mirror ClickUp:** "Person:Person" for 1:1s, proper case for group events.

### 4c. Email Identity Routing

**Primary sending address:** `stephbairey@gmail.com`  
**Business calendar address:** `linguainkmedia@gmail.com`  
**Additional address:** `mjbairey@gmail.com`  
**Writing/artistic identity:** `maya@bairey.com`

**Routing logic (needs verification):**
- stephbairey@gmail.com — default inbox, personal/community, receives all forwards
- steph@linguaink.com — Lingua Ink Books business, publishing clients
- steph@linguainkmedia.com — Lingua Ink Media business, TDA client projects, web dev
- steph@bairey.com — personal/job search/formal/government-name contexts
- maya@bairey.com — author correspondence, writing cohort, NIWA
- maya@linguaink.com — creative director work, illustrator coordination, author clients (covers both LIB and LIM creative work since maya@linguainkmedia.com doesn't exist)
- mjbairey@gmail.com — creative personal/community, Google-login contexts
- grannynewsletter@gmail.com — PRG newsletter sends and logistics
- pdxraginggrannies@gmail.com — PRG official/external communications
- webmaster@tomahawkdestiny.com — TDA website operations
- steph.bairey.arc@tomahawkdestiny.com — personal ARC committee correspondence
- arc@tomahawkdestiny.com — ARC shared distribution list
- doorknobs@lynnahaller.com — Lynn/HoD book shared distribution
- webgranny@gmail.com — IRG work
- info@linguaink.com — Lingua Ink front-facing contact
- webgranny@bairey.com (legacy, predates inbox access to webgranny@gmail.com)
- scb.zombie@gmail.com (legacy, should retire but tied to many signups)

### 4d. File Management System

**Architecture:** Google Drive with n8n automation for deterministic file routing.

**Tag-based routing:** Files named with bracketed tags like `[Painting-Celia Cover].jpg`. The tag determines routing destination.

**Client routing targets:** MAYA, LYNN, SULIMA (other clients not yet added to process).

**Matrix spreadsheet:** Maps tags to destination folders. Configuration layer for n8n automation — avoids AI costs by using deterministic rules.

### 4e. Key Relationships and Contexts

| Person/Entity | Relationship | Context |
|---------------|-------------|---------|
| Pete | Husband | TDA board responsibilities, personal calendar items |
| Lynn Haller | Client + friend | Signed author, publishing client, cohort member |
| Sulima Malzin | Client + Mentor, 86 years old | Signed author, Weekly calls (Thu 9am), website work, writing |
| Devon Ervin | Client | not-signed Author, Website project, Making Space program |
| Daniela Morescalchi | Client | Signed author, ex-Intel colleague |
| Carolyn Martin | Client | Signed author, website work |
| Dalton Law | Client | LIM client, website work, potential Diary app partner |
| ARC/TDA | Organizational commitment | Tomahawk Destiny Association Architectural Committee, chair, board-adjacent via Pete |
| TDA | Client | Tomahawk Destiny Association, website work |
| PRG | Organizational commitment | Portland Raging Grannies, newsletter creation/distribution, website work, all tech |
| IRG | Organizational commitment | International Raging Grannies, website work |
| Writing Cohort | Community Maya runs | Thu/Sun via Zoom, critique rotation, 5–8 regular members |
| Story Lounge | Community | Friday Intel alumni meetup |

### 4f. Identity Model

**Stephanie (Steph) Bairey** — Legal/business/family name. Used for contracts, personal appointments, dentist, Pete-related items.

**Maya Bairey** — Pen name. Used for Lingua Ink, writing, artistic work, the romance blog, the writing cohort, and creative endeavors. This is the name Claude uses.

**Lingua Ink Media** — The business entity through which Maya provides creative services including SEO/website development, book publishing/marketing.

**The boundary is intentional** — not a casual preference but a considered practice of identity management that reflects Maya's therapeutic work around inhabiting herself authentically vs. arranging herself for others.

---

## 5. Phases

### Pre-Phase: System Export Checklist

Before Phase 0 begins, Maya completes the system snapshot exports listed in Section 3d (including sanitization review). This is a Maya task, not a Claude Code phase.

### Phase 0: Inventory & Setup

**Input:** Maya's raw file locations (Drive folders, local directories, website URLs) + system snapshots already in `sources/`

**Step 1 — Source triage.** Claude Code (via File Cataloger subagent) gets read-only access to Maya's raw Drive folders, local file locations, and website URLs. It produces a preliminary catalog of everything available, with one-line summaries and relevance flags. Maya reviews and decides what to copy into `sources/`.

**Step 2 — Manifest.** Once Maya has populated `sources/`, Claude Code reads every file and produces the formal manifest with: (a) current and relevant, (b) outdated or superseded, (c) can't parse or doesn't understand, (d) duplicates or near-duplicates.

**Output:** `extraction/manifest.md`  
**Review gate:** Maya reviews manifest, marks files, adds context. Claude Code does not proceed until manifest is approved.

### Phase 1: Technical Systems

**Priority:** Highest  
**Input:** Manifest-approved source files + system snapshots + audit report + prior conversations

**Extraction targets:**
- ClickUp: Full architecture, custom field definitions with option IDs, naming conventions with examples, status workflow, time tracking config, API reference
- File Management: Complete tag vocabulary, routing matrix rules, n8n workflow documentation, Drive folder structure, client-to-folder mapping
- Calendar: All three calendars with roles, recurring event inventory, naming conventions, identity-to-calendar mapping
- Email: All addresses and contexts, sending rules, signatures, forwarding, label/filter structure (from Gmail XML export)
- Hosting & Domains: linguaink.com and bairey.com hosting, DNS, SSL, WordPress configs
- Tool Integrations: Granola (including speaker attribution limitations), Zoom, n8n instance, other connected tools

**Output:** `extraction/technical-systems/` (one file per system + synthesis file + `questions.md`)

**Review gate:** Claude Code presents extraction alongside proposed output. Maya reviews in one pass.

**Minimum required review:** (1) ClickUp custom field option IDs, (2) email identity routing rules, (3) file routing matrix completeness.

**After approval, produce:**
- `output/knowledge/tools.md` and `output/knowledge/conventions.md`
- `output/data/clickup-fields.yaml`, `output/data/email-identities.yaml`, `output/data/file-routing.yaml`, `output/data/calendar-map.yaml`
- Initial structure for `output/data/client-registry.yaml` — client names and project codes from ClickUp Project dropdown. Relationship details added in Phase 2.
- Domain plan **skeletons** for clickup-automation, file-management, calendar-sync, email-triage (using template)

### Phase 2: Business Operations

**Priority:** Second  
**Input:** Manifest-approved source files + Phase 1 output

**Extraction targets:**
- Service offerings: What Lingua Ink does (website development, book publishing, typesetting, courses, cohorts — what else?)
- Pricing models: Per-service pricing, retainer structures, royalty arrangements
- Client workflows: inquiry → proposal → contract → work → delivery → follow-up
- Client onboarding: What happens when a new client comes in
- Revenue model: How the Revenue custom field maps to income streams
- Royalty/publishing pipeline: Book production, royalty reporting cadence, consignment tracking (Broadway Books)
- Organizational commitments: ARC/TDA, PRG, IRG — what Maya does, time commitment, deliverables

**Output:** `extraction/business-operations/` + `questions.md`

**Review gate:** Maya reviews. Business operations are the most likely to need information only in Maya's head.

**Minimum required review:** (1) Active vs. inactive client relationships, (2) service offerings accuracy, (3) pricing/contract details that are wrong or outdated.

**After approval, produce:**
- `output/knowledge/clients.md`
- Enrich `output/data/client-registry.yaml` with relationship types, service context, contact details
- Enrich `output/knowledge/rhythms.md`
- Domain plan **skeleton** for revenue-workflow

### Phase 3: Brand Identity

**Priority:** Third  
**Input:** Website exports + style docs + blog posts + Phase 2 output

Invoke the **Voice Analyzer subagent** during this phase for writing sample analysis.

**Extraction targets:**
- Mission and values: What Lingua Ink stands for, what Maya stands for as a writer
- Voice and tone rules: How Lingua Ink writes vs. Maya vs. Steph. Specific linguistic patterns, vocabulary preferences, what each voice avoids
- Positioning: Who Lingua Ink serves, competitive differentiation
- Visual identity: Colors, typography, logo usage, brand guidelines
- Audience definitions: Who reads the blog, who hires Lingua Ink, who joins the cohort
- "Sailor's Code" creative identity: How Maya's fiction connects to her brand

**Three-example rule:** Every voice rule must cite at least three source examples. Fewer than three → mark `[LIKELY]`.

**Output:** `extraction/brand-identity/` + `questions.md`

**Review gate:** Maya's corrections matter most here. Brand identity is deeply personal — Claude Code can observe patterns but cannot understand *why* Maya makes voice choices.

**Minimum required review:** (1) Voice distinctions between Lingua Ink, Maya, and Steph, (2) voice rules that feel wrong or oversimplified, (3) Sailor's Code framing.

**After approval, produce:**
- `output/knowledge/identities.md`
- Domain plan **skeleton** for brand-codification

### Phase 4: Content & Marketing

**Priority:** Fourth  
**Input:** Blog posts + social presence + newsletter samples + Phase 3 output

**Extraction targets:**
- Blog strategy: Platforms (bairey.com, LinkedIn), voice per platform, cadence aspirations vs. reality
- Social media: Current presence, gaps, active vs. dormant
- Newsletter: PRG newsletter workflow, personal newsletter plans, distribution tools
- Writing Cohort as marketing: How the cohort serves community and business
- Story Lounge and Story Lab: Role in Maya's professional network
- Author platform: What exists, what's planned, Lingua Ink vs. Maya Bairey connections

**Output:** `extraction/content-marketing/` + `questions.md`

**Review gate:** Maya reviews with attention to aspirational vs. operational. Flag which content activities are real priorities vs. "should-do" guilt items.

**Minimum required review:** (1) Which content activities are real priorities, (2) PRG newsletter workflow accuracy, (3) active vs. dormant platforms.

**After approval:** Update `output/knowledge/rhythms.md` with content cadences. Produce any remaining domain plan skeletons.

### Phase 5: Synthesis

**Input:** All approved Phase 1–4 output

**Step 1 — Source refresh check.** If SB has run over multiple weeks, Maya re-exports critical system snapshots (ClickUp fields, Gmail filters, calendar) and flags significant changes. If nothing changed, note it and proceed.

**Step 2 — Produce deliverables:**
- `output/seamless-claude-md-draft.md` — Draft CLAUDE.md for SL, following the Let's Meet pattern
- **Finalized domain plans** — Complete all skeletons with full instructions, cross-references, implementation-level detail. Every plan follows the template. This is the only phase where domain plans become final.
- `output/agent-designs/` — **Prototype** design documents for SL automation agents. Clearly labeled as initial designs subject to refinement.
- **Data layer cross-validation** — Verify consistency across all YAML/JSON files. Mismatches go in gaps.md.
- `extraction/fact-index.md` — Global index of all key facts across all phases with source references.
- `output/HANDOFF.md` — Transition guide for SB → SL: what SB produced, file mapping to SL locations, setup steps, known limitations.
- `output/gaps.md` — Everything unresolved.

**Step 3 — Handoff simulation.** Start a fresh Claude Code session with only SB output. Ask it to perform a simple task (e.g., "Create a new ClickUp task for a new client" or "What email address for a PRG message?"). If it flounders, that's a gap to fill.

**Review gate:** Maya reviews the complete output package. Final approval before SL work begins.

---

## 6. Review Protocol

Every phase follows this rhythm:

**Step 1 — Claude Code extracts and proposes.** Reads source material, writes to `extraction/[phase]/`. Uses fact records (see `.claude/rules/extraction-protocol.md`). Generates `questions.md` consolidating all [VERIFY] and [UNKNOWN] items. Also produces proposed output (knowledge files, data files, domain plan skeletons).

**Step 2 — Maya reviews.** Reads extraction and proposed output together. Corrects errors, fills gaps, answers questions. Records source corrections in `maya-corrections.md`.

**Step 3 — Claude Code finalizes.** Incorporates corrections, updates output, generates minimum-required-review summary for critical items.

**Step 4 — Maya approves.** Confirms critical items, approves phase. Claude Code commits, updates `current-phase.md`, starts next phase fresh.

---

## 7. Session Continuity

Auto memory is **disabled** for SB. Every session starts clean. Continuity through committed files:

- `current-phase.md` — Active phase, what was completed, what's next. Updated each session.
- `pending-questions.md` — Accumulates across sessions. Questions removed once answered.
- `maya-corrections.md` — Persistent record of known source errors. Checked every session.
- `extraction/` and `output/` directories — The sole source of truth.

---

## 8. Domain Plan Template

All domain plan skeletons follow this template. During Phases 1–4, only Purpose, Inputs, and System Overview are filled. Remaining sections completed in Phase 5.

```markdown
# Domain Plan: [DOMAIN NAME]

## Purpose
What automation this plan enables. What problem it solves.

## Inputs
Which knowledge files and data files this plan relies on.
- knowledge/[file].md — [what it provides]
- data/[file].yaml — [what it provides]

## System Overview
How the system currently works (manual process). Key workflows, decision points, exceptions.

## Automation Requirements
What the automation must do. Specific behaviors, triggers, outputs. Reference data files for exact values.

## Edge Cases & Constraints
Things to watch out for. Identity routing exceptions, client-specific overrides, seasonal variations.

## Implementation Notes
API endpoints, field UUIDs, status codes, exact values needed for code. Cross-references to data files.

Examples of required detail level per domain:
- ClickUp Automation: API endpoints, field UUIDs, status transition rules, task creation templates, naming validation
- Email Triage: Filter rules, label hierarchy, auto-reply triggers, human-in-the-loop conditions
- File Management: Tag vocabulary, folder paths, routing rules, conflict resolution for ambiguous tags
- Calendar Sync: Calendar IDs, event types, identity mapping, recurring event handling
- Brand Codification: Voice rules with examples, identity-to-context mapping, approval requirements
- Revenue Workflow: Pricing lookups, invoicing triggers, royalty calculation rules

## Open Questions
Things to be resolved during SL implementation.
```

This template is also stored as `output/domain-plans/_template.md`.

---

## 9. SB Subagents

Defined in `.claude/agents/`. See those files for full specifications.

**File Cataloger** (`.claude/agents/file-cataloger.md`) — Phase 0. Read-only librarian. Catalogs source material for triage and manifest.

**Voice Analyzer** (`.claude/agents/voice-analyzer.md`) — Phase 3 only. Read-only literary critic. Analyzes writing samples for voice patterns across Maya's three identities.

---

## 10. Key Design Decisions

These are summarized here and recorded in `decisions.md` with full rationale.

- **Extraction/output split:** Extraction is messy intermediate work; output is Maya-approved. If it's in output/, Maya signed off.
- **Knowledge layer + data layer:** Prose for humans (explains why), YAML/JSON for machines (exact values SL loads). No duplication.
- **Domain plan skeletons until Phase 5:** Prevents rewrite churn from cross-phase dependencies.
- **Agent designs are prototypes:** Initial designs refined during SL. SB extracts knowledge; SL designs automation.
- **Policies separate from conventions:** Conventions guide implementation; policies constrain it. Violating a convention is messy; violating a policy causes harm.
- **maya-corrections.md:** Source material may contain errors. Corrections are persistent, checked every session, override the source they correct.
- **Auto memory disabled:** Reproducibility over speed. All state in committed files.
- **Data cross-validation required:** Client names, email addresses, and other values must be consistent across YAML files.

---

## 11. Success Criteria

SB is complete when:

1. **Every output file has been reviewed and approved by Maya.** No drafts remain in output/.
2. **gaps.md contains only intentional deferrals** — things for SL, not things forgotten.
3. **The draft CLAUDE.md for SL is specific enough** that a fresh Claude Code session can understand what Seamless does, how Maya's systems work, what conventions to follow, what never to assume, and which plan to read.
4. **Each domain plan contains implementation-level detail** — API IDs, exact field values, specific rules. Follows the template with all sections complete.
5. **Maya can read the knowledge layer and say:** "Yes, this is how I actually work."
6. **Each data file is loadable as configuration** — parseable, complete, cross-validated for consistency.
7. **policies.md captures every automation safety boundary** — including safe experimentation boundaries for SL testing.
8. **The handoff simulation passes** — a fresh Claude Code session with only SB output can perform a simple task.

---

## 12. Open Questions for Maya

Answer before or during Phase 0:

1. **Source material completeness:** Important documents not in Drive, websites, or local? Slack messages, text conversations, verbal agreements?
2. **Historical vs. current:** How far back is "current"? Is a 2023 contract still active? A 2024 style guide?
3. **Client confidentiality:** Client details that should NOT be in the SB repo, even though it's private?
4. **Organizational scope:** How deeply to document ARC/TDA, PRG, IRG? Just Maya's role, or full organizational context?
5. **Devon project status:** Treat as client workflow case study, or too in-flux?
6. **The romance blog:** Active or dormant? Current strategy or historical?
7. **Pete's role:** How much to document vs. out of scope?
8. **n8n export:** Can the workflow config be exported? *(Pre-Phase checklist assumes yes. If not, becomes [VERIFY] in Phase 1.)*

---

## 13. Risks and Mitigations

**Source material incomplete.** `sources/operator-notes/` and system snapshots address this. Phase 0 triage catches forgotten files. Review gates catch the rest. Phase 2 most vulnerable.

**Source material contains errors.** `maya-corrections.md` captures errors persistently. Fact records force source citation for traceability. Precedence hierarchy places operator corrections above all sources.

**Extraction takes too long.** Phase 0 triage reduces volume before files enter sources/. Manifest relevance classifications let Maya skip categories.

**Assumptions cascade.** Stop-after-extraction with review prevents propagation. Fact records make assumptions traceable. `questions.md` ensures nothing is missed.

**Scope creep into automation.** CLAUDE.md Never list prohibits. SB produces documents and data, not code.

**Output too abstract.** Success criteria #4, #6, #8 require implementation detail. Domain plan template specifies required detail. Handoff simulation tests sufficiency.

**Systems change during SB.** Output structured for change — tables with addable rows, rules with examples not exhaustive catalogs. Phase 5 source refresh check catches drift.

**Domain plan rewrite churn.** Skeletons until Phase 5. Finalized only when all upstream knowledge is reviewed.

**Data files inconsistent.** Phase 5 cross-reference validation. client-registry.yaml layered across Phases 1–2 (ClickUp names in Phase 1, relationships in Phase 2) for single source of truth on client names.

**Maya can't do extensive reviews.** Minimum-required-review summaries per phase. Consolidated questions.md for efficient review.

**Snapshots contain secrets.** Pre-Phase sanitization requirement. Maya reviews before committing.

**SL has no safe testing environment.** policies.md includes safe experimentation boundaries.
