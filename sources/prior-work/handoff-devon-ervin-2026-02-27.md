# Handoff: Devon Ervin Project — February 27, 2026

> **Note:** Items marked **[INFERRED]** are interpretations rather than explicitly stated facts. All other items are drawn from conversation history, project files, and documentation within this project.

---

## 1. What We Worked On Together

This project was a comprehensive website redesign and business system implementation for Devon Ervin, a life coach and former psychotherapist who runs Hope for Your Heart Coaching. The work was scoped in two phases at $975 each (5 hours each, billed at $195/hour), with a total project ceiling of $1,950.

### Phase 1: Event Sales & Booking Infrastructure

- Installed and configured Eventin Pro plugin for group program management
- Integrated PayPal payment gateway with Pay Later options
- Connected Zoom via the General App (not Server-to-Server OAuth) for auto-generated session links
- Built and configured email confirmation templates for event registrations
- Set up BookingPress for individual 1:1 coaching session booking (SCRATCHED! Maya built a custom plugin, not yet installed)
- Created the event registration system for Devon's 30-day Making Space program ($297)
- Configured child theme for Eventin email/thank-you page customization (override path: `eventin/templates/emails/`, copied from `wp-content/plugins/eventin/templates/emails/`)

### Phase 2: Copy, Design & Polish (Significantly Expanded)

