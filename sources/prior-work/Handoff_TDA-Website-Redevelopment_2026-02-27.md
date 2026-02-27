# Handoff: TDA Website Redevelopment — February 27, 2026

---

## 1. What We Worked On Together

### The Big Picture

You (Maya / Steph Bairey, Principal at Lingua Ink Media) are rebuilding the Tomahawk Destiny Association (TDA) website — a floating home community marina on the Columbia River in Portland, OR. The project migrates from an outdated FrontSteps/AssociationVoice platform to a modern WordPress installation, within a $1,000 board-approved budget, hosted on NixiHost.

The staging site is at: **https://staging.tomahawkdestiny.com**  
Production target: **tomahawkdestiny.com**

### What We Built Together

**Core Infrastructure:**
- WordPress installation with the **Leisure theme** (CurlyThemes) — custom CSS applied throughout
- **Ultimate Member** for user management: 143 residents imported via CSV, five custom roles configured (Owner, Renter, ARC Member, Board Member, Administrator)
- Resident data cleaned from FrontSteps export; CSV formatted for UM import with default password; all accounts set to `account_status = approved`

**Custom Plugins (all authored by Lingua Ink Media):**
- **TDA File Tree** (`tda-file-tree`) — accordion-style file browser that reads directly from `wp-content/uploads/tda-files/`, displays folders/files with emoji icons, shortcode `[tda_file_tree]`. Skips index.html files, shows "No files yet." for empty folders. Current version: 1.0.2.
- **TDA File Sync** (`tda-file-sync`) — registers files in `tda-files/` as WordPress media library attachments *without moving them*, enabling PDF search indexing while preserving Bill's folder hierarchy. Excludes dot-directories (like `.thumbnails`). Daily WP-Cron + manual trigger.
- **TDA Directory Tools** (change tracking module) — hooks into `profile_update`, `um_after_user_updated`, and `user_register` to stamp `_tda_last_modified` and `_tda_last_modified_by` on every profile save. Shortcode `[tda_change_report days="30"]` produces a filterable report (30/45/60/90 days) showing New vs. Edited badges with attribution.
- **TDA Email Preview** — adds a preview button to the Classic Editor publish box that opens a popup showing exactly how a post will appear in a MailPoet-branded email, including TDA header, footer, and color codes. Detects attachments (via the Attachments plugin by Jon Christopher) and shows a notice since MailPoet doesn't send file attachments.

**Other Plugins in Use:**
- **Advanced File Manager** — Bill's tool for uploading files; maintains folder hierarchy under `tda-files/`
- **WebEquipe PDF Search** — indexes PDFs registered in the media library (enabled by TDA File Sync)
- **MailPoet** — email communication; partially configured for automated post-to-email workflow
- **Simple File List Pro** ($25, purchased) — document organization; replaced original plan for WordPress Download Manager
- **FooGallery** — community photo gallery
- **The Events Calendar** — meeting management
- **Forminator** — form building (contact forms; future Stripe integration)
- **FileBird** — media library folder organization

**Directory System:**
- Printable directory page with dual views: By Name (alphabetical) and By Slip (grouped by slip number), accessible at `/printable-directory/`
- Print CSS suppresses Leisure theme header elements (`#header`, `#main-nav`, `#secondary-nav`, `#page-heading`)
- Resident count excludes TDA Webmaster account and inactive users from display (using `TDA_ACTIVE_ROLES` and `TDA_ROLE_LABELS` constants)
- Slip number prefix CSS: `.um-member-tagline.um-member-tagline-slip::before { content: "#"; }`

**Email/Communications System:**
- Board members with specific authorized email addresses (webmaster, president, secretary, contractor) can create posts that trigger MailPoet community-wide broadcasts
- Emails are community-wide only, no segmentation
- Email preview plugin shows authors exactly what the email will look like before publishing
- Posts serve double duty: website archive + resident email

**News/Posts Privacy:**
- Ultimate Member's "Hide from queries" feature used to fully remove restricted posts from archive listings for logged-out visitors (this was a specific bug fix — the standard restriction alone wasn't enough)

