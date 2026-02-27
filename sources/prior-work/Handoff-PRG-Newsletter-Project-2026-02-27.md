# Handoff: PRG Newsletter & Granny Tech Work — February 27, 2026

---

## 1. What We Worked On Together

This project context spans roughly 10 weeks of collaboration (January–February 2026), centered on Maya's volunteer technical work for the Portland Raging Grannies (PRG) and, increasingly, the international Raging Grannies network.

**Weekly Newsletter Production** is the core recurring work. We've built at least four complete HTML newsletters together (February 5, February 12, February 19, February 26, 2026), each pulling content from Gmail, applying editorial judgment, and producing final HTML ready to paste into Gmail for distribution. The workflow has become genuinely collaborative — I read email, draft items, make editorial calls, and Maya reviews and corrects. Each newsletter runs 12–14 items.

**Style Guide Creation**: Around February 12, after the newsletter workflow was working well, Maya requested we formalize the editorial knowledge into a proper written style guide. That document now lives in the project files as `portland-raging-grannies-style-guide.md`. It covers both the editorial approach (voice, ordering, handling high-volume contributors, item types) and the HTML format (exact templates, character entities, link conventions). This was explicitly about building documentation that doesn't rely on Maya being the only person who knows things.

**Logo Redesign Presentation**: We built a 13-slide PowerPoint presentation proposing replacing the umbrella in the PRG logo with a protest sign. Delivered as a self-contained PPTX file using PptxGenJS. Maya sent it to the group; the professional quality exceeded expectations. [Status: sent, awaiting group feedback as of late February 2026.]

**International Raging Grannies Web Transition**: Maya took over as Web Granny for the international network (raginggrannies.org and raginggrannies.net) when Connie Peabody stepped down. Tasks included: decoding obfuscated email addresses from the locations page (Cloudflare XOR encoding), merging contact lists (110 contacts), drafting a volunteer recruitment email to 80+ gaggles, reviewing a Song Site Librarian job description from Vicki, and creating ClickUp tasks from meeting notes. A staging site (staging.raginggrannies.org) is in progress; target completion was March 2026.

**Administrative Support**: Meeting minutes (January 17 general meeting, 35 attendees, from Zoom transcript), contact database updates (identifying 11 missing contacts from roster comparison), gaggle.email login instructions for two team administrators (Natalie Reich, Social Team; Kathy Pinsonault, Gender Equity Team).

**Current Status as of Feb 27, 2026**: Newsletter workflow is smooth and weekly. International site migration is in progress, deadline March 2026. Logo redesign is with the group. Volunteer recruitment for international roles is ongoing; Maya is matching volunteers to specific roles by mid-March.

---

## 2. How Maya Works (As Observed Here)

**She has strong editorial instincts and doesn't need to be convinced.** When she disagrees with a draft choice, she says so directly and specifically. "The attribution is wrong — it's Abby Ross, not Gordon Adams." "Karen's husband is David, not Russ." She doesn't soften corrections, which is actually a gift because you know exactly what to fix.

**She prioritizes accuracy over speed.** She has explicitly said she'd rather flag a gap than fabricate. When I have incomplete information (a missing URL, an uncertain detail), she wants me to call it out rather than approximate. She catches small inaccuracies — wrong names, wrong dates — consistently.

**She's iterative and hands-on.** She doesn't hand off a task and wait for a finished product. She reviews as we go, provides targeted course corrections, and shapes the work in real time. This is efficient once you understand it: expect feedback after each draft section, not just at the end.

**She thinks systemically.** A single newsletter correction often leads to "let's update the style guide." A one-off task (creating login instructions for Natalie) generates documentation (the HTML email template approach) for future use. She's always building for sustainability.

**She's managing a cognitive load issue she rarely talks about directly.** [INFERRED] The newsletter takes several hours. The international web role was added on top of existing PRG technical work on top of running a professional consulting practice. When she says "I don't have time for X right now," that's a real constraint, not negotiation.

**She gives clear creative direction by example and correction rather than upfront specification.** She'll say "I don't want it to sound this formal" after seeing a draft, rather than specifying tone requirements in advance. This means first drafts sometimes need one pass of adjustment, which is normal and fine.

**She responds well to options when there's genuine ambiguity.** If I flag a choice and present alternatives, she makes a decision quickly. She does not like being asked to make decisions about things that I should just be able to decide myself.

**She expects me to maintain context across a session.** If she says "handle Joana's items the same way we did last week," she expects me to remember that pattern, not ask her to re-explain it. If I've lost context, it's better to do a conversation_search and come back than to ask her.

