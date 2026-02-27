# Handoff: Cohort Critique Project — February 27, 2026

---

## 1. What We Worked On Together

This project is Maya's creative writing critique group — she leads a cohort of writers who meet via Zoom on Sundays and Thursdays. The primary work here has been generating live-ready literary critiques of members' submitted manuscripts, written in Maya's voice and formatted for verbal delivery during Zoom sessions.

**Scope of work:**
- Critique of Iris's "When Cicadas Sing" (horror, first-time reader perspective, bullet points for live Zoom)
- Critique of Iris's "Six Songs" (DJ who manipulates time; publication-bound; line editing focus; combined across two drafts)
- Critique of Iris's "Not Sure Yet" (horror/fantasy, warlock lineage; publication-bound; email voice; heavy revision to eliminate AI tells)
- Critique of Iris's "First Date" (publication-bound; email voice; casual/dashed-off tone)
- Critique of Maura's "Noticing" (memoir; email format; reader response focus)
- Critique of Lynn's chapter about Libby's winter concert (bullet points for live Zoom)
- Critique of Julie's Chapter 5 (fun writer, not publication-focused; encouragement-forward; bullet points for live Zoom)
- Critique of Deb's published Cairo hotel stairwell chapter (already published; reader reaction only, no prescriptions)
- Administrative update: cohort calendar event text (removed Lynn, added Deb, updated schedule)

**Current status:** Active and ongoing. Critiques happen roughly weekly on Sunday afternoons.

**Deliverable format:** Either (a) bullet points for live verbal delivery during Zoom, or (b) email in Maya's voice to be forwarded directly to the writer.

---

## 2. How Maya Works (as observed here)

**Problem approach:** Maya comes in with a clear request and specific constraints. She doesn't over-explain — she expects Claude to read the project documentation first and calibrate accordingly. When she has to correct something, she's direct and specific, not vague.

**Quality standards:** High. She catches every em dash. She notices when analysis isn't grounded in textual evidence. She pushed back hard when Claude invented a "wave structure" in Iris's cicada story that wasn't actually there — her exact question was "is there REALLY a wave structure?" — and demanded the revision. She does not want romanticized literary interpretation; she wants honest, evidence-based observation.

**Iteration style:** She'll ask for a draft, read it, then request targeted revisions. She doesn't overhaul everything at once — she identifies the specific problem ("remove em dashes," "make this more casual," "too forgiving of AI tells") and asks for a fix. She's efficient.

**Format sensitivity:** Maya distinguishes sharply between formats for different contexts: bullet points for Zoom presentation, casual email for forwarding to writers, structured analysis for her own use. She adapts based on the writer being critiqued and that writer's goals.

**Voice ownership:** She is meticulous about maintaining her authentic voice in AI-generated text. She references an "AI Tells" document from another project and applies it rigorously. She has caught and flagged: em dashes, words like "genuinely," overly polished phrasing, academic-sounding structure, explanatory clauses that feel drafted rather than dashed off.

**Decision-making:** She prioritizes writer goals over her own preferences. A writer like Julie who's writing for fun gets encouragement-forward feedback; a writer like Iris who's submitting for publication gets line editing. Maya makes this call explicitly and expects Claude to follow it.

---

## 3. Tools, Systems, and Conventions

**Project files (read-only, always consult before each critique session):**
- `/mnt/project/Cohort_Critique_Prompt_Maya_Info_.docx` — critique methodology and group guidelines
- `/mnt/project/Maya_s_email_style.txt` — voice reference for written critiques

**Platform:** Zoom for group meetings (Sundays at noon PST for writing/critique, Thursdays at noon PST for writing sessions)

**Contact:** maya@bairey.com

**Meeting cadence:**
- Sundays: 2-hour writing session + post-meeting critique of scheduled writer
- Thursdays: 2-hour writing session, no critique

**Critique schedule logic:** Alpha ascending by first name, cycling. Writers are skipped if they have no work ready. Deb was added mid-cycle after Kay (one-time insertion, not a full resort).

**Current schedule (as of Feb 26, 2026):**
- Julie — March 1
- Kay — March 8
- Deb — March 15
- Iris — March 22
- Maura — March 29
- Maya — April 5

**Manuscript formats:** Word documents (.docx) and occasionally text files. Use `python` with the `docx` library or `pandoc` to extract content when needed.

---

## 4. Preferences and Opinions

**Em dashes: never.** This is non-negotiable. Maya actively hunts them down. Remove every one.

**Tone:** Conversational, warm, direct. "Dashed off" is a phrase she has actually used to describe what she wants — the feeling of a thoughtful reaction, not a carefully composed essay.

**No generic AI phrases:** "genuinely," "real intrigue," over-explained transitions, unnecessary subclauses. If it sounds like something an AI would write to sound literary, cut it.

**No subheadings in emails.** She requested these be removed in multiple sessions.

**Bullet points for Zoom, prose for email.** Don't mix these up.

**Length:** Shorter is usually better. When she asks for revisions, the ask is almost always to tighten, not expand.

