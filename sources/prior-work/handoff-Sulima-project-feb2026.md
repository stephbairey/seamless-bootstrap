# Handoff: Light Waves Publishing Project — February 27, 2026

*Generated for Seamless Bootstrap knowledge extraction. Covers Maya Bairey's work with Sulima Malzin as observed within this Claude project context.*

---

## 1. What We Worked On Together

### Primary Project: Light Waves Blog Publishing Workflow

The central work of this project has been managing the multi-platform publication of Sulima Malzin's "Light Waves" blog posts. Maya is Sulima's content manager, webmaster, and publisher — and the work involves transforming Sulima's Word documents into polished posts across three platforms: WordPress (sulimamalzin.net), Mailpoet email newsletter, and Substack (sulima.substack.com).

The most documented session involved a Valentine's Day-themed post: "LOVE is LOVE is LOVE is..." This session became a full audit of the workflow, surfacing every edge case and producing a comprehensive process document (`LIGHT_WAVES_WORKFLOW.md`, now a project file).

**Deliverables produced:**
- Clean HTML for the WordPress post, preserving Sulima's voice
- Email-safe HTML version with YouTube embeds replaced by linked thumbnails with play button overlays
- YouTube thumbnail images generated via Python/PIL with semi-transparent play button compositing
- PDF excerpt from *All in the Soup Together* (interior pages), extracted using a workaround for a corrupt-seeming PDF
- The workflow process document itself — a durable reference capturing editorial decisions, technical patterns, and institutional knowledge

**Current status:** The workflow doc is finalized and in the project. The publish cycle for each new post should take ~20 minutes with Claude assistance.

### Secondary: Sulima's Salon / Personal Context

One conversation involved preparing for a lunch gathering at Sulima's home — not a publishing task, but a relationship maintenance and thinking-through task. Maya was preparing materials (garlic bread, potting soil for Sulima's peace lily) and thinking through a sensitive topic: a proposed drag "making/unmaking" performance for one of Sulima's salons, and the pushback it received around the "sideshow effect" — the concern that performing identity for audiences outside one's community can feel like tokenism regardless of intentions. Maya planned to contribute the Martha Graham quote about the duty to share one's unique experiences. This required retrieving meeting transcripts from Granola to recall the prior conversation context.

---

## 2. How Maya Works (as Observed Here)

**She knows what she wants; she just needs help executing.** Maya doesn't come to Claude uncertain about direction — she has strong editorial instincts and a clear sense of Sulima's voice. Where she needs help is the technical work (image extraction, link resolution, HTML generation, PDF manipulation) and the synthesis/drafting work that benefits from a thinking partner.

**She corrects course precisely and doesn't repeat herself.** When something is off, Maya identifies exactly what's wrong ("the preview email is too long — it's listing her references, not naming her arc") and states the fix once. She expects it to stick. She doesn't accept "I'll try to do better" — she expects the correction to be applied and demonstrated.

**She invests in the process document.** After the Valentine's Day session, we collaboratively built a detailed workflow doc. This is a signal: Maya values institutional knowledge capture. She thinks in systems, not just tasks.

**She picks her editorial battles with Sulima deliberately.** There's a recurring tension between preserving Sulima's voice (heavy bold, informal contractions, "click here" link style) and fixing things that would genuinely impede readability or functionality. Maya's rule is: flag, don't assume. She makes choices carefully and knows Sulima may push back.

**She has a strong aesthetic sense.** The preview email note to Sulima is a perfect example — she didn't want a summary of citations, she wanted a sentence that named the arc. "From resolve to tenderness to wonder, and the Gibson close turns the whole thing into a love letter that isn't about romance at all." That's the level of craft she holds herself to.

**She wants Claude emotionally engaged with her writing.** Her preferences specify: tie praise to specific choices, react genuinely, notice craft. This applies when she's writing in her own voice — which may not come up in publishing work, but will in other contexts.

**She asks clarifying questions before going off-track.** [INFERRED] Based on how she structured the workflow doc and corrected assumptions, she seems to prefer Claude asking over Claude guessing when there's genuine ambiguity. She said explicitly: "The right move is to ask for the final content rather than reconstructing from memory."

