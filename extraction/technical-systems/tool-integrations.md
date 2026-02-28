# Tool Integrations Extraction

**Phase:** 1 — Technical Systems
**Sources:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md`, `sources/prior-work/Handoff_ClaudeCode_2026-02-27.md`, `sources/prior-work/handoff-local-dashboard.md`, `sources/prior-work/Handoff-PRG-Newsletter-Project-2026-02-27.md`, `sources/prior-work/handoff-Sulima-project-feb2026.md`, `sources/prior-work/Handoff_Lingua-Ink-Project_Feb2026.md`
**Extracted:** 2026-02-27

---

## Complete Tool Inventory

### Primary Automation & Infrastructure

#### n8n (Core Automation Engine)
- **Claim:** Maya runs n8n locally via Docker as her core automation engine.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** file-management, email-triage, all automation domains
- **Last verified:** 2026-02-27

Details:
- Runs as Docker container on local machine
- Primary use: file routing (TagSpaces → Google Drive → n8n matrix lookup → folder)
- Secondary use: Amazon delivery tracking (two workflows → Google Sheets)
- Also: Google Folder ID lookup workflow, client-specific sort workflows
- Operates without supervision — Maya chose n8n over Cowork specifically for persistence/autonomy
- [See `extraction/technical-systems/file-management.md` for detailed n8n workflow documentation]

#### Docker
- **Claim:** Maya uses Docker for container management of self-hosted services, including n8n and others.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** all automation domains (infrastructure)

[UNKNOWN: What other Docker containers does Maya run besides n8n? The -arr stack is mentioned but not detailed.]

#### TagSpaces
- **Claim:** Maya uses TagSpaces for local file tagging via bracketed filename tags.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §2
- **Confidence:** CONFIRMED
- **Impact:** file-management

Tag format: Up to three bracketed tags appended to filenames (e.g., `[Cover]`, `[Newsletter]`, `[Copy]`, `[Asset]`, `[Source]`, `[Painting-Celia]`). Tags are embedded in filenames, not metadata, so they're visible everywhere.

#### Google Drive
- **Claim:** Google Drive serves as both file storage and intake pipeline for the n8n routing system.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §2
- **Confidence:** CONFIRMED
- **Impact:** file-management

Client-specific intake folders (e.g., `/MAYA`, `/SULIMA`) provide client context; n8n watches for new files in these folders.

#### Google Sheets
- **Claim:** Google Sheets serves as a data store for n8n output, including the delivery tracking dashboard.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** file-management, revenue-workflow

### Task & Project Management

#### ClickUp
- **Claim:** ClickUp is Maya's task management system. All tasks go to "Master Task List" in the Personal project.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §2
- **Confidence:** CONFIRMED
- **Impact:** clickup-automation

Master Task List ID: `901318968458`
[See `extraction/technical-systems/clickup.md` for detailed ClickUp documentation]

#### Airtable
- **Claim:** Maya uses Airtable for ARC (moorage committee) workflow management.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** low priority for SL automation (organizational, not business)

[UNKNOWN: What specific Airtable workflows does Maya use for ARC? Base structure, tables, automations?]

### Communication

#### Gmail
- **Claim:** Gmail is Maya's "operational nervous system" — she searches it constantly to reconstruct history, locate commitments, and find prior explanations to clients.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §2
- **Confidence:** CONFIRMED
- **Impact:** email-triage

Hub account: stephbairey@gmail.com (16 Send-As identities configured)
[See `extraction/technical-systems/email.md` for detailed email documentation]

#### gaggle.email
- **Claim:** Maya uses gaggle.email for PRG group email distribution (grannynewsletter@gaggle.email, pdxraginggrannies@gaggle.email).
- **Source:** `sources/prior-work/Handoff-PRG-Newsletter-Project-2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** email-triage (low priority for SL)

### Content & Publishing

#### WordPress + WooCommerce
- **Claim:** WordPress is Maya's primary CMS platform for client work and her own sites. WooCommerce handles book sales on linguaink.com.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3, WordPress export files
- **Confidence:** CONFIRMED
- **Impact:** hosting, revenue-workflow