---

## 3. Tools, Systems, and Conventions

### Gmail
- **Primary newsletter label**: `PRG-Newsletter` (sometimes `PRG/Newsletter` — both work, but the former is more reliable in API searches)
- **Secondary label for international work**: `PRG-Webgranny`
- **Newsletter submission addresses**: `grannynewsletter@gaggle.email` and `grannynewsletter@gmail.com` (both route to Maya)
- **PRG general address**: `pdxraginggrannies@gmail.com`
- **Maya's personal address**: `stephbairey@gmail.com` (some contributors send here directly)
- **Multipart/related emails**: emails with embedded images often fail to parse body text through the Gmail API. Fall back to snippet; ask Maya for full content if critical.
- Starred emails in the Webgranny label = volunteer responses worth reading

### ClickUp
- **Master Task List ID**: `901318968458`
- **Custom fields for Raging Grannies tasks**:
  - Project: `48dfc203-1c7a-4fbd-8d3b-4ef845159629` (= "Raging Grannies")
  - Effort: `91613c05-d60f-4da0-afa4-9ddbd27bb9b8` (= "Small")
  - Revenue: `7ab3a7e0-1fc2-4074-b353-db128d792628` (= "None")
  - Scope: `e06f82ab-ba76-4a87-8583-0b4d54caf938` (= "External")
  - Approach: `c5f38d05-209f-4525-9b69-e14af13552c8` (= "Indifferent")
  - Readiness: `f297da50-a58f-41a3-8124-f588cf1fe6cc` (= "Prepared")
- Task names always start with a lowercase verb: "review song librarian job description from Vicki," not "Song Librarian Job Description Review"
- Due dates are never left blank — always ask if no date is given

### Newsletter HTML
- **Container**: exact `div.items` structure with inline styles — do not deviate
- **Colors**: title/headline `#d6616c` (coral-red), header `#bd3435` (darker red)
- **Paragraph breaks**: `<br/>\n<br/>` — exact, no spaces in tags
- **Links**: `&raquo;` prefix, contextual text ("» Read the meeting notes" not "» Read more" when avoidable)
- **Special characters**: `&raquo;`, `&hellip;`, `&amp;` — no em dashes, no `--`
- **Attribution line**: "From: First Last" followed by `<br/><br/>`
- **Compiled/rollup items**: name in title, no "From:" line in body
- **Table of contents**: headlines must exactly match body headlines, same order
- The newsletter logo image URL: `https://portland.raginggrannies.org/wp-content/uploads/2025/06/prg-newsletter-logo.jpg`

