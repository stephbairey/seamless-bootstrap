# Maya Corrections

Persistent record of known errors in source material. Claude Code checks this file at the start of every session. Corrections override the source they correct.

## Correction 2026-02-27: ClickUp usage characterization
**Source with error:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §2
**What it says:** "[INFERRED] She uses ClickUp as an external brain dump more than a daily driver. She doesn't seem to work from it fluidly — she creates tasks, but returns to them inconsistently."
**What's actually true:** Maya uses ClickUp almost daily. The only inconsistency is sometimes letting a few days pass before marking items completed. Data entry (764 tasks, revenue tagging, time tracking) is meticulous.
**Discovered during:** Phase 1 review

## Correction 2026-02-27: ClickUp-Calendar sync status
**Source with error:** `extraction/technical-systems/calendar.md` — ClickUp-Calendar Integration section
**What it says:** Implies ClickUp-to-Calendar sync is active (✅-prefixed events documented as current)
**What's actually true:** ClickUp's native calendar sync was abandoned because it didn't work well. The ✅-prefixed events are legacy artifacts.
**Discovered during:** Phase 1 review

## Correction 2026-02-27: "Delivery:" calendar events
**Source with error:** `extraction/technical-systems/calendar.md` — stephbairey recurring events
**What it says:** Documents "Delivery:" events as ongoing/active on the stephbairey calendar
**What's actually true:** These are legacy. Maya has a new delivery tracking method and no longer puts deliveries on the calendar.
**Discovered during:** Phase 1 review

## Correction 2026-02-27: Writing Cohort calendar duplication
**Source with error:** `extraction/technical-systems/calendar.md`
**What it says:** Notes Writing Cohort appearing on all three calendars as a pattern to verify
**What's actually true:** Writing Cohort should only be on mjbairey. Duplication is accidental, caused by email confusion from other people over time.
**Discovered during:** Phase 1 review

## Correction 2026-02-27: WordPress dual accounts on linguaink.com
**Source with error:** `extraction/technical-systems/hosting-domains.md`
**What it says:** Flags two WordPress accounts (maya + Maya Editor) as possible legacy artifact
**What's actually true:** Intentional. "Maya Editor" authors Lingua Ink editorial/publishing posts. "maya" is the account used when bairey.com blog posts auto-duplicate to linguaink.com. Different authorship contexts.
**Discovered during:** Phase 1 review

<!-- Format for new corrections:

## Correction [DATE]: [Brief description]
**Source with error:** [file path or document name]
**What it says:** [the incorrect information]
**What's actually true:** [the correct information]
**Discovered during:** [Phase N review]

-->
