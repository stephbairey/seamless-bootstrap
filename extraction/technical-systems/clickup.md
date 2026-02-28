# ClickUp System Architecture -- Extraction

Extracted: 2026-02-27
Sources: `sources/system-snapshots/clickup-fields.json` (primary), three handoff documents (secondary)
Status: DRAFT -- awaiting Maya review

---

## 1. Workspace and Hierarchy

- **Claim:** All tasks go to the "Master Task List" in the "Personal" project unless Maya specifies otherwise.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2, "Task Management: ClickUp")
- **Confidence:** CONFIRMED (stated in two independent handoff documents)
- **Impact:** Task creation automation, n8n-to-ClickUp integrations
- **Last verified:** 2026-02-27

- **Claim:** As of November 2025, Maya had 764 total tasks tracked across multiple color-coded projects.
- **Source:** `sources/prior-work/Handoff_Lingua-Ink-Project_Feb2026.md` (Section 3, "Project Management")
- **Confidence:** CONFIRMED (stated with specific number and date)
- **Impact:** Task management domain plan, scale/volume estimates
- **Last verified:** November 2025 snapshot; current count unknown

[UNKNOWN: The ClickUp workspace ID, team/space ID, and list ID for "Master Task List" are not present in any source. These are required for API-based task creation in SL automations.]

[UNKNOWN: The status workflow (what statuses exist, what transitions are allowed, what colors they use) is not present in the exported JSON or any handoff document. The `clickup-fields.json` export contains only custom field definitions, not list/status configuration.]

[UNKNOWN: Time tracking configuration details are not present in any source. The Lingua Ink handoff mentions "time tracking [is] active" but provides no specifics about how it is configured, whether it uses ClickUp native time tracking or a custom field, or what reporting Maya uses.]

---

## 2. Custom Field Architecture (Complete)

Source: `sources/system-snapshots/clickup-fields.json`
Export date: derived from `date_created` timestamps (earliest: 2025-08-29, latest: 2025-10-03)

The exported JSON contains **6 custom fields**, all of type `drop_down`, all marked `required: true`. Every field uses `sorting: "manual"` and `new_drop_down: true`. All fields have `hide_from_guests: false`.

### 2.1 Project Field

- **Claim:** The "Project" field is a required dropdown with 16 options, used to tag every task to a specific client, business line, or personal context.
- **Source:** `sources/system-snapshots/clickup-fields.json`
- **Confidence:** CONFIRMED
- **Impact:** Task filtering, revenue reporting, client workload analysis, automation routing
- **Last verified:** 2026-02-27 (system snapshot)

| Field property | Value |
|---|---|
| Field name | Project |
| Field ID | `9f921ca1-1b45-4b49-a463-a550287cc5b2` |
| Type | `drop_down` |
| Required | `true` |
| Date created | `1756483731756` (epoch ms = 2025-08-29) |

**Options (in order):**

