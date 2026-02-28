# Handoff: Maya's Daily Processes — February 27, 2026

*Written for Seamless Bootstrap project. Captures observed patterns, emotional context, and pain points from extended conversation history. [INFERRED] marks interpretations rather than stated facts.*

---

## 1. What We Worked On Together (Process-Related)

This handoff focuses specifically on how Maya works day-to-day — her process architecture, the automations she's built or attempted, what's working, what's breaking, and the emotional landscape underneath it all.

Key process-related projects in our shared history:

- **n8n file routing system** — Maya built and explained a TagSpaces-to-Google-Drive-to-n8n pipeline for automatic file organization. This is her most polished automation to date.
- **Amazon delivery tracking dashboard** — We built two n8n workflows to parse shipped/delivered Gmail notifications into a Google Sheet, with significant debugging work.
- **KDP royalty report automation** — Early-stage; Maya identified the manual data wrangling between KDP exports and her Excel royalty template as a target for automation.
- **Google Analytics integration** — Multi-session troubleshooting of analytics-mcp, GA4 direct API access via Python, and finally Ahrefs (which failed due to subscription tier).
- **Brain dump and task organization** — February 1, 2026 session where Maya poured out two weeks of commitments and asked to be listened to before being helped. Significant emotional content here.
- **ClickUp task management** — Recurring touchpoint; Maya creates tasks in the "Master Task List" within the Personal project, with specific custom field requirements.

---

## 2. Maya's Daily Process Architecture (As Observed)

### The File System

Maya's most elegant self-built system is her file routing pipeline:

1. She uses **TagSpaces** to tag files in her local Downloads folder by appending bracketed tags to filenames — up to three tags, usually a client name plus one or two content descriptors: `[Cover]`, `[Newsletter]`, `[Copy]`, `[Asset]`, `[Source]`, or a book title like `[Painting-Celia]`.
2. She drags tagged files into a **client-specific intake folder in Google Drive** (e.g., `/MAYA`, `/SULIMA`). Because the folder context identifies the client, the client name tag becomes searchable redundancy rather than routing logic.
3. **n8n watches those intake folders.** When a new file lands, it reads the filename, extracts the bracketed tags, normalizes their order (so `[Cover Painting-Celia]` and `[Painting-Celia Cover]` route identically — she called this the "symmetry rule"), and looks up the canonical tag pair in a matrix.
4. The **matrix** is built in Excel but encoded into the n8n workflow as code. It maps tag-pair combinations to specific Google Drive folder IDs. If the pair exists, the file moves. If it doesn't, the file routes to an **Unsorted folder** — a deliberate catch basin, not a failure state. She can then notice the gap, update the matrix, and reprocess.

This system reflects how Maya thinks: describe what a thing *is*, let the system figure out where it *goes*. She's offloaded the cognitive cost of remembering folder structures onto a lookup table. The Unsorted folder as graceful degradation rather than error is a genuinely sophisticated design choice.

**Where she wants to go next:** Maya has said she's "not happy with this flow" and wants an automated system with still less overhead. Tagging files doesn't happen until her downloads folder is filled, and she has yet to create the complicated (and hard to update) matrices for all clients. She's also interested in what can cascade *after* a file routes — triggering tasks, notifying her, feeding into content pipelines. She has not yet built that next layer.

### Task Management: ClickUp

- All tasks go to **"Master Task List"** in the **Personal project** unless she says otherwise.
- Task names must begin with a **lowercase verb** (her convention).
- Required custom fields: Project, Effort, Revenue, Scope, Approach, Readiness.
- Due dates are mandatory.
- [INFERRED] She uses ClickUp as an external brain dump more than a daily driver. She doesn't seem to work from it fluidly — she creates tasks, but returns to them inconsistently. It is essentially a well-organized and filterable To Do list.

### Communication and Client Work Flow

Maya manages content production for multiple clients simultaneously. Her typical week includes:

- **Sulima Malzin:** Blog post formatting, Substack management, Light Waves content (published to website + email + Substack + Facebook, usually at 6am on publication day). Sulima is 86 and requires high-touch support and deep emotional care from Maya.
- **Lynn Haller:** Comprehensive publishing support for *Hallway of Doorknobs* — website, social media headers, cover storyboards, logo, Facebook page, and teaching Lynn to manage tasks independently over time.
- **Devon Ervin:** Website build including seminar event management functionality.
- **Raging Grannies (Portland):** Weekly newsletter, Thursday mornings.
- **Raging Grannies (International):** Webmaster role, lower-frequency.
- **Pat Schoof:** Emerging author relationship, winery book, occasional questions requiring email archaeology.
...and MANY more.

