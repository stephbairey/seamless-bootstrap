# Domain Plan: Calendar Sync

## Purpose
Provide unified calendar awareness across Maya's 3 Google Calendars and integrate calendar data with other systems (ClickUp task due dates, local dashboard display, meeting prep). Replace the abandoned ClickUp-Calendar native sync with something that actually works.

## Inputs
- knowledge/conventions.md — Calendar naming rules, identity routing for invites, HoD abbreviation
- knowledge/tools.md — Calendar architecture, Granola transcription, dashboard display
- data/calendar-map.yaml — 3 calendars with identity/purpose mapping, recurring events, integration status

## System Overview
**Three calendars, unified view:**
- **linguainkmedia@gmail.com** — Business and operations. Client meetings, organizational commitments. Invites sent when contact knows Steph/Lingua Ink.
- **mjbairey@gmail.com** — Creative and writing. Writing Cohort (Sundays noon-2pm, canonical home), critique groups, publishing tasks. Invites sent when contact knows Maya.
- **stephbairey@gmail.com** — Home and personal. Household events, Pete's Alexa entries. Feeds the local dashboard. History back to 2000.

All viewed in a unified view from linguainkmedia@gmail.com. All in America/Los_Angeles timezone.

**Naming conventions:** Client meetings use `ClientName and Steph @ Lingua Ink` (formal) or `Client:Steph` (informal). Multi-person meetings use `Name:Name:Name` format.

**Current integrations:**
- ClickUp-Calendar native sync: **abandoned** (didn't work well). ✅-prefixed events on linguainkmedia calendar are legacy artifacts.
- stephbairey calendar → local dashboard: **active**. Python fetcher pulls calendar data for the household display.
- Pete adds events via Alexa → stephbairey calendar.

**Known issues:**
- Writing Cohort appears on all 3 calendars (should only be on mjbairey). Duplication is accidental, caused by email confusion over time.
- Legacy "Delivery:" events on stephbairey calendar are no longer active — Maya uses a different delivery tracking method now.

**Identity routing for invites:** Follows the two-axis model. If the contact knows Maya → mjbairey. If Steph or Lingua Ink → linguainkmedia. Relationship history can override strict role logic.