**She moves fast and expects Claude to keep up.** The Valentine's Day session covered image extraction, link resolution, PDF workarounds, HTML formatting, email-safe conversion, and workflow documentation in a single session. She doesn't need hand-holding between tasks.

---

## 3. Tools, Systems, and Conventions

### WordPress
- **Site:** https://sulimamalzin.net
- **Media uploads pattern:** `https://sulimamalzin.net/wp-content/uploads/YYYY/MM/filename`
- **Post URL pattern:** `https://sulimamalzin.net/[slug]/`
- **YouTube embedding:** WordPress auto-embeds from bare `https://www.youtube.com/watch?v=XXXXX` URLs on their own line. Do NOT use iframes.
- **Draft/publish dance:** Post goes to draft → briefly published for homepage screenshot → reverted to draft → sent to Sulima for approval → published at 6am on publish day

### Mailpoet
- Lives inside WordPress
- Workflow: Duplicate last email → update title/description/preview text → pull latest post → swap YouTube embeds for linked thumbnails → send
- The Mailpoet template already includes the Buymeacoffee boilerplate — don't add it to the email HTML

### Substack
- **URL:** https://sulima.substack.com
- **Import method:** Settings → Import posts
- **Feed URL:** `https://ftr.fivefilters.net/makefulltextfeed.php?url=https%3A%2F%2Fsulimamalzin.net%2Ffeed&max=1&summary=1`
- **Post-import cleanup:** Remove the auto-generated "ad free" footer; replace with `Originally published on [sulimamalzin.net](POST_URL)`; add Buymeacoffee boilerplate

### YouTube Thumbnails (email-safe)
- Thumbnail URL pattern: `https://img.youtube.com/vi/VIDEO_ID/hqdefault.jpg` — reliable, no API key needed
- Play button overlay: 36px radius dark circle, white triangle offset 4px right for visual balance, saved as PNG to preserve transparency
- HTML pattern for email: `<a href="VIDEO_URL"><img src="THUMBNAIL_URL" alt="Description - click to watch on YouTube" width="750" /></a>`

### PDF Extraction (Sulima's book interiors)
- **Problem:** `/mnt/project/AITST2ndedinteriorpages.pdf` (*All in the Soup Together*, 94 pages) reports as "not a PDF" to PyMuPDF's `insert_pdf` method despite being a valid file
- **Workaround:** Render pages as pixmaps at 200 DPI using `page.get_pixmap(matrix=fitz.Matrix(200/72, 200/72))`, insert as images into a new PDF document
- **Other book interiors available in project:** `Words_That_Dance_ed2_v6_interior.pdf`, `TRIBUTARIES_6x9_v1a_revS.docx`, `afwb-kdp-print-content.pdf`

### Project Files (read-only reference)
| File | What it is |
|------|-----------|
| `/mnt/project/AITST2ndedinteriorpages.pdf` | *All in the Soup Together* interior, 94pp, image-based, requires pixmap workaround |
| `/mnt/project/AITST2ndedwholecover.pdf` | *All in the Soup Together* cover |
| `/mnt/project/TRIBUTARIES_6x9_v1a_revS.docx` | *Tributaries* interior |
| `/mnt/project/Tributaries_cover_6x9__front.jpg` | *Tributaries* cover |
| `/mnt/project/Words_That_Dance_ed2_v6_interior.pdf` | *Words That Dance* interior |
| `/mnt/project/wordsthatdancecover.jpg` | *Words That Dance* cover |
| `/mnt/project/afwb-kdp-print-content.pdf` | *Arms Filled with Bittersweet* interior |
| `/mnt/project/afwbkdpcover.jpg` | *Arms Filled with Bittersweet* cover |
| `/mnt/project/LIGHT_WAVES_WORKFLOW.md` | The workflow process doc — read this first for any publishing task |

### Granola Integration
- Accessible via MCP server at `https://mcp.granola.ai/mcp`
- Useful for retrieving transcripts from Maya's meetings with Sulima
- Successfully retrieved transcript using query: "Steph Sulima meeting February 12 2026" → meeting ID `cfdeeaf0-fef1-4a25-971d-6dcbc387c59b`
- Granola calls Maya "Steph" frequently; query worked when this name was included