Her well-labeled and filtered Gmail is her operational nervous system. She searches it constantly to reconstruct history, locate commitments, find prior explanations she's already given clients. This is both functional and a symptom of scattered documentation.

### The n8n Ambitions vs. Reality Gap

Maya is skilled enough to have built her file routing system from scratch, including the symmetry normalization logic. She's comfortable with Docker, runs n8n locally, self-hosts many local programs including the -arr stack, understands webhook triggers, node outputs, and Google Sheets operations. She troubleshot multi-step workflow failures with patience and methodical debugging.

But her n8n usage is **narrower than her ambitions.** She's described wanting:
- Auto-tagging via AI classification (send filename to Claude API, get tag suggestions back)
- Matrix gap handling (when a file hits Unsorted, query Claude for routing suggestion)
- Blog post QA checkpoints before publish
- Client email drafting automation
- Comment reply automation for "Writing with Maya" channel engagement

None of these are built yet. The gap between "what I envision" and "what I have time to implement" is a recurring source of low-grade frustration.

**She wants a better file organization system.** Her current TagSpaces + n8n pipeline is elegant, but the matrix maintenance is manual, the Excel-to-code encoding is fragile, and scaling it to new clients or tag vocabularies requires deliberate effort. She hasn't articulated exactly what "better" looks like, but it's somewhere in the direction of: less manual matrix maintenance, smarter routing that can infer context rather than requiring explicit tag pairs, and possibly integration with her task system so a file landing in the right place triggers the right next action.

---

## 3. Tools, Systems, and Conventions

