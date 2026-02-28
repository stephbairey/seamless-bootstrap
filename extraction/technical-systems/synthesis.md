# Phase 1 Technical Systems — Synthesis

**Phase:** 1 — Technical Systems
**Date:** 2026-02-27
**Status:** DRAFT — awaiting Maya review

---

## System Architecture Overview

Maya operates a distributed technical ecosystem across six major domains. This synthesis maps the cross-system connections, identifies integration points relevant for SL automation, and flags architectural patterns.

### The Big Picture

Maya's technical systems form three concentric rings:

**Inner ring (daily operations):** Gmail → ClickUp → Google Calendar → Google Drive
These four systems are where Maya spends most of her operational time. Gmail is the "operational nervous system" — she searches it constantly to find client history, commitments, and prior communications. ClickUp is the task system where everything gets tracked. Calendar provides scheduling. Drive holds all files.

**Middle ring (automation):** n8n → TagSpaces → Google Sheets → Excel
These systems automate repetitive work. n8n is the core engine, running six active workflows (3 file sort, 2 Amazon delivery, 1 folder ID utility). TagSpaces provides the input interface for file tagging. Google Sheets stores n8n output data. Excel holds the routing matrix source of truth.

**Outer ring (publishing & content):** WordPress (3 sites + client sites) → WooCommerce → MailPoet → Substack → HeyGen → Midjourney → Later
These systems produce and distribute content. WordPress is the CMS platform for all web properties. WooCommerce handles book sales. MailPoet manages email lists. Substack is used for Sulima's Light Waves. HeyGen and Midjourney are creative tools.

### Identity Routing Is Foundational

The most important cross-cutting pattern in Maya's systems is **identity routing**. Nearly every system has a different configuration based on which identity (Steph Bairey, Maya Bairey, Lingua Ink Media, PRG, or ARC/TDA) is being used:

- **Email:** 16 Send-As addresses mapped to 5 identity contexts, routed through a single Gmail hub
- **Calendar:** 3 calendars mapped to 3 primary identities (business, creative, personal/legal)
- **WordPress:** Different admin accounts and author identities per site
- **ClickUp:** Project dropdown values encode clients and identity contexts
- **File management:** Client-specific intake folders and routing matrices

Any SL automation must understand which identity context it's operating in. This is not optional — sending from the wrong address or posting to the wrong calendar would be immediately visible and damaging.

---

## Cross-System Integration Points

### Confirmed Integrations

| From | To | Mechanism | Status |
|------|-----|-----------|--------|
| Gmail (Amazon notifications) | n8n | Label trigger (`Label_6582208580953641436`) | Active |
| n8n | Google Sheets | Delivery data append | Active |
| n8n | Google Drive | File move (routing) | Active |
| TagSpaces | Google Drive | Manual drag to intake folder | Active (manual step) |
| Excel (routing matrix) | n8n | Manual encode as code | Active (manual sync) |
| ClickUp | Google Calendar | ✅-prefixed task sync | Active |
| WordPress | MailPoet | Newsletter from posts | Active |
| WordPress (sulimamalzin.net) | Substack | Feed import via fivefilters.net | Active |

### Potential SL Integration Points

Based on the extraction, these are the highest-value automation opportunities:

1. **Email triage and routing** — Gmail filters handle the basics, but Maya manually decides which identity to respond from. SL could propose identity-appropriate draft responses.

2. **File routing matrix maintenance** — Currently manual Excel → n8n code encoding. SL could automate matrix updates when new tag pairs appear in the Unsorted folder.

3. **ClickUp task creation from email** — Maya's Gmail is her CRM; she manually creates ClickUp tasks from email commitments. SL could detect commitments and propose tasks.

4. **Calendar consolidation** — Three calendars create cognitive load. SL could provide a unified view with identity context preserved.

5. **Content publishing pipeline** — The WordPress → MailPoet → Substack chain has manual steps. SL could streamline multi-platform publishing.