[See `extraction/technical-systems/hosting-domains.md` for detailed site inventory]

#### MailPoet
- **Claim:** Maya uses MailPoet (a WordPress plugin) for email list management with approximately 600 subscribers.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3, `sources/prior-work/Handoff_Lingua-Ink-Project_Feb2026.md` §3
- **Confidence:** CONFIRMED
- **Impact:** content-marketing, email-triage

[VERIFY: Is the ~600 subscriber number for the Lingua Ink Books newsletter specifically, or across all MailPoet lists?]

#### Substack
- **Claim:** Maya uses Substack for client publishing, specifically Sulima Malzin's Light Waves content at sulima.substack.com.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3, `sources/prior-work/handoff-Sulima-project-feb2026.md` §3
- **Confidence:** CONFIRMED
- **Impact:** content-marketing

Import method: Settings → Import posts, using a Full-Text RSS feed URL from fivefilters.net.

[VERIFY: Does Maya use Substack for any other purposes beyond Sulima's content?]

#### KDP + IngramSpark
- **Claim:** Maya uses Amazon KDP and IngramSpark for book publishing distribution.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** revenue-workflow

[UNKNOWN: Specific KDP account details, IngramSpark account details, distribution split between the two.]

### Analytics & SEO

#### GA4 (Google Analytics 4)
- **Claim:** Maya uses GA4 for analytics across multiple sites under a single "Bairey Web" account (ID 296827458).
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** content-marketing

Property IDs: bairey.com (420399644), linguaink.com (481632955), sulimamalzin.net (420435585), lynnahaller.com (520632482).

#### Ahrefs
- **Claim:** Maya uses Ahrefs for SEO analysis, but API access is non-functional due to free tier limitation.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** content-marketing (currently limited)

### Video & Media

#### HeyGen
- **Claim:** Maya uses HeyGen for AI avatar generation for the "Writing with Maya" YouTube channel.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** content-marketing

[VERIFY: Is the "Writing with Maya" channel active and producing content, or still in planning/early stages?]

#### Midjourney
- **Claim:** Maya uses Midjourney for visual asset creation.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** brand-codification, content-marketing

#### Wondershare Filmora
- **Claim:** Maya uses Wondershare Filmora for video editing.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** content-marketing

### Social Media

#### Later
- **Claim:** Maya uses Later for social media scheduling.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** content-marketing

[UNKNOWN: Which social media platforms does Maya post to via Later? Instagram, Facebook, LinkedIn, others?]

### Transcription & Meetings

#### Granola
- **Claim:** Maya uses Granola for meeting transcription. Tested with Pete using a single-mic setup.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** tool-integrations
- **Volatility:** UNKNOWN

**Known limitation:** Single-mic setup means speaker attribution is limited — Granola can't reliably distinguish between speakers in this configuration.

- **Claim:** Maya used Granola to recall conversation context from a prior Sulima salon discussion about drag performance and the "sideshow effect."
- **Source:** `sources/prior-work/handoff-Sulima-project-feb2026.md` §1
- **Confidence:** CONFIRMED
- **Impact:** tool-integrations

[VERIFY: Is Granola actively used for all meetings, or only specific ones? What is the speaker attribution limitation in practice — does Maya work around it?]

#### Zoom
- **Claim:** Maya uses Zoom for client meetings and organizational meetings (ARC, Writing Cohort, etc.).
- **Source:** Calendar data (multiple events mention "Zoom"), `sources/prior-work/Handoff-PRG-Newsletter-Project-2026-02-27.md` §1 (Zoom transcripts)
- **Confidence:** CONFIRMED
- **Impact:** calendar-sync, tool-integrations

[UNKNOWN: Zoom account details — personal or business plan? Recording settings? Integration with Granola?]

### Development Tools

#### Claude Code
- **Claim:** Maya uses Claude Code (v2.1.59) as her primary development tool, running via WSL2 on Ubuntu.
- **Source:** `sources/prior-work/Handoff_ClaudeCode_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** tool-integrations (development workflow, not SL automation target)

#### Local by Flywheel
- **Claim:** Maya uses Local by Flywheel as her WordPress development environment.
- **Source:** `sources/prior-work/Handoff_ClaudeCode_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** hosting (development workflow)

#### GitHub
- **Claim:** Maya's GitHub account is stephbairey / stephbairey@gmail.com. Repos live on the Windows filesystem at `C:\Users\scbzo\Documents\GitHub\`.
- **Source:** `sources/prior-work/Handoff_ClaudeCode_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** tool-integrations (development workflow)

Known repos: `lets-meet` (booking plugin), `local-dashboard` (home dashboard), `seamless-bootstrap` (this project)

### Home Infrastructure

#### Local Dashboard
- **Claim:** Maya runs a household information dashboard on a dedicated 1920x1080 screen in the floating home, showing weather, wind, tides/moon, river conditions, calendar, deliveries, bills, and account balances.
- **Source:** `sources/prior-work/handoff-local-dashboard.md` §1
- **Confidence:** CONFIRMED
- **Impact:** tool-integrations (potential SL integration point)

Stack: Python fetchers → JSON files → JavaScript frontend. Runs on a headless Windows 11 mini-PC. 8 slides with live data.

#### RustDesk
- **Claim:** Maya uses RustDesk for remote access to the dashboard mini-PC.
- **Source:** `sources/prior-work/handoff-local-dashboard.md` §3
- **Confidence:** CONFIRMED
- **Impact:** tool-integrations

#### Self-hosted services (Docker)
- **Claim:** Maya self-hosts multiple services via Docker, including n8n and the -arr stack.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** tool-integrations

[UNKNOWN: Complete list of self-hosted Docker services. The "-arr stack" is mentioned but not specified (Radarr, Sonarr, etc.).]

### Financial & Business Tools

#### Excel
- **Claim:** Maya uses Excel for the n8n routing matrix and royalty report template.
- **Source:** `sources/prior-work/Handoff_MayaDailyProcesses_2026-02-27.md` §3
- **Confidence:** CONFIRMED
- **Impact:** file-management, revenue-workflow

#### Fiverr
- **Claim:** Maya uses Fiverr for outsourcing tasks like course editing.
- **Source:** `sources/prior-work/Handoff_Lingua-Ink-Project_Feb2026.md` §3
- **Confidence:** CONFIRMED
- **Impact:** low priority for SL

---

## Tool Integration Map

These tools connect to each other in documented ways:

```
Gmail ──→ n8n (Amazon label triggers delivery tracking)
TagSpaces ──→ Google Drive ──→ n8n (file routing pipeline)
n8n ──→ Google Sheets (delivery data store)
n8n ──→ Google Drive (file moves to destination folders)
Excel ──→ n8n (routing matrix encoded as code)
ClickUp ──→ Google Calendar (task sync via ✅ events)
WordPress ──→ MailPoet (newsletter from posts)
WordPress ──→ Substack (feed import)
Granola ──→ Zoom? (meeting transcription)
Python fetchers ──→ JSON ──→ Dashboard frontend (local dashboard)
```

---

## Gaps and Questions

[VERIFY: Is Granola used for all meetings or only specific ones?]

[VERIFY: Is the "Writing with Maya" HeyGen channel active or still in planning?]

[VERIFY: ~600 MailPoet subscribers — Lingua Ink Books newsletter specifically, or all lists?]

[VERIFY: Does Maya use Substack for anything beyond Sulima's Light Waves?]

[UNKNOWN: Complete Docker container inventory (what besides n8n?)]

[UNKNOWN: Zoom account type (personal/business), recording settings, Granola integration]

[UNKNOWN: Later social media platforms and posting schedule]

[UNKNOWN: KDP and IngramSpark account details and distribution setup]

[UNKNOWN: Airtable ARC base structure and workflows]

[UNKNOWN: Are there tools not mentioned in handoffs that Maya uses regularly?]
