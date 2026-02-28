# Handoff: Pat Schoof Proposal — February 2026

---

## 1. What We Worked On Together

**Primary deliverable:** A six-page Word document (.docx) publishing services proposal for Pat Schoof, a potential Lingua Ink Media client writing a guidebook about 52 Napa Valley wineries.

**How we got there:** Steph (Maya) reached out to Pat after a mutual introduction from Jennifer Lashua (a former colleague of Steph's and a friend of Pat's). The email thread started in November 2025 and culminated in a Zoom meeting on February 13, 2026. Steph used the Granola meeting transcript to pull context before drafting the proposal.

**Scope of the proposal:**
- Typesetting / interior design
- ISBN registration
- Amazon KDP setup with SEO optimization
- IngramSpark distribution setup
- Goodreads author profile
- Contracts and copyright work
- Ebook formatting
- Author website (starting at $2,000)

**Structure:** The final proposal presented two parallel paths — self-publishing with Lingua Ink à la carte services at full pricing, versus publishing under the Lingua Ink Books imprint at approximately 25% discount. This dual-path structure was a strategic pivot from the original draft.

**Status at handoff:** Proposal completed and delivered as a .docx file. No confirmed response from Pat yet. The relationship is warm and active.

---

## 2. How Steph Works (as observed here)

**She researches before she writes.** Steph pulled the Granola meeting transcript before drafting anything — she wanted the full picture of Pat's situation, not just what was in the email thread. This is a strong signal: she's consultative by nature and wants proposals to feel personalized, not templated.

**She catches misrepresentation fast.** When the first draft said Pat had "secured the Napa Neighbors logo," Steph corrected it immediately: Pat had secured *permission to use* the logo. This isn't nitpicking — accuracy in client representation is a core value for her. She holds the work to the same standard she'd want held to herself.

**She pivots strategically, not just stylistically.** The biggest revision wasn't word-level — it was structural. Steph recognized mid-draft that the original framing assumed Pat wanted hybrid publishing, when actually Pat hadn't committed to that. The pivot to a dual-path proposal was Steph's idea and it was the right call. She thinks about how the client reads the document, not just what information is in it.

**Language matters to her — particularly the pressure register.** She flagged "we can" as too aggressive and asked for "we could" throughout. This reflects her consultative philosophy: she wants to be useful and clear, not pushy. The tone she aims for is "here's what's possible" not "here's what we'll do."

**She works iteratively and gives clear directional feedback.** When something's off, she identifies the specific problem rather than just saying "fix it." She's a collaborator, not a dictator — she'll often offer the solution herself or ask for options.

**[INFERRED]** She likely has a strong editorial background that makes her sensitive to word choice at a micro level. The "secured permission" correction and the "we can/we could" distinction both suggest someone who reads closely and thinks carefully about how language performs.

---

## 3. Tools, Systems, and Conventions

**Granola (MCP integration)**
- Used to pull meeting transcripts and notes
- Effective search query format: `"[Person A] and [Person B] [topic] [date]"` — e.g., `"Pat and Steph 52 Wineries book February 13 2026"`
- `get_meeting_transcript` function retrieves full dialogue and notes
- Granola captures detail that emails don't — Pat's specific winery permissions, her distribution strategy, etc.

**Document creation: Node.js + docx library**
- Install: `npm install -g docx`
- Brand colors:
  - `DEEP_WINE: "722F37"`
  - `WARM_GOLD: "C5A55A"`
- Tables use `WidthType.DXA` measurements (not percentages — percentages break in Google Docs)
- Content width at 1" margins: 9360 DXA
- Reusable helper functions for paragraph spacing and text formatting keep the code maintainable

**Quality control workflow:**
1. Run `scripts/office/validate.py` on the .docx
2. Convert to PDF with LibreOffice for visual preview
3. Fix layout issues (e.g., hard page breaks causing white space — solution was to remove hard breaks and let content flow naturally)

**Email / client contact:**
- Steph's email: steph@linguaink.com
- Steph's Calendly: https://calendly.com/bairey
- Lingua Ink submissions page: https://linguaink.com/submissions-and-publishing/

**Pat Schoof's contact:**
- Email: pnschoof@comcast.net

---

## 4. Preferences and Opinions

**Tone in proposals:** Consultative, warm, non-pressuring. "We could" over "we can." Respect client autonomy — present options, don't assume commitment.

**Accuracy over polish:** A factually wrong sentence in a client proposal is worse than a slightly awkward one. Steph will catch misrepresentations; better to flag uncertainty than to invent details.

**Formatting:** Professional, branded, structured — but the proposal should read like a thoughtful document, not a menu. The dual-path structure she requested is clean and comparison-friendly without being cold.

**Document delivery:** .docx for proposals (client can review and edit if needed). PDF preview for internal validation before sending.

**Length:** The Pat Schoof proposal was six pages — she wasn't cutting for brevity, she wanted it complete.

**[INFERRED]** Steph likely prefers prose over bullet-heavy formatting in her own writing (based on how she gives instructions — conversational, specific, flowing). Her personal voice is distinct from the Lingua Ink institutional voice.