### WordPress.com MCP
- Connected at `https://public-api.wordpress.com/wpcom/v2/mcp/v1`
- Not extensively used yet, but available for post management tasks

---

## 4. Preferences and Opinions

### Editorial / Voice
- **Preserve Sulima's voice above all else.** Heavy bold, spaced ellipses, "two&ahalf," "ourself," "singalong" (as noun/adjective), excessive italics — these are features, not bugs
- **Selective unbolding is okay** when bold stops being emphasis and becomes default. But flag it, don't silently edit
- **"Click here" link style is correct** for Sulima's blog. Do not modernize to contextual links
- **Poems go in blockquotes** with title and byline inside the blockquote — one visual unit
- **Hartmann-style quotes** (long quoted passages): `padding-left: 40px`
- **Periods go inside quotes** — Maya moves them. Sulima notices but accepts it

### Communication / Working with Maya
- **No bullet points by default.** Prose that flows. Format only when it genuinely helps
- **Match her energy** — conversational, direct, warm but not saccharine
- **Scale response to task.** Simple question → concise answer. Complex creative work → go deep
- **Emotional engagement with her writing.** Tie praise to specific choices. Generic praise is useless
- **Preview email arc note:** 1-2 sentences MAX. Name the through-line, not the references. "This one has a beautiful arc — from resolve to tenderness to wonder" is the right register
- **Ask, don't reconstruct.** If you don't have the final HTML, ask for it

### Technical Opinions
- Clean YouTube URLs only (bare watch URLs for WP, no iframes)
- Images uploaded to WP media library, not hotlinked from external sources
- Email HTML: only two changes from WP version (embed swap + remove Buymeacoffee boilerplate)

---

## 5. Key Relationships and Contexts

### Sulima Malzin
- 85-year-old poet in Oregon
- Maya's relationship with her is both professional and deeply personal — they are close friends
- Maya has published four of Sulima's books through Lingua Ink Books: *All in the Soup Together*, *Tributaries*, *Words That Dance*, *Arms Filled with Bittersweet*
- **Royalty split: 0%.** This is a labor of love, not a commercial arrangement
- Sulima hosts salon gatherings and lunch gatherings at her home
- She has opinions about her formatting and will sometimes push back on Maya's editorial choices
- She writes from a specific voice — elderly, warm, literary, community-oriented, with recurring themes of justice, art, and human connection
- She is not particularly technical; Maya handles all digital infrastructure

### Lingua Ink Books
- Maya's publishing imprint, publishing Sulima's four books
- Handles distribution through bookstore consignments, Amazon, more
- Has its own voice/brand identity, distinct from Maya's personal voice

### Maya's Platforms / Voices
- **Lingua Ink voice** — publisher voice, distinct from personal
- **Maya Bairey voice** — personal
- **LinkedIn** — professional, different register
- **Personal blog** — different from Sulima's blog work

---

## 6. Challenges and Friction Points

### Technical
- **The AITST PDF corruption issue** — the `insert_pdf` method fails; pixmap workaround at 200 DPI is the fix. This will likely recur whenever Maya needs to extract pages from this specific file
- **Sulima's links are reliably messy** — Yahoo search URLs, Substack redirects, hotlinked external images. Plan 10-15 minutes of link cleanup per post
- **Email-safe HTML requires a two-stage workflow** — the Mailpoet send modifies the post, requiring the original to be saved and restored. Easy to forget the restore step

### Editorial
- **The bold editing tension** — Maya has to decide post by post how much to edit. Sulima's boldness is authentic but can obscure emphasis when everything is bold
- **The "click here" style** — Maya likely has opinions about it but preserves it. Small ongoing friction

### Process
- **No memory between sessions** — Claude doesn't retain context. The workflow doc and project files are the institutional memory. Maya has to paste in final HTML rather than Claude reconstructing it
- **Substack import adds junk** — the "ad free" footer appears every time and must be manually removed

### Unresolved
- [INFERRED] The salon / sideshow effect conversation was not resolved during our sessions — Maya was preparing to bring the Martha Graham perspective to Sulima at lunch, but the outcome isn't captured here