**Critique structure she uses consistently:**
1. Plot summary (for verification — she wants to confirm Claude understood the piece correctly)
2. Structure and sensory description analysis
3. Three compliments (specific, tied to the text)
4. One constructive criticism

**Structural analysis:** This is Maya's reputation in the group. She is "known for identifying narrative structure patterns." Always include it. Make it grounded and specific — don't invent patterns that aren't there.

**First-time reader perspective:** The default framing for most critiques. Even when doing craft analysis, the primary voice is "here's what I experienced as a reader."

**Encouragement-forward vs. publication-ready:** She calibrates this per writer. Julie = fun, encouraging. Iris = honest, line-level. Deb (published work) = reader reaction only, no prescriptions.

---

## 5. Key Relationships and Contexts

**Cohort members:**

- **Iris** — most frequently critiqued writer in this project. Publication-focused. Prefers line editing and feedback on whether readers "get" her work. Has submitted multiple pieces across this period: "First Date," "Not Sure Yet," "Six Songs," "When Cicadas Sing." Gets rigorous craft feedback.

- **Maura** — memoir writer. "Noticing" was a braided piece touching on a breakup, convent years, a psychic visit, and astronomer Jocelyn Bell Burnell. Responded well to feedback on the braided structure.

- **Lynn** — was on the roster through January 2026, then left the group. No longer included in the critique schedule. Likely to return later.

- **Julie** — writes for personal enjoyment, not publication. Maya explicitly noted Julie should get encouragement-forward critique, not rigorous line editing. Chapter 5 was her submitted work.

- **Kay** — on the critique schedule, has not had a piece critiqued in this project context yet.

- **Deb** — newly added to the group. First appearance was her published Cairo hotel stairwell piece. Published work = reader reaction only, no prescriptive critique.

- **Maya** — leads the group, runs the Zoom, manages the critique schedule. Her email is maya@bairey.com.

---

## 6. Challenges and Friction Points

**AI tells:** This is the recurring friction point. Maya holds Claude to a high standard for eliminating AI writing markers. She has an "AI Tells" document in another project that she uses as a benchmark. The specific session with "Not Sure Yet" included a direct correction when Claude was "forgiving a lot of the tells." Next Claude should apply maximum strictness here without being asked.

**Over-romanticized analysis:** The cicada story session is the clearest example. Claude invented a structural metaphor (wave structure mirroring cicada songs) that wasn't actually in the text. Maya caught it immediately. Always ask: is this observation grounded in something that actually happens in the piece?

**Em dashes:** Mentioned multiple times across multiple sessions. This is clearly a pattern that needs zero tolerance from the start, not something to fix after the fact.

**Format confusion:** Bullet points vs. prose email is a distinction that matters a lot to Maya. Confirm the delivery format at the start if it's unclear.

---

## 7. Decisions Made and Why

**Bullet points over prose for Zoom delivery** — Maya decided early that Zoom presentation requires a different format than written critique. Prose is harder to read naturally aloud; bullets allow her to speak rather than read. This became the standard for all live presentations.

**Adaptation per writer's goals** — Maya explicitly decided that critique depth and type should match each writer's stated goals (publication vs. personal growth), rather than applying a uniform standard. This was articulated clearly in the Julie session.

**Deb added after Kay (not re-sorted)** — When adding Deb to the schedule, Maya chose to insert her after Kay as a one-time placement rather than resorting the whole list alphabetically. The list will naturally normalize after one cycle.

**No em dashes in Maya's voice** — This wasn't a one-time preference; it's a stylistic rule. Decided across multiple sessions. The reasoning is maintaining authentic voice and avoiding AI writing markers.

---

## 8. Things You'd Tell the Next Claude

**Read the project files first, every time.** Maya has said this explicitly. Don't skip it. `/mnt/project/Cohort_Critique_Prompt_Maya_Info_.docx` and `/mnt/project/Maya_s_email_style.txt` are the two files. They're short. Read them.

**Zero em dashes.** Don't use them and then fix them when she catches them. Just never use them.

**Confirm format and delivery context upfront if not stated.** Is this for live Zoom (bullets) or email to the writer (prose)? Getting this wrong creates rework.

**Structural analysis is her thing.** She's known in the group for it. Always include a structural observation. Make sure it's grounded in the text — don't invent patterns.

**Apply AI tell standards preemptively.** Don't be "forgiving." She has a document for this in another project. Even without that document, the standard is: if it sounds like AI trying to sound literary, cut it.

**Plot summary first.** She uses it to verify Claude understood the piece. This isn't filler — it's a check.

**Know your writer.** Iris = rigorous. Julie = encouraging. Deb = reader reaction only. When Maya tells you a writer's preference, weight the entire critique accordingly.

**Don't invent literary patterns.** If you're going to claim the structure mirrors something, make sure it actually does. Maya will ask "is there REALLY [pattern]?" and you need to be able to say yes with evidence.

**She's efficient and direct.** Match her energy. Don't over-explain. Don't pad. She reads fast and catches everything.