**MCP Integration (exploratory):**
- Connected WordPress to Claude Desktop via MCP, using a custom plugin with namespace `tda-directory` and abilities like `recently-changed` (accepts `days` parameter)
- Maya's interest was primarily in learning the MCP infrastructure, not the specific deliverable

### Current Status

The site is largely feature-complete on staging. Remaining pre-launch items (as of ~Feb 23, 2026):

**Steph — Pre-Launch Open:**
- Register remaining files via Add From Server (waiting on Bill's uploads)
- Committee chair calendar permissions
- Build welcome/resource page (waiting on Bill for content direction)
- Collaborate with Bill on file naming/descriptions/retention

**Steph — Post-Launch / Future:**
- Payment system / Stripe — emails sent to Tom (treasurer) and Joanne (bookkeeper), no response yet
- Training sessions for Bill and admins
- Revisit Bill's change report format after getting his feedback
- MailPoet integration — partially in place, workflow needs finalizing
- Finalize website maintenance line item (waiting on Bill to research current cost)
- Domain cutover (last step — after full approval)

**Bill — Open:**
- Research what the moorage pays their current web admin
- Download hidden files from Front Steps
- Collaborate on file naming and retention decisions
- Provide content for welcome/resource page
- Get finance/payment numbers to Tom O'Connor

---

## 2. How Maya Works (as observed here)

**Problem-solving style:** Maya works iteratively and tests immediately. She moves, encounters the edge case, and adjusts. This is efficient for her because she's in the WordPress backend and can verify behavior in real time.

**Decision-making:** Pragmatic, not perfectionist. When something is "good enough" and the cost of making it perfect is high, she drops it. Example: the resident count cosmetic issue — "I say no. There are a bunch of places to edit that and it's not worth it." She's also quick to recognize when a workaround is cleaner than the canonical solution.

**Quality bar:** High for anything user-facing, especially for non-technical users. She cares deeply about workflows that require no cognitive translation. Her phrase: users who "struggle to open Excel" and want intuitive interfaces "without caveats or mental translation steps." This isn't impatience with users — it's genuine design empathy.

**Instructions to Claude:** She tends to give context-rich, multi-part instructions. She'll often start with "here's what we did last time" and then "here's the new problem." She expects Claude to synthesize previous context without being re-briefed on everything. She uses `conversation_search` prompts freely and expects Claude to look things up before asking her to repeat herself.

**When something isn't right:** She's direct but not harsh. She'll say "that's awkward" or "I don't think that's working" and expect a quick revision, not a lengthy explanation of why the first attempt was reasonable.

**Handoffs:** Maya maintains detailed handoff documents between sessions because she works across multiple chat contexts. She has a systematic approach to this (as evidenced by the handoff template she's using right now). She treats these as operational continuity tools, not documentation for documentation's sake.

**Attention to unexpected details:** She notices when Claude implements something *she didn't ask for* that's genuinely useful (e.g., the automatic filtering of `.noemail@` placeholder addresses) and responds positively. She likes when Claude brings something to the table beyond the literal request.

---

## 3. Tools, Systems, and Conventions

### WordPress / Hosting
- **Host:** NixiHost
- **Staging URL:** https://staging.tomahawkdestiny.com
- **Production URL:** https://tomahawkdestiny.com
- **Admin account:** `tdaadmin` — full WordPress backend access; regular residents restricted from wp-admin

### Ultimate Member — Custom Field Slugs
These are the exact meta keys for UM custom fields (critical for CSV imports, queries, and plugin code):
- `slip` — slip/lot number
- `mailing_address`
- `residency` — residency status (Owner, Renter, Resident)
- `phone_number` — mobile phone
- `home_phone`
- `work-phone` (**hyphen**, not underscore — this is the one that will bite you)
- `user_email` — primary email
- `user_email_11` — secondary email
- `tda_title` — display title

### UM Role Slugs
- `um_owner`
- `um_renter`
- `um_resident`
- `um_arc-member`
- `um_board-member`
- `um_administrator`

(Note: Maya should verify these match exactly what's in UM → User Roles each session)

### File System Layout
- Bill's file uploads live in: `wp-content/uploads/tda-files/`
- Advanced File Manager maintains the folder hierarchy here
- TDA File Sync registers files from this directory into WordPress media library
- Thumbnails created by Advanced File Manager live in `.thumbnails` subdirectories — excluded from sync

### Custom Plugin Locations
All custom plugins live in `wp-content/plugins/`:
- `tda-file-tree/`
- `tda-file-sync/`
- `tda-directory-tools/` (includes change tracking shortcode)
- `tda-email-preview/`

### Email Authorization
Posts trigger MailPoet emails only from these four addresses:
- webmaster@tomahawkdestiny.com
- [president's email — confirm with current board roster]
- [secretary's email]
- [contractor email — likely Maya's Lingua Ink email]

### MailPoet Template Branding
Email preview plugin uses TDA-specific colors/fonts; the exact values are embedded in the preview plugin CSS. Attachment detection uses the Attachments plugin (Jon Christopher) meta key format.

### Printable Directory
- URL: `/printable-directory/`
- Shortcode: `[tda_printable_directory]`
- Two views: By Name (alphabetical) / By Slip (grouped)
- Print CSS suppresses: `#header`, `#main-nav`, `#secondary-nav`, `#page-heading`
- wp_date() used (not date()) for proper timezone handling

### Change Tracking Shortcode
- `[tda_change_report days="30"]`
- URL parameter override: `?days=60`
- Tracks via `_tda_last_modified` and `_tda_last_modified_by` user meta
- Change tracking is NOT retroactive — only captures edits made after plugin installation

### MCP Integration
- Endpoint namespace: `tda-directory`
- Abilities: `recently-changed` (accepts `days` parameter)
- No restart needed if endpoint paths are unchanged

### Budget Summary (as of early Feb 2026)
One-time costs (board-approved):
- Website development: $1,000.00
- Hosting reimbursement (7 months @ $12): $84.00
- File search plugin upgrade: $139.39
- **Total owed: $1,223.39**

Annual operating (FY2027):
- Hosting: $144/year ($12/month)
- Website maintenance/updates: TBD (Bill researching)

Payment to Lingua Ink Media: check to 470 N Tomahawk Island Drive, Portland OR 97217, or Stripe link (with $15 service fee).

---

## 4. Preferences and Opinions

**Formatting:** Maya dislikes over-structured, bullet-heavy responses. She prefers prose. She will not say this explicitly every session, so Claude should default to conversational delivery unless the content genuinely needs a table or list.

**Response length:** Scale to the task. Short answers to short questions. She doesn't need warm-up paragraphs or recaps of what she just said.

**Tone:** Friend-with-expertise. Warm, direct, not clinical. She responds well to genuine reactions and specificity. She notices when responses feel canned.

**Technical opinions:**
- Free plugins strongly preferred; premium only when genuinely necessary (exception: Simple File List Pro at $25 was worth it)
- Custom code is fine when it's the right call (she built three custom plugins in this project)
- Prefers "does the job cleanly" over "technically elegant but complex"
- Dislikes solutions that create new administrative burden for non-technical users

**UX philosophy:** Exact replication of existing workflows matters more than introducing superior alternatives that require behavioral change. New systems should match existing mental models, not require users to adapt.

**On plugin conflicts / architectural tension:** When plugins work against each other, she appreciates creative bridging solutions (TDA File Sync was exactly this — it elegantly solved the tension between the media library requirement and Bill's folder hierarchy).

**Communication style with stakeholders:** Formal when needed (board emails, budget requests) but not stilted. She edits for smoothness — "that's awkward" is a meaningful signal.

---

## 5. Key Relationships and Contexts

**Bill Bowling** — Current TDA webmaster; reports to the board; the primary day-to-day admin of the new site post-launch. Non-technical but capable of following documented procedures. Has strong opinions about file organization (he maintains the `tda-files/` folder hierarchy manually). Maya has a collaborative, collegial relationship with him. He requested: (1) a change tracking report for monthly committee meetings, (2) a printable directory, (3) more compact document display. He also has institutional knowledge about the community (property history, boundary pins, etc.) that isn't written down anywhere. Maya is aware of this and accounts for it.

**Tom O'Connor** — TDA Treasurer. Relevant for Stripe payment setup. Maya has emailed him but hasn't heard back.

**Joanne** — TDA Bookkeeper. Also looped in on Stripe discussions.

**Liz Munnelly** — TDA Board Secretary. Maya helped draft an email to her about boundary pins and coordinating with Mike's team and Don Gire.

**Don Gire** — Has institutional knowledge about property boundary pins "in his head rather than on paper." 

**The TDA Board** — Maya demoed the staging site to them in late January 2026; they were impressed ("everyone was sort of stunned, as expected"). The board approved the $1,000 budget and the project scope.

**Lingua Ink Media** — Maya's business. She is the Principal (not Creative Director — she updated this title around early Feb 2026). The business has two wings: Lingua Ink Books (creative) and Lingua Ink Media (technical/web development). She is a resident of Tomahawk Floating Homes and does this work as both a professional service and a community contribution.

---

## 6. Challenges and Friction Points

**The FrontSteps export mess:** Resident data from the old platform required significant cleanup — multiple properties per person, slip numbers with letters (556A, 556B), multiple phone types, placeholder `.noemail@` addresses. Maya handled much of this manually, augmented by her personal knowledge of the community.

**Ultimate Member tab bug:** Profile fields wouldn't display on the front-end view despite correct configuration. Root cause: UM's tab system was hiding content when tabs were disabled. Resolved by re-enabling the "About" tab. This is a non-obvious gotcha — document it clearly if onboarding another developer.

**News/posts privacy:** Ultimate Member's standard content restriction wasn't enough to remove restricted posts from archive listings. Required also enabling "Hide from queries." Two-step fix that wasn't apparent from UM documentation.

**Print CSS and the Leisure theme:** Leisure theme's header kept appearing in printed directory output. Required targeting `#header`, `#main-nav`, `#secondary-nav`, `#page-heading` specifically — these aren't surfaced in WPBakery or standard page template settings. Had to fetch theme docs directly to find the Individual Page Settings meta box.

**The two-plugin architectural conflict:** Advanced File Manager was creating `.thumbnails` subdirectories that TDA File Sync was incorrectly registering as media library entries. Required v1.0.1 to exclude dot-directories during scanning and v1.0.2 to also prune existing attachment records pointing to dot-directories.

**Stripe/payment system:** Still unresolved. Tom and Joanne haven't responded to Maya's outreach. This will eventually require working directly with the treasurer to set up a TDA-owned Stripe account (bank account, routing info, EIN, etc.). Classified as post-launch.

**Committee chair calendar permissions:** On the open list for a while; not yet implemented. Likely a straightforward The Events Calendar role configuration but hasn't been prioritized.

**Bill's welcome/resource page content:** Maya is blocked on this; it's waiting on Bill to provide direction. She's described it as a "new resident start here" style page.

**Timezone display:** An earlier edge case — `date()` in PHP doesn't respect WordPress timezone settings. Fixed by using `wp_date()` instead. Worth remembering this convention for any future time-display code.

---

## 7. Decisions Made and Why

**Ultimate Member over alternatives (WP-Members, MemberPress free):**  
UM was chosen because it includes a member directory capability out of the box, not just content restriction. The alternatives would have required separate solutions for the directory feature. UM also handles registration, login forms, and password reset in a unified system. Tradeoff: UM has more complexity and occasional quirks (like the tab bug), but the all-in-one value won out.

**TDA File Tree (custom) over WP File Download ($49):**  
Replaced a commercial plugin with a custom build. The $49 plugin (WP File Download by JoomUnited) had the accordion UI needed, but building a lightweight custom solution was more appropriate for the project budget and gave full control. The custom plugin ended up being simpler and more targeted than the commercial option.

**Two-plugin architecture (File Tree + File Sync) over integrated solution:**  
The architectural tension: WordPress media library requires registered attachments for PDF indexing, but registering files moves them out of Bill's hierarchical folder structure. Rather than forcing a choice between the two, TDA File Sync bridges them — registering files as attachments *in place* without touching the files. This preserves Bill's entire existing workflow while enabling PDF search. Maya described it as "elegant" and it genuinely is.

**MailPoet for community-wide broadcasts (no segmentation):**  
All emails go to all residents. Segments were considered but ruled out for simplicity — the board wanted a single broadcast mechanism, not audience management. The four authorized email addresses restrict who can trigger a send, which is sufficient access control.

**Email preview plugin (custom) over MailPoet's native preview:**  
MailPoet's native preview requires navigating the MailPoet backend, which is too many steps for non-technical board members. A custom popup preview directly in the post editor gives authors an accurate visual confirmation before publishing, without requiring them to understand MailPoet's interface at all.

**Dropping the resident count cosmetic fix:**  
The directory displayed a slightly inaccurate resident count (included TDA Webmaster account and inactive users in the number). Fixing it would have required edits in multiple places. Maya explicitly decided: "I say no. There are a bunch of places to edit that and it's not worth it." Good call — it's invisible to most users.

**Simple File List Pro ($25) over WordPress Download Manager (free):**  
Download Manager was the original plan, but Simple File List Pro more closely matched the current site's folder-based workflow that Bill was already familiar with. The exact-replication principle won over the cost savings.

---

## 8. Things You'd Tell the Next Claude

**Context retrieval is your first job.** Maya expects you to search previous conversations before asking her to repeat herself. She has a rich project history in this chat context. Use `conversation_search` liberally with specific terms — field names, plugin names, feature names — and cross-reference the task lists that appear in recent chats. The most recent consolidated task list was from Feb 27, 2026.

**The `work-phone` field uses a hyphen, not an underscore.** This will bite you if you write code that touches UM custom fields and you forget. The slug is `work-phone`.

**Never suggest "let's use a plugin" when we've already built a custom one.** TDA File Tree, TDA File Sync, TDA Directory Tools, and TDA Email Preview are all active and working. Don't recommend alternatives.

**Bill is the day-to-day admin, not a developer.** Any solution involving him needs to work without explanation. If you're designing a workflow and you find yourself writing "Bill will need to..." and the next words involve anything technical, flag it.

**MailPoet integration is partially done but not finalized.** The email preview plugin exists. The workflow for triggering sends from posts is partially set up. Don't treat this as unstarted — ask Maya what state it's in before proposing a build plan.

**The project is essentially in "last mile" mode.** The site is largely feature-complete. The main open items are: committee chair calendar permissions, Bill's remaining file uploads and naming decisions, the welcome/resource page (blocked on Bill), and Stripe (blocked on treasurer). Don't get excited and propose new features unless Maya explicitly opens that door.

**Maya has strong "cost of change" awareness.** Before proposing a fix that touches multiple files or has ripple effects, flag the scope. She'll often decide a small imperfection isn't worth a large fix.

**She writes well and knows it.** When helping with stakeholder communications (board emails, budget docs, drafts to Bill), pay attention to her voice — it's professional but not stuffy, specific, and slightly warm. Don't default to corporate register.

**The MCP integration between Claude Desktop and WordPress is live.** Maya was actively exploring this as of Feb 19, 2026. If she mentions "CD" and "CW" in a session, those are shorthand for two Claude instances she was running simultaneously (Claude Desktop and Claude Website).

**Timezone gotcha:** Always use `wp_date()` not `date()` in any PHP that displays timestamps to users.

**Dot-directories exclusion:** The `.thumbnails` folders created by Advanced File Manager must always be excluded from any file scanning logic. This pattern applies to TDA File Sync and any future code that touches `tda-files/`.

**The "exact replication" principle is load-bearing.** Maya repeatedly chose familiar-but-imperfect over new-but-better when "better" meant users had to change their mental model. Don't propose redesigns of existing workflows unless there's a significant problem with them.

---

*Document generated: February 27, 2026*  
*Project: TDA Website Redevelopment*  
*Primary: Maya Bairey / Lingua Ink Media*  
*Staging: https://staging.tomahawkdestiny.com*