---

## 7. Decisions Made and Why

### Decision: Workflow process doc should live in the project
**What:** Rather than keep the workflow in a conversation, we built a structured markdown doc that lives as a project file.
**Why:** Claude has no memory between sessions. The doc is the memory. Any future Claude instance can read `LIGHT_WAVES_WORKFLOW.md` before starting a publishing task and know exactly what to do without re-explanation.
**Lesson:** Maya invests in documentation when she can see it will save her time later.

### Decision: Email preview note should be 1-2 sentences naming the arc, not summarizing references
**What:** Early draft of the preview email summary was too long and structural ("You open with Howard Thurman's 'moments of high resolve'...").
**Why:** Maya's correction was precise — the point is to make Sulima feel the shape of what she made, not to inventory her citations. The right length is short; the right content is the through-line.
**Lesson:** For preview emails, think like a perceptive reader, not an editor making notes.

### Decision: Pixmap workaround for AITST PDF extraction
**What:** Standard PDF-to-PDF page extraction fails on the AITST interior. We switched to rendering each page as a 200 DPI pixmap, then assembling into a new PDF.
**Why:** The file reports as invalid to PyMuPDF's `insert_pdf` even though it's a valid PDF. The pixmap approach bypasses whatever structural issue is causing the rejection.
**Tradeoff:** Slightly larger file size; fully functional output.

### Decision: Preserve Sulima's bold even when it seems excessive
**What:** The editorial default is to preserve Sulima's formatting choices, including heavy bold usage.
**Why:** It's her blog. Her boldness is not poor formatting — it's how she marks what matters to her. Maya may selectively unbold when bold stops being emphasis and becomes default, but this is a judgment call made carefully, not a blanket cleanup.

---

## 8. Things I'd Tell the Next Claude

**Read `LIGHT_WAVES_WORKFLOW.md` before doing anything publishing-related.** It has everything: the sequence, the formatting rules, the link cleanup patterns, the email HTML pattern, the Substack import steps, the lessons learned. Don't skip it.

**Ask for the final HTML, don't reconstruct it.** Maya edits in WordPress after Claude produces the initial HTML. The canonical version is what she has in the editor, not what Claude remembers producing. If you need the email-safe version, ask: "Can you paste the final WordPress HTML so I can generate the email version?"

**Sulima's voice is non-negotiable. Functionality is negotiable.** If something is a voice quirk (bold, ellipses, "two&ahalf"), preserve it. If something is broken (bad link, hotlinked external image, Yahoo search URL), fix it. When uncertain, flag and let Maya decide.

**The preview email note is a craft challenge, not a summary task.** One to two sentences. Name the arc. Use the register of a perceptive reader, not an editor. Maya will rewrite it anyway, but your draft should be at the right length and in the right spirit.

**Maya is doing this as a labor of love.** There's no money in this. The 0% royalty arrangement, the bookstore consignments, the personal friendship — this is all motivated by genuine care for Sulima and for her work. The tone of the work should reflect that. This isn't a client engagement, it's a friendship that happens to involve publishing.

**The relationship with Sulima is delicate in places.** Sulima is 85 and deeply invested in her creative identity. Maya navigates editorial suggestions carefully. Don't get ahead of what Maya has authorized.

**Granola is available for meeting context.** If Maya references a conversation with Sulima or another person and you need context, Granola MCP can pull transcripts. The query "Steph Sulima meeting [date]" has worked.

**Maya's personal voice is distinct from the Lingua Ink / Sulima work.** If she switches into writing in her own voice, the register changes — more literary, more personal, emotionally engaged. Read her preferences file; she cares about craft at that level and expects Claude to engage with it seriously.

**The AITST PDF needs the pixmap workaround every time.** Don't try `insert_pdf` on it — it will fail. Go straight to the render-as-pixmap approach.

**Verify everything Sulima writes about current events.** She references deaths, holidays, recent news. Jesse Jackson died the week of the Valentine's Day post. These need to be confirmed before publishing.

---

*Generated by Claude Sonnet 4.6 · February 27, 2026 · Based on observed project context in the Light Waves publishing project*
