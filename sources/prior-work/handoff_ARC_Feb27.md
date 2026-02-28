# Handoff: TDA Architectural Review Committee — February 27, 2026

---

## 1. What We Worked On Together

This project has been the ongoing operational hub for Maya's work as Chair of the Architectural Review Committee (ARC) at Tomahawk Destiny Association — a 71-home floating home community on the Willamette River in Portland, Oregon.

**Documents created or refined:**
- Monthly ARC meeting agendas (January 2026, formatting based on December 2025 template)
- Formal ARC meeting minutes (January 2026, February 2026), pulled from Granola transcripts and raw notes
- Monthly board reports (January 2026, February 2026) — short, structured Word docs submitted before board meetings
- Four violation letters for the 2023 survey follow-up resurvey (Slips #210, #446, #526, #540), formatted on official TDA letterhead template
- A comprehensive enforcement case history document for Slip #376 (Sheadel/Gonia gates + jet ski dock), used as background for consultation with former ARC members Percy Wise and Steve Bustin
- An email summary of the #376 case history
- Specific consultation questions for Percy and Steve
- Jurisdictional analysis of ARC vs. Board authority over the "Free Bench" (Tomahawk Treasures) common area
- Communications to ARC members and Board liaison Gigi Bustin about holding a members-only meeting
- Research on whether ARC meetings must be public (they don't; Board meetings do per Bylaws Article IV, Section 4)
- A ClickUp task creation for the February 14 letter-writing work session
- Enforcement standard calibration questions for the committee's private session

**Current status:** The ARC is in an active enforcement cycle. Major open items as of late February 2026: Slip #376 (jet ski dock compliance pending; gate situation clarified as approved), resurvey letters sent to Slips #210, #446, #526, #540, responses/compliance pending. Danna Herrell has been appointed to fill Mike Duncan's vacancy. Teresa Lawwill remains difficult to reach (traveling, email issues). The Free Bench/Tomahawk Treasures jurisdictional question was being handled; ARC asserting authority under Administrative Resolution #2.

---

## 2. How Maya Works (as observed here)

**Accuracy over speed.** Maya will explicitly ask to stop and correct a detail rather than accept a close-enough answer. She corrected slip numbers, owner names, co-chair titles, and letter dates multiple times — every correction was specific and right. Don't guess when you don't know something. Say "I'm not certain about this detail" and she will provide it.

**Methodical, governance-first problem solving.** When she encounters a tricky situation, Maya's first instinct is to go to the governing documents. What do the bylaws say? What does the ARC rule actually say? What does Administrative Resolution #2 actually authorize? She wants citations, not vibes.

**Collaborative before unilateral.** She consults her committee before taking positions. This shows up even in small things — when drafting a proposal to her committee, she frames it as seeking input rather than announcing a decision, even when she's clearly already decided. She is especially careful not to look like she and her husband Peter (TDA Board President) are coordinating, because they are not.

**Direct but diplomatic.** Maya knows what outcome she wants and communicates it clearly. But she's also very careful about tone in community-facing documents. She'll catch loaded language, overly harsh framing, or anything that reads as punitive rather than procedural. She prefers matter-of-fact and professional over emotional or moralizing.

**Delegation instinct.** She consistently steers monitoring and logistical tasks toward volunteers (Beautification Committee, Percy/Steve, etc.) rather than burdening her committee members. This is both practical and philosophical for her.

**How she gives feedback on drafts:** She reads carefully and marks specific corrections. She won't give vague feedback like "this doesn't feel right" — she'll say "change 'co-chairs' to remove that title, they don't currently hold that position" or "the slip number is wrong, it should be #540 not #542." When she redirects, take the exact words she offers and use them.

**Meeting notes pattern:** She provides raw notes + Granola transcript, and expects the final minutes to use the established template format (see December 2025 minutes). She wants brief context summaries for complex issues, not just action items. She wants absent members listed without special notation (just "Absent:"). She cares about the meeting time being accurate.

---

## 3. Tools, Systems, and Conventions

**Granola** — AI note-taking used at all ARC meetings. Transcripts and structured notes both available. When pulling from Granola, use `list_meetings` with `custom_start`/`custom_end` parameters (the "today" shortcut is unreliable). Pull both `get_meetings` (structured notes) and `get_meeting_transcript` (full transcript) — they contain different and complementary detail.

**ClickUp** — Task management. Maya has a "Tomahawk Destiny" project within her workspace. The relevant list ID is `901318968458`. Custom field UUIDs (extracted from existing tasks to avoid guessing):
- Project field: `9f921ca1-1b45-4b49-a463-a550287cc5b2`, Tomahawk Destiny value: `226fe75e-8c30-4a59-ac6c-82cf375c5e55`
- Effort: `5db96854-9117-4857-8306-6f740ec31c3e`
- When adding tasks, examine an existing task first to extract all custom field UUIDs rather than querying field definitions (more reliable).

**Airtable** — Was being implemented as the tracker for ARC requests and decisions. Login credentials were sent to committee members via email. Not heavily used in this project context yet. Will move tracking to the new website she is building, in March 2026.

**TDA letterhead template** — Stored as a .docx file. Uses Playfair Display font, 11pt body text, 720-point left indentation, BodyText paragraph style. Has header/footer graphics that must be preserved when generating new documents. When creating violation letters, the workflow is: unpack the template, replace placeholder content in `document.xml`, preserve all `<w:sectPr>` (contains header/footer references), repack with `--original` pointing to the source file. XML special characters must be escaped (`&` → `&amp;`, `<` → `&lt;`).

**Meeting minutes format** — See the December 2025 ARC Minutes as the canonical template. Structure: bold header block with date/time/attendance, bold section titles with bullet sub-items for substantive discussion, **Action Items** section at end listing person responsible and task, adjournment time. Font is Calibri. Minutes in this project are stored as actual Word XML, not plain text with .docx extension.

**Board reports format** — Short, structured. Sections: Membership, Completed, In Progress, Upcoming, Support Needed (or "none at this time"). Calibri 11pt, bold inline section headers, moderate spacing. About one page. Due before the monthly board meeting (usually held last week of month).

**Governing document stack (in order of precedence):**
1. TDA Bylaws
2. TDA Rules and Regulations (amended January 24, 2011)
3. ARC Rules (Most Recent Approved version in project files)
4. Administrative Resolution #2 (governs common area appearance authority)
5. Portland City Code Title 28 (relevant to floating home structures)

**Zoom link for ARC meetings:** `https://us06web.zoom.us/j/9927228163?pwd=VDNaOW8wMFZpcWh0UnlVWFB1NTZIZz09`

**Community website:** Bill Bowling is the webmaster. ARC posts approval notices to both the bulletin board and website for the required 7-day community review period.

**Address format for violation letters:** N Tomahawk Island Drive, Portland, OR (specific house numbers correspond to slip numbers — confirm with Maya, don't assume).

---

## 4. Preferences and Opinions

**Document formatting:**
- Word docs over markdown for any official or formal deliverable
- Calibri font for ARC documents (not Times, not Arial for formal docs)
- Playfair Display on official TDA letterhead — preserve it, do not change it
- US Letter size (not A4 — always set explicitly in docx-js)
- Clean, simple formatting. No decorative elements, no excessive headers in board reports
- Brief reports preferred. She will explicitly ask for brevity and edit down anything that runs long

**Communication style:**
- No "I" in committee communications — "the committee" or collective voice
- No "we" before checking with committee members
- No loaded language in enforcement letters (e.g., "deliberately ignored" — don't write that)
- Tone of enforcement letters: matter-of-fact, procedural, not punitive or moralistic
- Professional but not stiff. She navigates this well herself; follow her lead when editing

**What she finds unhelpful:**
- Guessing at details (slip numbers, names, dates, titles) instead of flagging uncertainty
- Over-explaining process in committee documents
- Vague or generic feedback responses
- Anything that could embarrass the committee if forwarded or seen publicly

**What she responds well to:**
- Specific, accurate citations from governing documents
- Options presented for her to choose between
- Drafts that are close but know where their own gaps are
- Fast iteration — she'll make specific corrections and expects them applied immediately

**[INFERRED]** Maya has a strong instinct for optics and perception management. She thinks several steps ahead about how a document will land with different audiences (the resident who receives a violation letter, the broader community who might see it, the board who reviews ARC actions). This shapes both her language choices and her governance decisions.

---

## 5. Key Relationships and Contexts

**Maya (Steph) Bairey** — ARC Chair. Maya goes by both Maya and Steph in different contexts; the meeting minutes use "Steph Bairey" as her formal name. She's been at TDA about 19 months.

**Peter Bairey** — Maya's husband, TDA Board President. The "power couple" optics are something Maya is acutely aware of and actively manages. She emphasizes ARC independence from Board influence.

**Sylvia Davids** — ARC Secretary. Reliable, present at most meetings.

**Kate Brinkley** — ARC member. Handles bulletin board postings, resident outreach (contacting Munnelly about Patterson's drawings, etc.), and website coordination with Bill Bowling.

**Teresa Lawwill** — ARC member. Has had persistent email access issues (iPhone setup problems). Has been traveling (Panama as of January 2026). Not reliable for near-term communication.

**Danna Herrell** — Newest ARC member (Slip #380), appointed to fill Mike Duncan's vacancy. Board approved her appointment January 26, 2026. Kate is helping onboard her.

**Mike Duncan** — Resigned from ARC. Had expressed disinterest in serving before formally resigning.

**Gigi Bustin** — TDA Board liaison to ARC. Has historical knowledge of rules and community context; her husband Steve Bustin is a former ARC co-chair. She was being somewhat disruptive to the committee's decision-making process ("hijacking" meetings was Maya's word). Maya managed this through the members-only meeting decision.

**Percy Wise** — Former ARC co-chair. Major institutional knowledge resource. Maya consults him for historical files, enforcement letter templates, rule interpretation on edge cases like the #376 situation.

**Steve Bustin** — Former ARC co-chair (Gigi's husband). Also a historical knowledge resource. It was Steve/Percy who clarified that the 36-inch height rule applies specifically to structures 48-60 feet from the walkway — a key ruling that changed the #376 gate analysis.

**Bill Bowling** — Community webmaster. Handles ARC posting to website. There have been ongoing issues with outdated contact information on the site.

**Don Gire** — Placed property boundary pins at Slip #376. Three green pins: only the outer two mark actual slip boundaries (the inner one does not). This is critical context for the jet ski dock encroachment measurement.

**Tracy Gonia / Jeff Sheadel** — Owners at Slip #376. The long-running enforcement case. Gates installed without ARC approval; jet ski dock encroaches ~3 feet beyond slip boundary.

**Property owners with outstanding violations:**
- Slip #210: Anderson
- Slip #446: Kaplan
- Slip #526: Rosebery
- Slip #540: Wiley

---

## 6. Challenges and Friction Points

**The #376 case has been dragging since at least June 2025.** The complexity: gates were installed without approval, but the specific height rule (36" rule) turned out to apply only to structures 48-60 feet from the walkway — the gates are 10-15 feet from the walkway. Gate situation was ultimately resolved as approved. Jet ski dock encroachment is clearer and actionable. Two previous ARC committees sent warning letters; current committee needs to access those historical records.

**Document handoff from previous committee was poor.** Maya has been working to locate historical files — prior enforcement letters, old survey notes, institutional knowledge — that weren't properly transferred when leadership changed. Percy and Steve have been the workaround.

**Teresa's email situation is an ongoing operational friction point.** It's been unresolved since September 2025. She's abroad.

**Jurisdictional ambiguity between ARC and Board** keeps surfacing. The Free Bench/Tomahawk Treasures situation was one instance. Maya's consistent approach is to go to the governing documents and establish clear written authority before acting.

**Optics of the Bairey leadership dynamic.** Maya and Peter both leading major governance positions this early in their tenure creates real and perceived risks. Maya is thoughtful about this, but it requires extra care in how decisions are framed and documented.

**Consistent enforcement standards haven't been fully established yet.** The February 15 members-only meeting was specifically to address this — developing internal consensus on thresholds for violations like peeling paint, structural deterioration, deck maintenance before applying them uniformly across properties.

---

## 7. Decisions Made and Why

**Gates at #376 ultimately approved, not cited.** The committee initially drafted an enforcement letter about gate height, but after consulting Percy and Steve discovered that the 36-inch visual obstruction rule applies specifically to structures 48-60 feet from the walkway (protecting view corridors at the river end of slips). The gates are only 10-15 feet from the walkway, outside that provision. The committee concluded the gates didn't violate the specific height rule, and the broader "prior written approval" violation was addressed. Alternative considered: cite the Section 1 and Section 3 general approval requirement regardless. Decision: gates approved; jet ski dock remains actionable.

**Exclude Gigi from one ARC meeting.** Rationale: Gigi was disruptive to committee decision-making. Research confirmed no legal requirement for ARC meetings to be public. Decision framed publicly as "team bonding" for the new committee. Alternative considered: continuing to include her and managing dynamics in-meeting. Decision: private meeting to develop internal enforcement standards before applying them. The messaging was intentionally diplomatic and Gigi was informed respectfully.

**Resurvey the top 5 violation properties before escalating.** The 2023 survey flags were old. Board requested current status. Decision: in-person resurvey before sending any new letters or escalating to board enforcement. This also allowed the committee to document remediated violations and give credit for improvements — a more defensible and fair approach. Survey happened February 9, 2026. Letters followed.

**Consult Percy/Steve before finalizing #376 letter.** Multiple times the committee chose to hold the letter pending their input rather than send something that might be wrong. Maya explicitly values getting it right over getting it out fast.

**[INFERRED] Move ARC to online forms.** Mentioned as "upcoming" in the February 2026 board report. Likely intended to reduce the friction of residents submitting requests informally or incompletely (see the Patterson/218 situation where drawings were missing).

---

## 8. Things You'd Tell the Next Claude

**On names:** Maya goes by both "Maya" and "Steph" — her formal name in meeting documents is Steph Bairey, but she may introduce herself as Maya in conversation. Don't assume which she's using in a given context.

**On slip numbers:** Always verify slip numbers before including them in documents. She has caught wrong slip numbers (#542 vs #540, #218 vs other confusion) multiple times. If you're generating violation letters or case references, confirm the number explicitly.

**On the letterhead template:** It's a real XML document with Playfair Display font and specific header/footer graphics. You cannot just drop content into it as a text replacement — you need to unpack, carefully edit document.xml, and repack using `scripts/office/pack.py --original [source]`. The BodyText paragraph style must be preserved. Test with validation before delivering.

**On Granola:** Use `list_meetings` with explicit date range parameters. Pull both the structured notes and the full transcript. The transcript catches things the structured notes miss.

**On the #376 case:** This is legally nuanced. The gate violation analysis changed significantly after Percy/Steve consultation. The current status is: gates approved/resolved, jet ski dock enforcement pending compliance. Don't reopen the gate question. Don't conflate the two sub-issues.

**On the board report format:** Maya likes it short. One page. Bold inline section headers. If she hasn't said she needs support, write "Support Needed: None at this time."

**On Percy and Steve:** They are former co-chairs (not current). Don't add titles. They're consulted informally as institutional knowledge, not as official committee members.

**On enforcement letter tone:** These letters go to neighbors and community members. The tone should be professional, procedural, and neutral. Avoid any language that sounds punitive, accusatory, or emotionally loaded. Maya will catch it and ask you to revise.

**On the power couple dynamic:** Maya is very aware that she and Peter hold the two top positions in TDA. She actively works to ensure ARC decisions appear independent and fact-based. Don't write anything that would reinforce the perception of top-down coordination between the Board and ARC.

**On governing document citations:** When she needs a rule citation, go to the actual documents in the project. The key docs are: TDA Bylaws, TDA Rules and Regulations, Current ARC Rules, Most Recent Approved ARC Rule (they're slightly different documents — check both). Don't paraphrase rules; quote the specific language.

**On her working style:** She is efficient and specific. She will give you the exact correction she wants, and she expects it applied precisely. She appreciates when you flag your own uncertainty ("I'm not sure of this slip number — can you confirm?") rather than guessing. She works iteratively and doesn't need long explanations of what you did — just deliver the document.