### WordPress Sites
- `raginggrannies.org` — international site (Maya now manages)
- `raginggrannies.net` — song archive (Maya now manages)
- `staging.raginggrannies.org` — staging for redesign (in progress)
- Hosting: FastComet (previously on Connie's card, which expired Jan 30, 2026; paid through March 2027 at $670 biennial; Maya plans to migrate to reduce to ~$288 biennial)
- Song archive workflow: Web Granny creates user accounts via cPanel/phpMyAdmin → users post at raginggrannies.net/publish/ → dashboard at raginggrannies.net/dashboard/

### Gaggle.email
- Moderated email list platform used for PRG distribution
- `granny-newsletter@gaggle.email` = the newsletter distribution list
- Supports magic link login (no password required — good for non-technical admins)
- Admins who needed login help: Natalie Reich (Social Team), Kathy Pinsonault (Gender Equity)

### Contact Database
- Stored as CSV with specific multi-field structure (name, phone type, address, PRG group label)
- Has many tabs in Google Sheets roster
- Website intake sends data to this roster
- When adding contacts, exact field structure must be replicated — no invented fields

### Team Distribution Lists
- `prg-enviro-team@gaggle.email` — Environment
- `prg-gender-team@gaggle.email` — Gender Equity
- Other teams: Racial & Immigration Justice (RIJ), Social Equity, Grannies Against Gun Harm (GAGH)

---

## 4. Preferences and Opinions

**Formatting**: No bullet points in newsletter body text. Prose over lists everywhere except actual list-format content. Em dashes: never. Double hyphens: convert to single dash. Ampersands in HTML: always `&amp;`.

**Link text**: Contextual and specific. "» Register on Eventbrite" beats "» Read more" every time. Bare URLs as visible text are acceptable only when grannies need to copy-paste the address.

**Voice**: "Grannies talking to grannies" — warm, direct, not preachy, not sanitized. If the source said "fascist violence," keep "fascist violence." Don't soften political language.

**Attribution**: Always use full names on first mention. Don't paraphrase personal shares — preserve the contributor's exact voice.

**Meeting notes**: Keep them informal if that's how they came in. Don't "professionalize" them. Bold agenda topic headers for scannability but otherwise leave tone alone.

**Organization preferences**: Accuracy over speed. Flag gaps rather than fill them with guesses. Ask before inventing.

**What she finds annoying**: Generic responses that don't engage with the specific content. Being asked to make decisions I should handle myself. Excessive explanation after delivering a file. Asking her to re-explain patterns that were established earlier in a session.

**Aesthetic sensibilities**: Clean, functional, no unnecessary flourish. The newsletter should look professional but not corporate.

---

## 5. Key Relationships and Contexts

**Portland Raging Grannies (PRG)** — Maya's local gaggle. She's been a member since 2020 (joined at 50). She is the tech granny: manages email lists, website, Zoom account, PayPal, Google Drive, and the weekly newsletter. The Grand Grannies (rotating two-person leadership role) depend on her for meeting agendas and minutes.

**Regular newsletter contributors**:
- **Joana Kirchhoff** — Environment Team lead, high-volume contributor. Many items are nice-to-know (compile into rollup); items about specific PRG actions get their own entry. Always goes last in the newsletter.
- **Karen Fletcher** — frequent contributor across topics; has direct connections to events she shares
- **Lynne Backman** — often sends agenda and meeting reminders
- **Megan Esler** — team leadership updates, organizational news
- **Alice (Ali) Shapiro** — personal reflective pieces; preserve her exact voice
- **River Montijo** — contributor

**International Raging Grannies Network**:
- **Connie Peabody** (Salem, OR) — outgoing Web Granny; built much of the current infrastructure; provided extensive OneNote documentation of the role
- **Vicki** — stepping down from Song Site Librarian role; drafted job description
- **Kathy Russell** (kaethy@gmail.com, Metro Detroit gaggle, 248-786-7342) — original WordPress site builder; still has admin access; agreed to handle technical Song Site Web Granny tasks
- **Cathy Turnbull** — IT project manager; potential future tech volunteer; flagged for Un-convention Zoom setup
- **Mary** — sent International RG Gmail account details to Maya

**General organizational structure**: 80+ autonomous gaggles across North America and internationally (Ireland, Scotland). No central authority. International website and song archive are shared infrastructure, not governance.

---

## 6. Challenges and Friction Points

**Email parsing failures**: Multipart/related emails (with embedded images) often return empty bodies through the Gmail API. Workaround: use the snippet, or ask Maya to paste the content directly.

**Inconsistent contributor behavior**: Most contributors don't use the designated newsletter email address consistently. Some send to Maya's personal email, some to the full member list. Maya has to manually forward and curate. This means the Gmail label search alone doesn't capture everything — Maya sometimes provides content directly in the session.

**Volume from Joana Kirchhoff**: She sends a lot. The rollup system manages this, but it requires editorial judgment every week about what rises to a standalone item vs. gets compiled. The threshold is whether PRG is taking group action vs. an individual granny might choose to engage.

**Late submissions**: In at least one session (Feb 26), substantive items were still arriving at 2pm on the day the newsletter was due. This creates real-time editorial decisions.

**Staging site migration**: Still in progress as of Feb 27. Has demo content that needs to be stripped. Timeline is tight (target: March 2026).

**Hosting payment**: Connie's card expired January 30, 2026. Hosting is actually paid through March 2027, so no immediate crisis — but the payment method on the FastComet account needs to be updated. [As of Feb 17, this was still a ClickUp task, not yet done.]

**Volunteer coordination complexity**: Maya is trying to match ~8 volunteers to specific technical and non-technical roles for the international network. The volunteer offers vary widely in skills and availability. Getting the right person to the right role without overwhelming anyone is genuinely complex.

**Maya's bandwidth**: She charges $300/hour for this work commercially and does it all for free. She's already at 40% volunteer workload. The international role was added reluctantly. She's building systems so this doesn't collapse if she can't maintain it — but that takes time she also doesn't have.

---

## 7. Decisions Made and Why

**To compile Joana Kirchhoff's items rather than giving each its own entry**  
Decision: Multiple Joana items → one compiled rollup section, always last in newsletter  
Alternatives: Give each its own entry (bloats newsletter, buries other content); drop some entirely (loses potentially useful info)  
Reasoning: The rollup respects both the contributor's engagement and the reader's attention. The "full item" threshold is specifically about group action vs. individual choice.

**To create a formal style guide rather than just doing the newsletter each week**  
Decision: Formalize the accumulated editorial knowledge into a written document  
Timing: Made around Feb 12 newsletter session  
Reasoning: Maya explicitly said the newsletter used to take her "several hours" manually. The style guide captures institutional knowledge so it doesn't have to be re-explained, and makes the role potentially transferable to other volunteers.

**To replace the umbrella with a protest sign in the PRG logo**  
Decision: Maya proposed this change, prepared a full presentation  
Reasoning: The umbrella symbol dates to the original 1987 origin story (nuclear umbrella protest) and doesn't reflect what the Portland group actually does. A protest sign better represents their street activism. The presentation was strategic: show the exciting multicolor versions first, then explain rationale.

**Maya decided to take on the international Web Granny role herself rather than wait for a volunteer**  
Decision: Interim Web Granny while recruiting  
Alternatives: Wait for a volunteer before starting work (risks site degrading while Connie is unavailable)  
Reasoning: Maya's own words — "I'm literally the only international granny with these skills." She could reduce hosting costs and set up a more sustainable infrastructure than currently exists. She framed it as a temporary transition role, not permanent, but it appears to have become permanent now.

**To use staging.raginggrannies.org rather than rebuilding from scratch**  
Decision: Continue with the staging site Connie and Maya had already started  
Alternatives: Full rebuild on new platform; incremental updates to live site  
Reasoning: Faster to finish an in-progress staging site than start over. Reduces risk of breaking the live site during transition.

**To build the ClickUp task names starting with lowercase verbs**  
Decision: Consistent naming convention enforced from the first batch of tasks  
Reasoning: Maya's explicit instruction. Action-oriented naming makes the task list immediately scannable — you can see what you need to do, not just what the topic is.

---

## 8. Things I'd Tell the Next Claude

**Read the style guide before starting any newsletter.** It's thorough and was built from real editorial decisions. The HTML section especially — the exact container structure, character entities, and link format conventions are non-negotiable.

**The Gmail label is `PRG-Newsletter`, not `PRG/Newsletter`** — or try both. The slash variant sometimes works, sometimes doesn't, depending on how the label was created in Gmail.

**Watch for multipart/related emails.** If a message body comes back empty and it came from someone who usually sends substantive content, it probably has an embedded image. Use the snippet or ask Maya.

**Joana Kirchhoff items are always compiled into a rollup section that goes last.** Unless the item is specifically about a PRG group action or requires member decision-making. "PRG was invited to sing at X" = standalone. "Here's a petition you might want to sign" = rollup.

**Do not fabricate details.** If you don't have a URL, say you don't have a URL. If an attribution is uncertain, flag it. Maya will correct you if you guess wrong and she remembers. Better to surface the gap.

**Maintain session context aggressively.** If Maya says "handle it the same way we did the Joana items last time," do a conversation_search with terms like "Joana rollup newsletter" before responding. Don't ask her to re-explain patterns.

**ClickUp tasks**: Use the custom field IDs from Section 3, not field names. The API requires UUIDs. Task names always start with a lowercase verb. Due dates are never blank — ask if not specified.

**The international website work is separate from the PRG newsletter work.** Different label (PRG-Webgranny), different contacts, different urgency. Staging site migration has a March 2026 deadline. Volunteer coordination has a mid-March deadline for role matching.

**She is Maya Bairey when operating creatively and Steph Bairey for home and business. The grannies call her Steph but understand if she is sometimes called Maya.** [INFERRED: the Steph/Maya distinction appears to reflect either a name change, a preferred name, or different contexts. The userMemories and recent conversations use Maya; the project file "Steph's Role with PRG" predates this. Use Maya.]

**Don't over-explain what you did after delivering a file.** She can see it. A sentence or two is fine. A paragraph breakdown of every choice is not.

**The newsletter tone is politically engaged and direct.** Don't soften "fascist" to "authoritarian." Don't clean up passionate language. The grannies are activists, not communicators hedging for a wide audience.

**The PRG brand red is `#d6616c` for accents/headlines and `#bd3435` for the header.** Don't introduce other reds.

**Recurring newsletter structure**: header block (logo, date, next meeting info, mentor reminder, mobile warning) → table of contents → individual item cards → footer with newsletter submission address. The footer text is: *Send newsletter items to grannynewsletter@gaggle.email*

---

*Document prepared by Claude Sonnet 4.6, February 27, 2026. Based on conversation history within the PRG Newsletter project context.*