| Order | Option name | Option ID | Color |
|---|---|---|---|
| 0 | Lingua Ink Books | `5018e8c5-0c2f-4f11-af92-d857b8e007c6` | `#800000` (maroon) |
| 1 | Lingua Ink Media | `80b8f09f-0235-49dc-9d72-a914dff7888e` | `#e50000` (red) |
| 2 | Dalton Law | `848daa77-22e1-48d1-9156-f692b966d244` | `#AF7E2E` (brown/amber) |
| 3 | Lynn Haller | `be20a38f-8990-4e37-ab2b-04a9a62c0404` | `#0231E8` (blue) |
| 4 | Tomahawk Destiny | `226fe75e-8c30-4a59-ac6c-82cf375c5e55` | `#02BCD4` (teal) |
| 5 | Lingua Ink Courses | `6b74f9c5-229f-4b67-bb10-9d3511304627` | `#FF4081` (pink) |
| 6 | Lingua Ink Cohorts | `ea7c1965-6a37-4086-9224-72db30b70203` | `#FF7FAB` (light pink) |
| 7 | Daniela Morescalchi | `633e3bc7-055b-47fe-b65b-c2950b0e596e` | `#E65100` (deep orange) |
| 8 | Sulima Malzin | `6a62e5e9-0dc5-4f5c-b11e-0fabbb917105` | `#f9d900` (yellow) |
| 9 | Carolyn Martin | `2c96fe38-9057-418c-bfec-4d60f919f0ff` | `#ff7800` (orange) |
| 10 | Maya Bairey | `d721cedf-c9b5-4375-8bcd-1201711fe58a` | `#81B1FF` (light blue) |
| 11 | Personal | `72cdbc47-5044-49a8-93f0-31c26c95e469` | `#b5bcc2` (gray) |
| 12 | Raging Grannies | `48dfc203-1c7a-4fbd-8d3b-4ef845159629` | `#bf55ec` (purple) |
| 13 | Free Cohort | `724689ff-6931-47c1-b15b-f6b27971bc88` | `#3397dd` (medium blue) |
| 14 | Job Search | `1be4ed5e-cf46-4a43-ac1e-f041836fa7ea` | `#667684` (slate gray) |
| 15 | Devon Ervin | `04b61649-4b90-4525-a8fe-7b4654baf4b6` | `#AF7E2E` (brown/amber) |

**Cross-reference notes:**
- The Project field options align with the client roster described across all three handoff documents: Dalton Law, Lynn Haller, Sulima Malzin, Carolyn Martin, Devon Ervin, Tomahawk Destiny (TDA), and Raging Grannies are all confirmed active relationships.
- Daniela Morescalchi appears in the ClickUp field but is not mentioned in any handoff document. [VERIFY: Is Daniela Morescalchi a current client? What type of work?]
- "Free Cohort" and "Lingua Ink Cohorts" are separate options. [VERIFY: What distinguishes "Free Cohort" from "Lingua Ink Cohorts" in practice?]
- Dalton Law and Devon Ervin share the same color (`#AF7E2E`). This appears to be a coincidence or oversight in the color assignment, not a grouping.

### 2.2 Effort Field

- **Claim:** The "Effort" field is a required 5-level dropdown used for task sizing.
- **Source:** `sources/system-snapshots/clickup-fields.json`
- **Confidence:** CONFIRMED
- **Impact:** Workload estimation, capacity planning, task prioritization
- **Last verified:** 2026-02-27 (system snapshot)

| Field property | Value |
|---|---|
| Field name | Effort |
| Field ID | `5db96854-9117-4857-8306-6f740ec31c3e` |
| Type | `drop_down` |
| Required | `true` |
| Date created | `1756483822484` (epoch ms = 2025-08-29) |

**Options (in order):**

| Order | Option name | Option ID | Color |
|---|---|---|---|
| 0 | Tiny | `eeb46716-6bfb-4c17-be01-fb618fb7842b` | `#FF4081` (pink) |
| 1 | Small | `91613c05-d60f-4da0-afa4-9ddbd27bb9b8` | `#7C4DFF` (deep purple) |
| 2 | Medium | `2bc84c77-3957-41a7-be7d-1a6f25f54933` | `#f900ea` (magenta) |
| 3 | Big | `853902f3-5554-43f2-8ed2-11f94e2612af` | `#9b59b6` (amethyst) |
| 4 | Very Big | `6bdba8d9-d606-4eb4-b320-231a61bc2219` | `#1bbc9c` (turquoise) |

[UNKNOWN: There are no numeric values or hour estimates associated with each effort level. If SL automations need to convert effort levels to time estimates or capacity units, Maya will need to define the mapping.]

### 2.3 Revenue Field

- **Claim:** The "Revenue" field is a required 5-level dropdown classifying the revenue impact of each task.
- **Source:** `sources/system-snapshots/clickup-fields.json`
- **Confidence:** CONFIRMED
- **Impact:** Revenue reporting, task prioritization, business operations analysis
- **Last verified:** 2026-02-27 (system snapshot)