---

## 5. Key Relationships and Contexts

**Pat Schoof** — Potential client / author
- Former HR executive; accomplished runner; "budding author" (Jen Lashua's words)
- Project: 52 Napa Valley wineries guidebook, organized alphabetically, covering dog- and kid-friendliness, location, discounts, hospitality, unique touches
- Has already visited all 52 wineries and documented each experience
- Has permission from all 52 wineries to feature them
- Secured rights to use the Napa Neighbors logo
- Commissioned a local map maker
- Hired a graphic designer for amenity icons
- Scheduled cover photography featuring 52 wine corks
- Distribution strategy: Meadowood, Copperfield's bookstore in Napa, hotel concierge desks (possibly winery tasting rooms)
- Connection to Steph: introduced by Jennifer Lashua (mutual friend/former colleague)
- Tone in emails: warm, enthusiastic, casual ("Zoom is fine with me :)")
- Has NOT committed to hybrid publishing — may want to self-publish and buy services à la carte

**Jennifer Lashua** — Mutual connector
- Email: runningjen@gmail.com
- Former colleague of Steph's; friend of Pat's
- Made the introduction in November 2025

**Lingua Ink Media** — Steph's company
- Offers hybrid publishing under the Lingua Ink Books imprint
- Also offers standalone à la carte publishing services for self-publishing authors
- Steph's title: Principal
- Phone: 503-847-9860
- Website: linguaink.com
- Client base is "mostly female" (per Jen Lashua's intro email)

---

## 6. Challenges and Friction Points

**The "assumed commitment" problem.** The first proposal draft was framed around hybrid publishing as the assumed path — which was wrong. Pat had expressed interest in learning about options, not in committing to Lingua Ink's imprint. The fix was architectural (restructure to dual paths), not cosmetic. This is a recurring risk in new client proposals: the temptation to assume interest equals commitment.

**Accuracy in client representation.** Steph caught a misstatement about the Napa Neighbors logo. Future drafts should be careful to represent client achievements and permissions precisely — especially in proposals where credibility is on the line.

**Hard page breaks in docx layout.** The initial document had awkward white space caused by hard page breaks inserted to control pagination. Solution: remove hard breaks and let natural content flow handle it.

**[INFERRED]** There may be ongoing tension between wanting to lead with Lingua Ink's hybrid publishing value proposition (which benefits the company more) and respecting that clients may genuinely prefer self-publishing. Steph navigates this with the dual-path structure, but it requires ongoing calibration per client.

---

## 7. Decisions Made and Why

**Decision: Restructure to dual-path proposal**
- Original: Single path framing around hybrid publishing with Lingua Ink imprint
- Revised: Two clear paths — self-publishing with full-price à la carte services vs. publishing under Lingua Ink Books imprint at ~25% discount
- Why: Pat hadn't committed to the imprint path; presenting it as the default would feel presumptuous and potentially off-putting. The dual-path framing respects her autonomy while still making the hybrid option attractive through pricing.

**Decision: "We could" language throughout**
- Original drafts used "we can" in describing services
- Changed to "we could" per Steph's direction
- Why: Softer register keeps the proposal consultative rather than assumptive. Matches Steph's relationship-first approach to client acquisition.

**Decision: Use Granola transcript before drafting**
- Alternative would have been to draft from the email thread alone
- Why: The email thread didn't capture key details (winery permissions, distribution strategy, Pat's specific progress). The Granola transcript gave the full picture and made the proposal feel genuinely personalized.

---

## 8. Things I'd Tell the Next Claude

**Always read the Granola transcript before drafting anything client-facing.** Emails are the skeleton; Granola has the muscle. The level of personalization Steph expects requires the full meeting context.

**Be precise about what clients have vs. have permission to do.** "Secured the logo" and "secured permission to use the logo" are different things. Steph reads closely and will catch it — better to get it right the first time.

**Don't assume publishing path preference.** Unless Pat (or any client) has explicitly said they want to publish under the Lingua Ink imprint, present the dual-path structure. Full-price self-publishing services vs. discounted imprint path.

**The Lingua Ink voice is professional and consultative, not salesy.** Warm, expert, respectful of client autonomy. Maya's personal voice (in her own writing) is distinct from the Lingua Ink institutional voice — don't conflate them.

**Brand colors for all Lingua Ink documents:** DEEP_WINE `#722F37`, WARM_GOLD `#C5A55A`. These should be consistent across proposals, emails headers, any branded output.

**Steph's name is Steph, not Maya** — her email signature is Steph Bairey. "Maya" appears in the project memory but "Steph" is how she signs her client correspondence. [Note: clarify with her which name to use in which context.]

**Validate before presenting.** Run the office validation script AND do a PDF preview before showing Steph any .docx. Layout issues (white space, pagination) should be caught before review, not during.

**Pat Schoof's project is further along than it might seem.** She's not in "idea stage" — she has permissions from all 52 wineries, a map, icons, cover photography scheduled, and a distribution strategy. Proposals and suggestions should meet her where she is, not treat her as a beginner.

---

*Generated February 27, 2026*