- Built a comprehensive 17-section long-form sales page for "Making Space for What Matters Most"
- Created a 4-page sales funnel: welcome page, self-selection page, how-it-works page, enrollment page
- Executed a complete sitewide design overhaul with new coastal color palette (#4c6e90, #57a8b9, #d4c2b5, #faf8f5)
- Updated typography sitewide to Questrial/Work Sans fonts
- Redesigned homepage with animated ocean wave hero section and 9-section structure using an "I see you" empathy-driven approach
- Cleaned up discontinued two-payment system references across checkout pages, email templates, and booking forms
- Removed em-dashes per Devon's explicit preference
- Addressed responsive video implementation and CSS positioning challenges
- Produced comprehensive reference documents and client handoff materials

### Current Status

As of late February 2026, the project is in final cleanup/polish phase. The major technical infrastructure and design work is complete. Outstanding items involve final detail passes: em-dash removal, template alignment cleanup, color scheme refinements, and verifying Devon has her child theme active for Eventin email customization to take effect.

Scope expanded significantly beyond the original 10 hours — Phase 2 alone grew to include the sales funnel, complete CSS overhaul, and homepage redesign, all of which were outside the original estimate. Maya has been managing this thoughtfully.

---

## 2. How Maya Works (As Observed Here)

### Problem-Solving Approach

- Methodical and phase-based: content audit first, then strategic planning, then infrastructure, then design, then polish. Resists jumping ahead.
- Strongly prefers finishing one project fully before starting the next — evidenced by thorough cleanup passes before moving to homepage implementation.
- When something isn't working, Maya applies practical cost-benefit thinking. Example: abandoned the email forwarding project when it required more client involvement than it was worth.
- **[INFERRED]** Tends to identify scope creep early but proceeds anyway when client needs clearly warrant it — then manages expectations afterward rather than stopping mid-task.

### Decision-Making Style

- Prefers offering options (A/B/C) rather than making unilateral calls on ambiguous items — especially naming, structure, or things Devon will live with long-term.
- Makes independent judgment calls on technical implementation details without asking, but loops in Devon on anything affecting voice, copy, or user experience.
- **[INFERRED]** Has a high threshold for "good enough" before client demos — will push hard to get a deliverable across the finish line before a scheduled meeting rather than show incomplete work.

### Quality Standards

- Holds herself to a high standard on design coherence — the coastal color palette integration was meticulous, successfully harmonizing Devon's preferred peach (#EBCBB2 to #dfd2c8) with the new blues.
- Values systematic documentation: creates comprehensive reference docs, task lists in ClickUp, and handoff materials as a natural part of the workflow, not an afterthought.
- Communication style is direct, practical, and concise — dislikes verbose explanations and unnecessary hedging.

### How Maya Gives Instructions

- Uses precise language — specific file paths, exact field values, real examples. Doesn't do vague.
- Tracks "remember until later" items explicitly for technical setup instructions she'll need to return to.
- Uses ClickUp with custom field filtering (Project = "Devon Ervin") to stay organized across concurrent projects.
- **[INFERRED]** Slightly impatient with problems that circle back unnecessarily — prefers a clean solution path over iterating on something broken.

---

## 3. Tools, Systems, and Conventions

### Platform & Environment

- WordPress with Enfold/Avia theme framework — no staging environment; works directly on the live site
- Child theme setup required for Eventin email customization to persist through plugin updates
- Eventin Pro: event management plugin for group programs
- PayPal: payment processing with Pay Later options enabled
- Zoom: integrated via General App (not Server-to-Server OAuth) for auto-generated meeting links

### Technical Specifics

- Coastal color palette: `#4c6e90` (deep blue), `#57a8b9` (teal), `#d4c2b5` (warm sand), `#faf8f5` (off-white)
- Devon's legacy/preferred peach: `#EBCBB2` to `#dfd2c8` — kept in harmony with coastal palette
- Typography: Questrial (headings) / Work Sans (body)
- Eventin email template override path: `wp-content/plugins/eventin/templates/emails/` → child theme `eventin/templates/emails/`
- WordPress site code for Devon Ervin project: `26X82uNcf5T9$H8CjcdMXMbH`
- Devon's email: devonervin2010@gmail.com
- Maya's email: maya@bairey.com (also steph@bairey.com / stephbairey@gmail.com / steph@linguainkmedia.com / maya@linguaink.com)

### Project Management

- ClickUp for task tracking — custom field "Project = Devon Ervin" to filter Maya's Devon work
- Project organized in clear phases with time estimates per task
- Claude used extensively for content creation, technical problem-solving, and documentation within this project
- Filmora for video editing (e.g., animation speed adjustments for hero section)
- Envato and other stock footage sources for brand-appropriate video content

### URLs and Domains

- Primary site: devonervin.com
- Secondary: hopeforyourheartcoaching.com
- Program domain: makingspaceforwhatmattersmost.com
- Also owned: makingspaceforwhatmatters.com, lovelylittlelivingspaces.com (use TBD)

---

## 4. Preferences and Opinions

### Formatting & Communication

- **No em-dashes** — Devon specifically requested their removal throughout the site and all copy
- Prefers concise, direct communication over elaborate explanations
- Warm but not saccharine tone in all deliverables

### Design Aesthetic

- Coastal/nature themes: ocean, water, natural light, warmth
- Devon's brand is spiritual but not preachy — accessibility over intensity
- Hero section: animated ocean wave, not static imagery — movement was important
- Devon's peach palette (#EBCBB2) was her original preference; Maya successfully integrated it rather than replacing it
- **[INFERRED]** Maya has strong opinions about design coherence and will push back gently when a client preference would undermine the overall palette — but finds the integration solution rather than forcing an either/or.

### Technical Opinions

- No staging environment tolerance — works live, which requires extra care and confidence
- Practical about tool selection: chose Zoom General App integration over Server-to-Server OAuth because it was more appropriate for Devon's use case
- Abandons over-engineered solutions when simpler options exist — email forwarding project is a clear example

### Project Management Style

- Strongly prefers phase completion before moving on — doesn't like loose threads
- Total project ceiling $2,000 was a real constraint, not a soft guideline; Maya structured work to honor it even as scope expanded

---

## 5. Key Relationships and Contexts

### Devon Ervin — Primary Client

- Life coach and former psychotherapist; specializes in helping women in midlife navigate overwhelm
- Core methodology: decluttering physical spaces, relationships, and toxic patterns; uses grief writing as a primary tool
- Spiritual voice — God/Spirit/Universe language is natural to her and should be preserved, not sanitized
- Strong writer with her own authentic voice; Maya's role is to enhance and structure, not replace
- Devon sends copy in batches via email (devonervin2010@gmail.com) — often iterative chunks (sections 1-4, then 5-6, then 7, etc.)
- Responds well to detailed documentation and systematic progress tracking
- Also authored *The Reluctant Caregiver* (a memoir about her husband's brain injury), which connects to her coaching audience
- Runs a Facebook group; has an environmental activism side that occasionally intersects with her coaching audience

### Maya Bairey — Developer/Strategist

- Full name: Steph (Maya) Bairey — goes by Maya for this work context as Devon is a fellow author
- Running multiple concurrent projects: Devon, Lynn's storyboard edits, ARC tasks, cohort work
- Also appears as an endorser of Devon's book on the Devon Ervin site

### Other Contexts

- **Lingua Ink:** separate voice/context from Maya Bairey — next Claude should treat these as distinct voices if Lingua Ink work comes up
- **Lynn:** another client with storyboard editing work (separate project, different context)
- **ARC:** mentioned as concurrent work — nature unclear from this project context

---

## 6. Challenges and Friction Points

- No staging environment — all work happens on the live site, which adds risk and pressure to every change
- Scope expansion: Phase 2 grew dramatically beyond original estimate (basic copy updates → full sales funnel + complete CSS overhaul + homepage redesign)
- Responsive video implementation for the homepage hero section was technically challenging — CSS positioning issues
- Email forwarding project was abandoned when it required more client involvement than the value warranted — right call, but took time to reach
- Eventin email/thank-you page customization requires Devon to have child theme active — this dependency is out of Maya's hands and still needs verification
- Two-payment system cleanup: references to discontinued payment option were scattered across multiple places (checkout pages, email templates, booking forms) and required a systematic sweep
- Keeping Devon's peach aesthetic alive while introducing the new coastal palette required careful color integration work
- **[INFERRED]** Client communication via email (rather than a shared project management tool) means Maya is doing more organization and tracking work than would be necessary with a shared workspace

---

## 7. Decisions Made and Why

### Eventin Pro over alternatives for group program management
Chosen for its deep WordPress integration, PayPal compatibility, and Zoom connectivity. The alternative (Calendly or a third-party booking tool) would have required redirecting users off-site. Eventin keeps the full purchase flow on Devon's domain.

### Zoom General App vs. Server-to-Server OAuth
Maya chose the General App integration because Devon's use case didn't require server-to-server automation complexity. Simpler, more maintainable for a solo practitioner.

### Integrating peach palette rather than replacing it
Devon had a strong attachment to her original peach/warm tones (#EBCBB2). Rather than forcing a choice between old and new, Maya harmonized the two — keeping peach as an accent warm tone within the new coastal palette. This preserved Devon's brand comfort while achieving the design upgrade.

### Abandoning the email forwarding project
The setup required more direct involvement from Devon than the value justified. Maya made the practical call to drop it rather than create a dependency loop that would slow the project.

### 17-section long-form sales page structure
Devon had a detailed content framework she brought to the project (the "Conscious Offer Template") with 17 defined sections. Rather than redesigning the architecture, Maya worked within Devon's framework and executed it technically. This honored Devon's creative ownership while Maya handled implementation.

### $195/hour rate and $2,000 total ceiling
The rate and ceiling were set to make the project accessible while keeping Maya's time valued. As scope expanded, Maya worked within the ceiling rather than renegotiating — which means some work was likely done at a reduced effective rate. Worth knowing for future scoping conversations with Devon.

---

## 8. Things I'd Tell the Next Claude

- **Devon is the content owner.** Her voice is warm, spiritual, and deeply personal. When drafting or editing her copy, preserve her idioms and don't over-professionalize. She writes for the heart, not the resume.
- **Em-dashes are banned.** Devon asked for them to be removed. Don't reintroduce them anywhere.
- **The two-payment system is gone.** If you see any reference to a payment plan or installment option for Making Space, it's a legacy artifact that needs to be removed. The price is $297, one payment.
- **The child theme activation is still a pending dependency** for Eventin email customization. Before assuming email templates are live, verify Devon has the child theme active.
- **Maya tracks tasks in ClickUp** under Project = "Devon Ervin". If she asks you to help manage tasks or check what's open, search there first.
- **Devon sends sales page content in numbered sections via email,** iteratively. If new section content shows up, it fits into the 17-section sales page structure.
- **Maya is running concurrent projects** (Lynn, ARC, cohort work, Lingua Ink). Don't assume a question is about Devon unless it's clearly in this project context. Context-switch carefully.
- **The "Lingua Ink" voice is different from "Maya Bairey" voice.** If Lingua Ink work appears, treat it as a distinct brand/persona.
- **When Maya says "finish before starting something new," she means it.** Don't suggest parallelizing if she's in cleanup mode.
- **[INFERRED]** Maya is comfortable with uncertainty and ambiguity but doesn't want it dragged out. Give her a recommendation with a clear rationale and let her decide. She'll redirect you if she disagrees — and she's direct about it.
- **[INFERRED]** She has done a ton of work on this project and some of it has gone beyond original scope in ways that aren't fully compensated. Be efficient with her time. Don't over-explain or pad responses.

---

*Generated: February 27, 2026 | Seamless Bootstrap Handoff Series | Devon Ervin Project*