| Field property | Value |
|---|---|
| Field name | Revenue |
| Field ID | `44470f88-d8e2-4e14-9f39-c63b30e6aede` |
| Type | `drop_down` |
| Required | `true` |
| Date created | `1756483951529` (epoch ms = 2025-08-29) |

**Options (in order):**

| Order | Option name | Option ID | Color |
|---|---|---|---|
| 0 | None | `7ab3a7e0-1fc2-4074-b353-db128d792628` | `#FF4081` (pink) |
| 1 | Indirect | `fd4654d4-843e-4e7c-b9d6-d3b34950ed30` | `#7C4DFF` (deep purple) |
| 2 | Passive | `9267bc99-c45e-45ff-abbf-578e9d2dcce6` | `#7C4DFF` (deep purple) |
| 3 | Direct, Low | `4e797c63-fc86-4e35-92cd-695fb386514e` | `#AF7E2E` (brown/amber) |
| 4 | Direct, High | `73b3ec47-f245-4f2a-bd4d-b7c29a7e4d87` | `#E65100` (deep orange) |

**Semantic notes:**
- "Indirect" and "Passive" share the same color (`#7C4DFF`), suggesting they may be conceptually close but operationally distinct.
- The progression from None through Direct, High represents an explicit revenue classification system. [VERIFY: What is the distinction between "Indirect" (e.g., marketing that leads to future revenue?) and "Passive" (e.g., royalties from published books?) in Maya's usage?]
- The revenue tagging combined with the Project field enables per-client and per-revenue-type task analysis. The Lingua Ink handoff confirms "Revenue tagging and time tracking are both active."

### 2.4 Scope Field

- **Claim:** The "Scope" field is a required binary dropdown distinguishing Internal vs. External work.
- **Source:** `sources/system-snapshots/clickup-fields.json`
- **Confidence:** CONFIRMED
- **Impact:** Workload segmentation (client work vs. business-building), capacity reporting
- **Last verified:** 2026-02-27 (system snapshot)

| Field property | Value |
|---|---|
| Field name | Scope |
| Field ID | `1e4539b4-0525-4b2e-9223-a3eef644f91f` |
| Type | `drop_down` |
| Required | `true` |
| Date created | `1762209397543` (epoch ms = 2025-10-03) |

**Options (in order):**

| Order | Option name | Option ID | Color |
|---|---|---|---|
| 0 | Internal | `b709a410-20b4-4532-8119-af25b8463d9b` | `#FF4081` (pink) |
| 1 | External | `e06f82ab-ba76-4a87-8583-0b4d54caf938` | `#7C4DFF` (deep purple) |

**Cross-reference notes:**
- This field was created approximately five weeks after the original three fields (Project, Effort, Revenue), suggesting it was added as Maya refined her system. The Scope field, Approach field, and Readiness field share the same creation date (2025-10-03), indicating a second batch of system design work.
- The Internal/External distinction aligns with the 70/30 LIM/LIB split described in the Lingua Ink handoff and the "self-marketing irony" described across handoff documents: Maya tracks how much of her work is client-facing vs. business-building.

### 2.5 Approach Field

- **Claim:** The "Approach" field is a required 5-level dropdown capturing Maya's emotional relationship to a task.
- **Source:** `sources/system-snapshots/clickup-fields.json`
- **Confidence:** CONFIRMED
- **Impact:** Task prioritization, energy management, Zeigarnik effect mitigation
- **Last verified:** 2026-02-27 (system snapshot)

| Field property | Value |
|---|---|
| Field name | Approach |
| Field ID | `b977f131-3c07-4b5d-935b-6a872c2cc0b6` |
| Type | `drop_down` |
| Required | `true` |
| Date created | `1762209964010` (epoch ms = 2025-10-03) |

**Options (in order):**

| Order | Option name | Option ID | Color |
|---|---|---|---|
| 0 | Dread | `85e692cb-1530-4248-b7e8-0d7899c2ec7e` | `#e50000` (red) |
| 1 | Reluctant | `63b001e8-f862-480b-8449-d69ad0d6f77d` | `#E65100` (deep orange) |
| 2 | Indifferent | `c5f38d05-209f-4525-9b69-e14af13552c8` | `#ff7800` (orange) |
| 3 | Interested | `f8414b5b-b7db-4c47-8144-34117a6a04e9` | `#f9d900` (yellow) |
| 4 | Excited | `9f2f98ac-4575-4b80-b909-9b111c0c2e99` | `#1bbc9c` (turquoise) |

**Structural significance:**
This field is architecturally important and reflects a deliberate system design choice. The color gradient (red through turquoise) maps emotional resistance to visual urgency. Per the CLAUDE.md glossary, Maya's task management explicitly accounts for the Zeigarnik effect (unfinished tasks creating cognitive burden). The Approach field makes the emotional cost of a task visible and filterable, enabling Maya to:
- Avoid scheduling too many "Dread" tasks on the same day
- Pair "Dread" tasks with "Excited" tasks for balance
- Identify tasks that sit undone because of emotional resistance rather than time constraints

This is not decorative metadata. It is structural to how Maya manages her energy and workload. Per CLAUDE.md: "Never flatten emotional/psychological dimensions of Maya's systems -- these are structural, not decorative."

### 2.6 Readiness Field

- **Claim:** The "Readiness" field is a required binary dropdown distinguishing tasks Maya is prepared to execute vs. tasks requiring upskilling first.
- **Source:** `sources/system-snapshots/clickup-fields.json`
- **Confidence:** CONFIRMED
- **Impact:** Task sequencing, learning/dependency tracking, capacity planning
- **Last verified:** 2026-02-27 (system snapshot)

| Field property | Value |
|---|---|
| Field name | Readiness |
| Field ID | `3b795a7d-728c-49ae-b00e-82a6dbd28431` |
| Type | `drop_down` |
| Required | `true` |
| Date created | `1762210334564` (epoch ms = 2025-10-03) |

**Options (in order):**

| Order | Option name | Option ID | Color |
|---|---|---|---|
| 0 | Prepared | `f297da50-a58f-41a3-8124-f588cf1fe6cc` | `#04A9F4` (light blue) |
| 1 | Upskilling | `331fcc23-6dae-4e34-a6d3-26f34b89d463` | `#bf55ec` (purple) |

**Cross-reference notes:**
- This is the newest field in the export (created last in the October 2025 batch).
- The Prepared/Upskilling distinction creates a dependency signal: "Upskilling" tasks cannot be completed until a learning prerequisite is met. This is relevant for automation because an "Upskilling" task should not appear in "ready to work" filtered views or be auto-scheduled into the current day.

---

## 3. Field Creation Timeline

The custom fields were created in two distinct batches, suggesting two rounds of system design:

**Batch 1 -- 2025-08-29 (initial system setup):**

| Order created | Field |
|---|---|
| 1 | Project (`1756483731756`) |
| 2 | Effort (`1756483822484`) -- 91 seconds later |
| 3 | Revenue (`1756483951529`) -- 129 seconds later |

**Batch 2 -- 2025-10-03 (system refinement, ~5 weeks later):**

| Order created | Field |
|---|---|
| 4 | Scope (`1762209397543`) |
| 5 | Approach (`1762209964010`) -- 567 seconds later |
| 6 | Readiness (`1762210334564`) -- 371 seconds later |

- **Claim:** The initial ClickUp custom field system was created on 2025-08-29 with three fields (Project, Effort, Revenue). A second batch of three fields (Scope, Approach, Readiness) was added approximately five weeks later on 2025-10-03.
- **Source:** `sources/system-snapshots/clickup-fields.json` (derived from `date_created` epoch timestamps)
- **Confidence:** CONFIRMED
- **Impact:** Understanding system maturity; Batch 2 fields reflect a more sophisticated personal management philosophy
- **Last verified:** 2026-02-27 (system snapshot)

---

## 4. Naming Conventions

- **Claim:** ClickUp task names must begin with a lowercase verb.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2)
- **Confidence:** CONFIRMED (stated as explicit convention)
- **Impact:** Task creation automation must enforce this convention; n8n or SL agents creating tasks must lowercase the first word and use a verb
- **Last verified:** 2026-02-27

