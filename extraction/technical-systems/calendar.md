# Calendar System Extraction

**Phase:** 1 — Technical Systems
**Sources:** `sources/system-snapshots/linguainkmedia@gmail.com.ics`, `sources/system-snapshots/mjbairey@gmail.com.ics`, `sources/system-snapshots/stephbairey@gmail.com.ics`, `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`
**Extracted:** 2026-02-27

---

## Calendar Architecture

Maya uses three Google Calendars, each tied to a distinct email identity. All three are set to **America/Los_Angeles** timezone (Pacific Time). The stephbairey calendar also contains historical timezone entries for America/Denver and America/Phoenix (from Maya's Intel era).

### Calendar 1: linguainkmedia@gmail.com (Business/Operations)

- **Claim:** The linguainkmedia@gmail.com calendar is the primary operational calendar for Lingua Ink Media business activities.
- **Source:** `sources/system-snapshots/linguainkmedia@gmail.com.ics`
- **Confidence:** CONFIRMED
- **Impact:** calendar-sync, email-triage
- **Last verified:** 2026-02-28 (export date)

**Content profile:** Client meetings, organizational commitments (ARC, PRG, TDA), business operations (royalty reports, blog tasks), writing cohort sessions, and ClickUp-synced tasks.

**Naming conventions observed:**
- Client meetings use format `ClientName and Steph @ Lingua Ink` (e.g., "Devon Ervin and Steph @ Lingua Ink", "Jennifer Lashua and Steph @ Lingua Ink", "Kate Brinkley and Steph @ Lingua Ink")
- Informal client touchpoints use `Client:Steph` format (e.g., "Daniela:Steph", "Rapha:Steph", "Steph:Lavinia")
- Multi-person meetings use `Name:Name:Name` format (e.g., "Eve:Lynn:Maya", "Lynn:Frank:Maya")
- ClickUp-synced tasks have `✅` prefix and ClickUp task ID suffix (e.g., "✅ Sync calendar [Lingua Ink Media] - 86abecu9t", "✅ Writing Cohort [Maya Bairey] - 86abha4bw")
- Personal items tagged with `[Personal]` suffix (e.g., "✅ make dentist appointment [Personal] - 86abcqf77")
- Project items tagged with `[Project Name]` suffix (e.g., "✅ review Evan's funnel [Job Search] - 86abcqc3w")

**Notable leakage:** Some personal events (Dentist, Grocery run, Cook dinner, Clean house) appear on this business calendar. [VERIFY: Is this intentional, or should personal events only be on stephbairey?]

### Calendar 2: mjbairey@gmail.com (Personal/Writing/Author)

- **Claim:** The mjbairey@gmail.com calendar serves Maya's personal, creative, and author-platform activities.
- **Source:** `sources/system-snapshots/mjbairey@gmail.com.ics`
- **Confidence:** CONFIRMED
- **Impact:** calendar-sync, content-marketing
- **Last verified:** 2026-02-28 (export date)

**Content profile:** Writing activities (cohort, critique groups), book publishing tasks (KDP, Amazon, book awards), social media tasks, personal social events, travel.

**Naming conventions observed:**
- Writing group events: "Writing Cohort", "Writing Group", "Monday Critique Group", "Tuesday Critique Group", "Willamette Writers Critique Group: Winter Mist"
- Publishing tasks: action-oriented names like "Upload Paperback", "Apply to Book Awards", "Create a Media Kit", "Set Up Your Author Page"
- Social media tasks: "Post to Socials", "Send Newsletter Blast", "Promote Newsletter Sign Ups", "Kindle Sale Post"
- Watch parties/social: plain descriptive names ("Hamilton Watch Party", "Les Mis Watch Party")

### Calendar 3: stephbairey@gmail.com (Legal Identity/Historical/Personal)

- **Claim:** The stephbairey@gmail.com calendar is the oldest and largest calendar, containing Maya's full life history including Intel career, personal finance, family milestones, and current daily life.
- **Source:** `sources/system-snapshots/stephbairey@gmail.com.ics`
- **Confidence:** CONFIRMED
- **Impact:** calendar-sync (low priority for automation — mostly archival)
- **Last verified:** 2026-02-28 (export date)

**Content profile:** Intel corporate meetings (historical), personal finance (bills, paychecks with amounts), Amazon delivery tracking, family milestones (anniversaries, birthdays), medical appointments, current organizational work (ARC, PRG, TDA), and embedded to-do lists.

**Naming conventions observed:**
- Intel-era: "1:1 Name/Name" format (e.g., "1:1 Danika/Steph", "1:1 Steph & Tricia")
- Financial items include dollar amounts: "Capital One ($1,030)", "Paycheck ($2,875)", "Google Fi ($49) paid"
- Amazon deliveries: "Delivery: ItemDescription" (e.g., "Delivery: Cat flap", "Delivery: Vitamin D")
- To-do items: "To Do] TaskDescription" format (note: single bracket) (e.g., "To Do] Cat box", "To Do] laundry")
- Personal appointments: "Steph: Provider/Activity" (e.g., "Steph: Dentist", "Steph: Therapy", "Steph: PSU")
- Relationship milestones: "Nth Hook up Anniversary", "Nth Marriage anniversary"
- "PETERDAY" — appears as a recurring event name
- Work blocks: "Do Not Schedule: WORK", "Steph Off Work", "HEADS DOWN"

**Size note:** This is by far the largest calendar (~5.6MB). Contains events dating back to at least 2000 (yearly anniversary recurrences). Most of the historical Intel content (2012–2024) is archival.

[VERIFY: Is the stephbairey calendar still actively used for new events, or has operational activity moved to linguainkmedia?]

---

## Identity-to-Calendar Mapping

| Identity | Calendar | Primary Use |
|----------|----------|-------------|
| Lingua Ink Media (business) | linguainkmedia@gmail.com | Client meetings, business operations, org commitments |
| Maya Bairey (creative/author) | mjbairey@gmail.com | Writing groups, publishing tasks, social media, personal |
| Steph Bairey (legal/personal) | stephbairey@gmail.com | Financial tracking, medical, Intel history, family milestones |

- **Claim:** ClickUp task sync pushes tasks to the linguainkmedia calendar, not to the others.
- **Source:** `sources/system-snapshots/linguainkmedia@gmail.com.ics` (✅-prefixed events with ClickUp IDs)
- **Confidence:** CONFIRMED
- **Impact:** clickup-automation, calendar-sync

- **Claim:** Writing Cohort events appear on at least two calendars (linguainkmedia and mjbairey), suggesting cross-calendar visibility or duplicate entry.
- **Source:** All three .ics files
- **Confidence:** CONFIRMED
- **Impact:** calendar-sync (deduplication)

[VERIFY: Are all three calendars visible in a single Google Calendar view, or does Maya switch between them?]

---

## Recurring Event Inventory

### linguainkmedia@gmail.com — Active/Recent Recurring Events

| Event | Frequency | Day/Time | Status |
|-------|-----------|----------|--------|
| create PRG newsletter | Monthly, 3rd Sunday | Sun 10:00–11:00 | Active (series continues through 2026) |
| Royalty reports | Monthly, 1st of month | 1st 09:00–10:00 | Active (EXDATE for Jan 1 2026) |
| Writing Cohort / Entreprenuer Cohort | Weekly, Sundays | Sun 12:00–14:00 | Active (rolling series, latest through March 2026) |
| HoD meeting series | Weekly, Thursdays | Thu 13:00–15:00 | Active (rolling series through 2026) |
| Story Lounge | Weekly, Tuesdays | Tue 13:00–14:00 | Active |
| Raging Grannies Monthly Meeting / PRG meeting | Monthly, 3rd Saturday | Sat 09:30–11:30 | Active through Nov 2025, then continued as 3rd Sunday |
| Second Sunday | Monthly, 3rd Sunday | Sun 10:00–11:00 | Active |
| Devon Ervin and Steph @ Lingua Ink | Weekly, Thursdays | Thu 10:00–11:00 | Active |
| PRG Gender Equity meeting | Bi-weekly, Mondays | Mon 15:00–16:00 | Active through Dec 2025 |
| Blocked time | Weekly | Varies | Recurring |
| Steph: Sulima | Weekly | Varies | Recurring |
| Daniela:Steph | Weekly, Thursdays | Thu | Recurring |

### mjbairey@gmail.com — Active/Recent Recurring Events

| Event | Frequency | Day/Time | Status |
|-------|-----------|----------|--------|
| Writing Cohort | Weekly, Sundays | Sun 12:00–14:00 | Active (rolling series) |
| Writing Group / Critique Group | Weekly, Thursdays | Thu 13:00–15:00 | Active (rolling series) |
| Monday Critique Group | Weekly, Mondays | Mon | Active |
| Tuesday Critique Group | Weekly, Tuesdays | Tue | Active |
| Lynn | Weekly, Thursdays | Thu 13:00–15:00 | Active |
| Sal Zoom | Periodic | Varies | Observed |

### stephbairey@gmail.com — Current Recurring Events (excluding historical Intel)

| Event | Frequency | Day/Time | Status |
|-------|-----------|----------|--------|
| Writing Cohort | Weekly, Sundays | Sun 12:00–14:00 | Active |
| Story Lounge | Periodic | Varies | Observed |
| PRG meeting | Monthly | Varies | Active |
| ARC / ARC Meeting | Monthly | Varies | Active |
| TDA Board Meeting | Periodic | Varies | Active |
| Gender equity meeting | Monthly | Varies | Active |
| Send PRG Newsletter | Monthly | Varies | Active |
| Amazon delivery tracking | Event-driven | Varies | Ongoing (automated from Gmail) |

[UNKNOWN: What system creates the "Delivery:" events on the stephbairey calendar? They appear to be auto-generated from Amazon shipping notifications. Is this a native Gmail/Calendar integration or an n8n workflow?]

---

## ClickUp-Calendar Integration

- **Claim:** ClickUp tasks sync to the linguainkmedia Google Calendar with a specific format: `✅ task name [Project Name] - clickup_task_id`
- **Source:** `sources/system-snapshots/linguainkmedia@gmail.com.ics`
- **Confidence:** CONFIRMED
- **Impact:** clickup-automation, calendar-sync

Observed synced tasks:
- `✅ Sync calendar [Lingua Ink Media] - 86abecu9t`
- `✅ Writing Cohort [Maya Bairey] - 86abha4bw`
- `✅ post romance blog [Maya Bairey] - 86abd1f4f`
- `✅ review Evan's funnel [Job Search] - 86abcqc3w`
- `✅ schedule artery scan, OHSU [Personal] - 86abcqdjk`
- `✅ make dentist appointment [Personal] - 86abcqf77`
- `Reschedule Granny party [Personal] - 86abcqf5v`

The task ID format appears to be alphanumeric, 9 characters (e.g., `86abcqf77`, `86abecu9t`).

[VERIFY: Is ClickUp-to-Calendar sync native (ClickUp's built-in Google Calendar integration) or via n8n?]
[VERIFY: Do the bracketed project names in calendar entries match ClickUp's "Project" custom field values exactly?]

---

## Calendar Usage Patterns

- **Claim:** Maya uses the linguainkmedia calendar as her active operational calendar. Client meetings, business deadlines, and ClickUp synced tasks all land here.
- **Source:** `sources/system-snapshots/linguainkmedia@gmail.com.ics`, `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`
- **Confidence:** LIKELY
- **Impact:** calendar-sync

- **Claim:** The mjbairey calendar is used for writing/creative community activities that are separate from the Lingua Ink business identity.
- **Source:** `sources/system-snapshots/mjbairey@gmail.com.ics`
- **Confidence:** LIKELY
- **Impact:** calendar-sync, brand-codification

- **Claim:** The stephbairey calendar is the "everything else" calendar — personal life, finance, medical, family. It was likely the primary calendar during Maya's Intel career and now serves as the personal/historical layer beneath the business and creative calendars.
- **Source:** `sources/system-snapshots/stephbairey@gmail.com.ics`
- **Confidence:** LIKELY
- **Impact:** calendar-sync (low priority for SL automation)

- **Claim:** Maya described her process system as feeling "scattered across ClickUp, n8n, Gmail, various calendars, etc." The three-calendar split contributes to this feeling.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §5
- **Confidence:** CONFIRMED
- **Impact:** calendar-sync (consolidation opportunity)

---

## Client Meeting Patterns (from linguainkmedia calendar)

Active client relationships with calendar entries:
- **Devon Ervin** — Weekly Thursday meetings (10:00–11:00)
- **Daniela Morescalchi** — Regular meetings, "Daniela:Steph" format
- **Lynn Haller** — Appears on both linguainkmedia and mjbairey calendars
- **Sulima** — "Steph: Sulima", "Steph/Sulima zoom", "Sulima tech support"
- **Nicole** — "Nicole/Steph, Web Work"
- **Kate Brinkley** — "Kate Brinkley and Steph @ Lingua Ink"
- **Lila MacLellan** — "Lila MacLellan and Steph @ Lingua Ink"
- **Minea Moore** — "Minea Moore and Steph @ Lingua Ink"
- **Jennifer Lashua** — "Jennifer Lashua and Steph @ Lingua Ink"
- **Pat** — "Pat and Steph: 52 Wineries book"
- **HoD** (Harbor of Dreams?) — Weekly Thursday meetings, also with illustrator

[UNKNOWN: What does "HoD" stand for? It appears as both "HoD meeting" and "HoD Storyboarding" and "HoD meeting with Illustrator and Steph @ Lingua Ink".]

---

## Organizational Commitments (from calendar data)

| Organization | Events on Calendar | Frequency |
|---|---|---|
| ARC (Tomahawk Destiny Association) | ARC Meeting (In Person), ARC Meeting (Zoom) | Monthly |
| PRG (Portland Raging Grannies) | create PRG newsletter, PRG Gender Equity meeting, Raging Grannies Monthly Meeting | Monthly newsletter, monthly meeting |
| TDA | TDA Online Payments - Sync, TDA Website - Launch Sync | Periodic |
| Story Lounge | Story Lounge | Weekly |
| Writing Cohort | Writing Cohort, Entreprenuer Cohort | Weekly |
| Startup Coach | Startup Coach | Periodic |
| Food for Thought | Food for Thought lunch | Periodic |

---

## Gaps and Questions

[VERIFY: Are all three calendars visible simultaneously in Maya's Google Calendar view, or does she toggle between them?]

[VERIFY: Is ClickUp-to-Calendar sync native or through n8n? The ✅-prefixed events suggest a ClickUp native integration.]

[VERIFY: What does "HoD" stand for? (Harbor of Dreams? A client project?)]

[VERIFY: Is the stephbairey calendar still used for new events, or is it purely historical?]

[UNKNOWN: What system generates the "Delivery:" events on the stephbairey calendar? These appear auto-generated from Amazon notifications.]

[UNKNOWN: Is there a fourth calendar or shared calendar (e.g., for Pete/family) that doesn't appear in these exports?]

[VERIFY: The Writing Cohort appears on all three calendars. Is this intentional duplication, or should it only be on one calendar?]

[DISCREPANCY: Some events use "Steph" in the name on the linguainkmedia business calendar (e.g., "Devon Ervin and Steph @ Lingua Ink"). This suggests clients know Maya as "Steph" professionally through Lingua Ink. Consistent with identity routing rules.]