6. **Royalty report automation** — KDP exports require manual wrangling into Maya's Excel template. SL could automate the data transformation.

---

## Architectural Patterns

These patterns appear consistently across Maya's systems and should inform SL design:

### 1. Graceful Degradation Over Failure

The Unsorted folder in the file routing system is the canonical example. When the system can't route a file, it catches it safely rather than failing. This pattern should be replicated in SL: when automation is uncertain, queue for human review rather than failing or guessing.

### 2. Describe-Don't-Organize

Maya's tagging philosophy: describe what a thing *is* (via tags), let the system figure out where it *goes*. This offloads cognitive cost. SL should follow this principle — ask Maya to classify intent, not destination.

### 3. Local-First, Cloud-Backed

n8n runs locally in Docker. The dashboard runs on a local mini-PC. TagSpaces is a local app. Cloud services (Gmail, Drive, Calendar) are integration targets, not primary infrastructure. SL should respect this by running locally where possible.

### 4. Persistence Over Convenience

Maya chose n8n over Cowork because n8n runs without supervision in Docker. She prefers systems that work while she sleeps. SL automations should be persistent, not session-dependent.

### 5. Systems Serve Multiple Functions

Maya's systems are partly operational and partly psychological. The Unsorted folder isn't just a catch basin — it's reassurance that nothing gets lost. ClickUp isn't just a task list — it's an external memory system. SL should not optimize away the emotional functions of these systems.

---

## Data Quality Assessment

| Source Type | Quality | Notes |
|-------------|---------|-------|
| System snapshots (JSON/XML/ICS) | HIGH | Machine-generated, precise, current |
| Operator notes (email-send-as-config.md) | HIGH | Maya's own documentation |
| Prior work handoffs | MODERATE | Good context, but [INFERRED] items need verification |
| WordPress XML exports | HIGH for structure, LOW for hosting details | Content inventory is complete; hosting/DNS details absent |

### Known Gaps in Source Coverage

1. **ClickUp status workflow** — The clickup-fields.json export only contains custom fields, not statuses, views, or list structure.
2. **Google Drive folder hierarchy** — The Google Drive ID Matrix.xlsx is binary and couldn't be fully parsed. Folder IDs are confirmed from n8n workflow code, but the full hierarchy is incomplete.
3. **Hosting infrastructure** — No direct hosting provider documentation. Nixihost inferred from SMTP servers but not confirmed.
4. **Docker container inventory** — n8n is documented; other containers (the "-arr stack" and others) are mentioned but not detailed.
5. **Zoom/Granola integration** — Both tools are confirmed in use but integration details (recording settings, transcript handling) are absent.

---

## Cross-System Conflicts and Discrepancies

- **[DISCREPANCY]** The Daily Processes handoff describes ClickUp usage as "[INFERRED] inconsistent" while the Lingua Ink handoff calls it "meticulous" with 764 tasks. These likely describe different aspects: data quality (meticulous) vs. daily workflow integration (inconsistent). Maya should clarify.

- **[DISCREPANCY]** Calendar events on the linguainkmedia business calendar include personal items (dentist, grocery). This may be intentional (all-in-one operational view) or overflow. Maya should clarify.

- **[DISCREPANCY]** Writing Cohort events appear on all three calendars. This could be deliberate (visible from any calendar view) or accidental duplication.

---

## Minimum Required Review Items (per plan.md §Phase 1)

1. **ClickUp custom field option IDs** — All 42 option IDs across 6 fields have been extracted from the system snapshot. Maya should confirm these are current and that no fields have been added since export.

2. **Email identity routing rules** — 16 Send-As identities have been documented. Maya should verify: (a) which identities are actively used, (b) the routing logic for "when do I send as X vs Y", (c) whether any identities should be retired.

3. **File routing matrix completeness** — Three client matrices (Lynn, Maya, Sulima) have been fully extracted from n8n workflows. Maya should verify: (a) are these the only three clients with routing, (b) is the Unsorted folder actually monitored, (c) what triggers matrix updates.