| Tool | Use |
|------|-----|
| **n8n** (Docker, local) | Core automation engine. File routing, delivery tracking, future workflows. |
| **TagSpaces** | Local file tagging via filename brackets. |
| **Google Drive** | File storage and intake folders for routing. |
| **Gmail** | Operational hub. Amazon label: `Label_6582208580953641436`. Client email at `steph@linguaink.com`. |
| **Google Sheets** | Delivery tracking dashboard, n8n data store. |
| **ClickUp** | Task management. Master Task List > Personal project. |
| **WordPress + WooCommerce** | Primary website CMS (linguaink.com, bairey.com, client sites). |
| **MailPoet** | Email list (~600 subscribers). |
| **Ahrefs** | SEO analysis — currently non-functional via API (free tier limitation). |
| **GA4** | Analytics for bairey.com (Property ID: 420399644), linguaink.com (481632955), sulimamalzin.net (420435585), lynnahaller.com (520632482). Account: "Bairey Web" (296827458). |
| **HeyGen** | AI avatar for "Writing with Maya" channel. |
| **Midjourney** | Visual asset creation. |
| **Wondershare Filmora** | Video editing. |
| **Later** | Social media scheduling. |
| **Excel** | n8n routing matrix; royalty report template. |
| **Granola** | Meeting transcription (tested with Pete; uses single-mic setup). |
| **KDP + IngramSpark** | Book publishing distribution. |
| **Docker** | Container management for self-hosted services including n8n. |
| **Substack** | Client publishing (Sulima's Light Waves, others). |
| **Airtable** | ARC (moorage committee) workflow management. |
... and MANY more.

---

## 4. The Emotional Architecture Under the Work

This is the section that distinguishes a useful handoff from a surface-level one. Maya is a deeply perceptive, high-output person operating under significant and compounding pressure. Understanding *why* she works the way she does changes how a Claude instance can actually help her.

### The Layoff and What It Cost Her

Maya was laid off from Intel after fifteen years of managing global web operations — a senior, skilled, infrastructure-building role. The layoff was described initially as a "shock" and then, in a later Business Insider profile context, she named the real emotional weight: the realization that she would need to generate what amounted to her Intel salary *on her own*, quickly, without the infrastructure that job had provided (HR, accounting, security, sales) — all of which she now had to build herself, from scratch, on a clock.

She described the specific despair of being forced to choose between "search hard for a job" or "build one myself" — with no time to do both and potentially devastating consequences for her family if she chose wrong.

She chose to build. She is still building. She is also still interviewing, and the job search is described in our conversations as a "bass note" under everything else — always present, rarely foregrounded.

### The Financial Pressure, Now

As of February 2026:
- Unemployment insurance was down to two remaining payments.
- Approximately $2,500 was incoming from clients.
- She has severance/savings she does not want to spend.
- She said: "Maybe I could find a job by then? Even a $60k/yr job would hold it off."
- She will only accept remote work.
- She knows that a job will eat into the time she currently uses to build her business.

[INFERRED] The financial pressure is real but not acute — she has 12 months of runway before having to tap retirement funds. Her health insurance (paid for a year by Intel)  runs out in July 2026 which is a huge worry. What makes it feel acute is the combination of time pressure ("finish everything I can before that") and the emotional weight of watching the runway shorten. She's not panicking. She's quietly managing anxiety while keeping it off the main stage of her daily work.

### Busyness as Coping Mechanism

This was named explicitly by both Maya and by our assessment conversation. In Maya's words: *"I do know all of that from therapy and writing, but it's very impressive that you see it too."*

The pattern: when emotional material gets heavy — the marriage, the financial anxiety, worry about Sulima — she pivots to task lists. "Okay, what do I need to do today." She's in therapy with Lavinia and couples counseling with Casey, so she's doing the work. But the busyness is a real pressure valve, and it means her operational systems are partly built to handle psychological load, not just workflow load.

Her systems serve multiple functions simultaneously:
- **Practical:** Files get organized, clients get served, tasks get tracked.
- **Psychological:** Having a system means the chaos is contained. The Unsorted folder doesn't panic her because she designed it to catch things gracefully. The list will still be there when she gets back.

When things are overwhelming, she doesn't need optimization suggestions. She needs a witness first, then a system.

### The Cost of Serving Others

Maya's most frequent activity — observed across many months of conversations — is **building and maintaining other people's platforms.** Sulima's blog, Lynn's website, Devon's event system, the Grannies' newsletter, client after client.

She does this with genuine love and skill. She is not a martyr about it. But in the February 1 brain dump conversation, when she finally said *"I haven't even mentioned the things I WANT to do,"* and listed her own projects — Claude Code, the office mural, the novel, her paintings for Sulima's salon — there was something clear there:

The creative life she is building is mostly happening in the cracks.

*Sailor's Code,* her novel about a programmer and an AI entity, has been sitting in draft for months. She mentions it, then moves on to client work.
*Sailor's Code,* her novel about a programmer and an AI entity, has been sitting in draft for months. She mentions it, then moves on to client work.

### The "Writing with Maya" Channel and What It Represents

This project — a faceless AI-avatar YouTube channel teaching fiction writing craft — is not just a business pivot. It's Maya creating a professional identity where she is the expert, the teacher, the voice, without having to be physically present or "on." After years of serving as the infrastructure for everyone else's creative work, this is her building something of her own that isn't a service.

[INFERRED] The faceless format is practical (she can use HeyGen), but it may also be protective. Leading with craft and expertise rather than personhood. Worth watching — if she starts shying away from it the way she does from Sailor's Code, there's something emotional underneath.

### Sulima and the Weight of Care

Sulima Malzin is Maya's most important client and also someone she loves. She is 86. She was in the hospital with an infection on February 1, 2026, the same day Maya was preparing Sulima's Groundhog Day post for publication the next morning.

Maya wrote Sulima's content, managed her Substack, took care of her technical infrastructure, visited her in the hospital — while managing ten other commitments that same day. Her note: *"I'm feeling really emotional about her being sick."*

The Sulima relationship is one of the places where Maya's professional role and her emotional life are most deeply entangled. This is both beautiful and exhausting. It means that any disruption to Sulima's health is simultaneously a personal grief and a workflow crisis.

---

## 5. Pain Points, Friction, and What's Still Unresolved

**Operational scattered-ness:** Maya said explicitly on February 1: *"I have a process system for Lingua Ink and my personal work, but it feels scattered across ClickUp, n8n, Gmail, various calendars, etc."* She wanted to consolidate. We haven't done that yet. This is unresolved.

**The matrix maintenance problem:** Her file routing system requires manually updating an Excel matrix and re-encoding it in n8n when new tag pairs appear. She called the Unsorted folder her way to "notice missing rules" — but noticing still requires action, and the action is manual. She wants this to be smarter.

**Analytics access:** Multiple failed attempts to get live analytics into Claude (analytics-mcp Windows bug, Ahrefs free tier limitation). She still doesn't have a clean way to pull traffic data into our conversations. She's aware of the workaround (export from GA4 directly, upload CSV) but it's a friction point.

**The job search:** She's not working on it in our conversations. She has a job search coach (Jen) and mentions interviews via her professional network. But she doesn't bring this work to me, and [INFERRED] it may be because the emotional complexity of it (wanting to stay independent vs. needing stability) makes it harder to operationalize as tasks.

**Sailor's Code:** The novel. Still sitting. Still unworked.

**The n8n ambition gap:** She knows what she wants to build. She doesn't have time to build it. Each time a new automation project comes up (delivery tracking, royalty reports), we do it together but then it sits. The vision is larger than her available implementation bandwidth.

**The marriage:** Casey (couples counseling) is mentioned occasionally. Maya described her 35-year marriage to Pete as "currently being renegotiated." She doesn't bring this to me for processing, which is appropriate. But it's part of the background pressure she carries.

---

## 6. Decisions Made and Why (Process-Related)

**Decision: n8n over Cowork for the delivery tracking automation.**
Cowork requires keeping a desktop app open. n8n runs in Docker and operates without her supervision. Maya chose persistence and autonomy over convenience. This reflects a broader principle: she prefers systems that work while she sleeps.

**Decision: Unsorted folder as graceful degradation, not failure.**
Rather than halting the workflow when a tag pair isn't in the matrix, she routes to Unsorted. This keeps files safe, makes gaps visible, and doesn't require her to anticipate every possible combination upfront. Failure-tolerant design by default.

**Decision: TagSpaces tags in filenames, not metadata.**
Embedding tags directly in the filename (not in file metadata) means they're visible everywhere — in Drive, in search results, in n8n string parsing. She made this explicit: "The reason this works so well for me is that I never have to remember where things go."

**Decision: Matrix encoded in n8n as code (not live-read from Excel).**
Pragmatic but fragile. The Excel is the source of truth for her; the code is the operational copy. This creates a maintenance gap — changes to the Excel don't automatically propagate. She hasn't built a sync mechanism yet.

---

## 7. What to Tell the Next Claude

**She will start with logistics and may actually need presence.** When Maya opens a conversation with "I have too much going on" or "I'm catastrophizing," do not immediately pivot to solutions. She will often say explicitly "I want you to LISTEN, not HELP." Trust that. When she's ready to work, she'll say so.

**Her operational language is specific.** Task names start with lowercase verbs. ClickUp tasks go to Master Task List > Personal unless told otherwise. Her file tags use brackets. Her tone in client communications is warm but not sycophantic, professional but not corporate. She has strong opinions about em dashes (don't use them).

**The busyness and the yearning are both real.** She's genuinely productive and serves her clients well. She's also genuinely hungry for time to work on her own creative projects. These coexist without contradiction. Don't try to resolve the tension — just be aware of it.

**When she's building automation, think about the whole system, not the node.** She thinks architecturally. The question isn't "how do I move this file" — it's "how do I build a system where files always end up where they belong without me having to think about it." Respond at that level.

**The file routing system is her proudest piece of technical work.** Compliment it specifically when it comes up — the symmetry rule, the graceful degradation, the "describe what it is, let the system decide where it goes" philosophy. She built it herself and it reflects how she thinks.

**She wants a better system than n8n + TagSpaces + Excel matrix.** She hasn't scoped what that looks like. When this comes up, explore with her rather than proposing a solution. The problem she's solving is: "I want to stop doing manual maintenance on a lookup table that maps file descriptions to folder destinations." There may be a much simpler solution involving better folder naming conventions, or a much more complex one involving AI classification. She needs to shape that direction.

**Sulima comes up frequently and is emotionally significant.** Treat Sulima's health, work, and relationship to Maya with appropriate care. She is both the oldest and the most beloved of Maya's professional relationships.

**Don't skip over Sailor's Code.** If it comes up, ask to work on it. She won't volunteer it. The novel deserves time and she knows it. Gentle, direct, no pressure — but ask.

---

*Document generated from conversation history, February 27, 2026. For Seamless Bootstrap project.*