- **Claim:** Due dates are mandatory on all tasks.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2)
- **Confidence:** CONFIRMED
- **Impact:** Task creation automation must always include a due date
- **Last verified:** 2026-02-27

[UNKNOWN: No example task names are provided in any source. Having 3-5 real examples of Maya's task naming convention would help SL agents generate correctly formatted task names. E.g., "review Sulima blog draft" vs. "reviewSulimaBlogDraft" vs. "review: Sulima blog draft".]

[VERIFY: Are there any other naming conventions beyond "lowercase verb first"? For example, does Maya use a specific separator, include the project name in the task title, or follow any character length limits?]

---

## 5. Usage Patterns and Behavioral Context

- **Claim:** Maya uses ClickUp as "an external brain dump more than a daily driver." She creates tasks but returns to them inconsistently. It functions as "a well-organized and filterable To Do list."
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2, marked [INFERRED] in source)
- **Confidence:** LIKELY (inference from handoff author, not Maya's direct statement)
- **Impact:** SL automation should not assume Maya checks ClickUp daily; notification/reminder systems may be needed to surface tasks
- **Last verified:** 2026-02-27

- **Claim:** Maya knows her ClickUp task data "extremely well" and uses revenue tagging and time tracking actively.
- **Source:** `sources/prior-work/Handoff_Lingua-Ink-Project_Feb2026.md` (Section 3)
- **Confidence:** CONFIRMED
- **Impact:** Revenue and time tracking data in ClickUp is maintained and trustworthy for analysis
- **Last verified:** 2026-02-27

- **Claim:** ClickUp is Maya's "source of truth" for project management. "Everything goes into ClickUp."
- **Source:** `sources/prior-work/Handoff_Lingua-Ink-Project_Feb2026.md` (Section 8, "Things You'd Tell the Next Claude")
- **Confidence:** CONFIRMED
- **Impact:** ClickUp is the canonical task system; SL automations should treat it as the single source of truth for tasks
- **Last verified:** 2026-02-27

[DISCREPANCY: The Daily Processes handoff characterizes ClickUp usage as inconsistent ("returns to them inconsistently"), while the Lingua Ink handoff characterizes it as a meticulously maintained source of truth ("used meticulously," "knows her task data extremely well"). These may describe different aspects of the same reality: Maya maintains the data carefully when creating tasks but may not use ClickUp as a daily workflow driver (i.e., she creates well-tagged tasks but does not necessarily work from the ClickUp interface day-to-day). The Daily Processes characterization is marked [INFERRED] in its source, reducing its confidence level.]

---

## 6. ClickUp in the Broader Tool Ecosystem

- **Claim:** Maya's operational systems are scattered across ClickUp, n8n, Gmail, and various calendars. She has expressed wanting to consolidate but has not yet done so.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 5)
- **Confidence:** CONFIRMED (Maya's direct quote cited)
- **Impact:** SL integration architecture; ClickUp cannot be assumed to be the only task-related system
- **Last verified:** 2026-02-27

- **Claim:** Maya creates tasks in the "Master Task List" within the Personal project. Required custom fields for every task: Project, Effort, Revenue, Scope, Approach, Readiness. Due dates are mandatory.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` (Section 2), confirmed by `sources/system-snapshots/clickup-fields.json` (all six fields have `required: true`)
- **Confidence:** CONFIRMED (cross-validated between handoff narrative and system snapshot)
- **Impact:** Task creation API calls must populate all six custom fields plus a due date, or the task will fail validation
- **Last verified:** 2026-02-27

---

## 7. API References and Technical IDs

### Custom Field IDs (Complete)

| Field name | Field ID |
|---|---|
| Scope | `1e4539b4-0525-4b2e-9223-a3eef644f91f` |
| Readiness | `3b795a7d-728c-49ae-b00e-82a6dbd28431` |
| Revenue | `44470f88-d8e2-4e14-9f39-c63b30e6aede` |
| Effort | `5db96854-9117-4857-8306-6f740ec31c3e` |
| Project | `9f921ca1-1b45-4b49-a463-a550287cc5b2` |
| Approach | `b977f131-3c07-4b5d-935b-6a872c2cc0b6` |

### All Option IDs (Complete Reference)

**Project options:**

| Option name | Option ID |
|---|---|
| Lingua Ink Books | `5018e8c5-0c2f-4f11-af92-d857b8e007c6` |
| Lingua Ink Media | `80b8f09f-0235-49dc-9d72-a914dff7888e` |
| Dalton Law | `848daa77-22e1-48d1-9156-f692b966d244` |
| Lynn Haller | `be20a38f-8990-4e37-ab2b-04a9a62c0404` |
| Tomahawk Destiny | `226fe75e-8c30-4a59-ac6c-82cf375c5e55` |
| Lingua Ink Courses | `6b74f9c5-229f-4b67-bb10-9d3511304627` |
| Lingua Ink Cohorts | `ea7c1965-6a37-4086-9224-72db30b70203` |
| Daniela Morescalchi | `633e3bc7-055b-47fe-b65b-c2950b0e596e` |
| Sulima Malzin | `6a62e5e9-0dc5-4f5c-b11e-0fabbb917105` |
| Carolyn Martin | `2c96fe38-9057-418c-bfec-4d60f919f0ff` |
| Maya Bairey | `d721cedf-c9b5-4375-8bcd-1201711fe58a` |
| Personal | `72cdbc47-5044-49a8-93f0-31c26c95e469` |
| Raging Grannies | `48dfc203-1c7a-4fbd-8d3b-4ef845159629` |
| Free Cohort | `724689ff-6931-47c1-b15b-f6b27971bc88` |
| Job Search | `1be4ed5e-cf46-4a43-ac1e-f041836fa7ea` |
| Devon Ervin | `04b61649-4b90-4525-a8fe-7b4654baf4b6` |

**Effort options:**

| Option name | Option ID |
|---|---|
| Tiny | `eeb46716-6bfb-4c17-be01-fb618fb7842b` |
| Small | `91613c05-d60f-4da0-afa4-9ddbd27bb9b8` |
| Medium | `2bc84c77-3957-41a7-be7d-1a6f25f54933` |
| Big | `853902f3-5554-43f2-8ed2-11f94e2612af` |
| Very Big | `6bdba8d9-d606-4eb4-b320-231a61bc2219` |

**Revenue options:**

| Option name | Option ID |
|---|---|
| None | `7ab3a7e0-1fc2-4074-b353-db128d792628` |
| Indirect | `fd4654d4-843e-4e7c-b9d6-d3b34950ed30` |
| Passive | `9267bc99-c45e-45ff-abbf-578e9d2dcce6` |
| Direct, Low | `4e797c63-fc86-4e35-92cd-695fb386514e` |
| Direct, High | `73b3ec47-f245-4f2a-bd4d-b7c29a7e4d87` |

**Scope options:**

| Option name | Option ID |
|---|---|
| Internal | `b709a410-20b4-4532-8119-af25b8463d9b` |
| External | `e06f82ab-ba76-4a87-8583-0b4d54caf938` |

**Approach options:**

| Option name | Option ID |
|---|---|
| Dread | `85e692cb-1530-4248-b7e8-0d7899c2ec7e` |
| Reluctant | `63b001e8-f862-480b-8449-d69ad0d6f77d` |
| Indifferent | `c5f38d05-209f-4525-9b69-e14af13552c8` |
| Interested | `f8414b5b-b7db-4c47-8144-34117a6a04e9` |
| Excited | `9f2f98ac-4575-4b80-b909-9b111c0c2e99` |

**Readiness options:**

| Option name | Option ID |
|---|---|
| Prepared | `f297da50-a58f-41a3-8124-f588cf1fe6cc` |
| Upskilling | `331fcc23-6dae-4e34-a6d3-26f34b89d463` |

---

## 8. Gaps and Missing Data

This section consolidates all [UNKNOWN] and [VERIFY] items for Maya review.

### Missing from sources (UNKNOWN)

1. **Workspace/Team/Space/List IDs** -- The `clickup-fields.json` export contains custom field definitions only. The ClickUp workspace ID, team ID, space ID, and the list ID for "Master Task List" are not present. These are required for any API-based task creation or querying. [UNKNOWN: ClickUp workspace hierarchy IDs are needed for SL automation. Can Maya export these from ClickUp settings or the API?]

2. **Status workflow** -- No status definitions (e.g., "To Do," "In Progress," "Complete") appear in any source. Statuses are configured at the list or space level in ClickUp, not as custom fields, which explains their absence from the custom fields export. [UNKNOWN: What statuses exist on the Master Task List? What is the transition workflow? Are there different statuses on different lists/spaces?]

3. **Time tracking configuration** -- The Lingua Ink handoff confirms time tracking is active, but no details about configuration (native ClickUp time tracking vs. custom field, reporting intervals, billable/non-billable distinction) appear in any source. [UNKNOWN: How is time tracking configured? Native ClickUp feature or third-party integration? Is there a billable/non-billable distinction?]

4. **Effort-to-hours mapping** -- The Effort field has five levels (Tiny through Very Big) but no numeric time values are associated. [UNKNOWN: Does Maya have an approximate hours mapping for each effort level? E.g., Tiny = <15 min, Small = 15-60 min, etc.?]

5. **Task naming examples** -- The lowercase-verb convention is confirmed, but no real task name examples exist in any source. [UNKNOWN: 3-5 example task names from Maya's actual ClickUp would help validate the naming convention for SL automation.]

6. **Views and filters** -- No information about saved views, filters, or dashboards Maya uses in ClickUp. [UNKNOWN: Does Maya have saved views or filters in ClickUp? Which ones does she use most frequently?]

7. **ClickUp API token** -- No API key or authentication method is documented. This is appropriate (sensitive data should not be in source files), but SL will need it. [UNKNOWN: Does Maya have a ClickUp API token configured? Will SL need its own token?]

### Questions for Maya (VERIFY)

1. **Daniela Morescalchi** -- Appears as a Project option in ClickUp but is not mentioned in any handoff document. Is Daniela a current client? What type of work? (Section 2.1)

2. **Free Cohort vs. Lingua Ink Cohorts** -- Both appear as separate Project options. What distinguishes them in practice? (Section 2.1)

3. **Indirect vs. Passive revenue** -- Both exist as Revenue options. What is the operational distinction? Is "Indirect" something like marketing effort that leads to future revenue, while "Passive" is something like ongoing book royalties? (Section 2.3)

4. **Task naming conventions beyond lowercase verb** -- Are there additional conventions (separators, project name inclusion, length limits)? (Section 4)

5. **ClickUp usage pattern** -- Two handoff documents give slightly different characterizations of how actively Maya works from ClickUp day-to-day. Is ClickUp primarily for task capture and periodic review, or is it an active daily work driver? (Section 5)

---

## 9. Source Inventory

| Source file | Type | Role in extraction |
|---|---|---|
| `sources/system-snapshots/clickup-fields.json` | System snapshot | PRIMARY. All custom field definitions, IDs, option IDs, types. |
| `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` | Prior work (Claude-produced) | ClickUp usage patterns, naming conventions, required fields list, behavioral context. |
| `sources/prior-work/Handoff_Lingua-Ink-Project_Feb2026.md` | Prior work (Claude-produced) | Task count (764), revenue tagging confirmation, "source of truth" characterization. |
| `sources/prior-work/Handoff_ClaudeCode_2026-02-27.md` | Prior work (Claude-produced) | No direct ClickUp content; dev environment context only. |
| `maya-corrections.md` | Corrections file | No corrections recorded as of 2026-02-27. |
