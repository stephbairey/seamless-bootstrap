# Handoff: Local Dashboard — February 27, 2026

---

## 1. What We Worked On Together

This project context covers the full arc of Maya's home dashboard rebuild — from early design and data source research through implementation and completion of a working 8-slide system.

**Scope:** A household information display dashboard running on a dedicated 1920×1080 screen in Maya and Pete's floating home on the Columbia River, North Portland Harbor. The dashboard rotates through slides showing live data: weather, wind, tides/moon, river conditions, calendar, deliveries, bills, and account balances.

**Where we started:** Maya had a legacy dashboard (15+ years old) running on WAMP (Windows, Apache, MySQL, PHP) and Python. She wanted to rebuild it with a modern UX while preserving the core pipeline architecture. She also wanted to use the project as a vehicle to learn Claude Code.

**What we did:**
- Researched and tested NOAA, USGS, and Bonneville Dam APIs for real-time data
- Designed the wind slide — evaluated Sailflow embed vs. custom build, chose custom; analyzed three layout approaches (instrument/compass rose, timeline sparkline, hybrid)
- Worked through Claude Code adoption — hit Git Bash detection issues on Windows, pivoted to WSL (Ubuntu), got it working reliably
- Maya used Claude Code over a ~16-hour weekend sprint to build all 8 slides
- Created this SKILL.md file to preserve project context across conversations
- Briefly explored a side opportunity: a pain diary mobile app for personal injury clients (attorney Nicole's idea), including business model analysis and HIPAA considerations — that's a separate project thread, not part of the dashboard

**Current status:** Dashboard is complete and functional. All 8 slides working with live data. Ongoing work is polish, layout refinements, and iterating on wind slide based on Pete's usage feedback.

**Repository:** https://github.com/stephbairey/local-dashboard, branch `v2`

---

## 2. How Maya Works (as observed here)

Maya is a capable developer who knows what she wants and can articulate it clearly. She doesn't need to be hand-held through technical concepts, but she's also not a "just give me the code" person — she thinks about *why* things work, not just what works.

**Problem-solving style:** She researches before committing. When we evaluated wind data sources, she didn't just pick the first option — she wanted to understand the tradeoffs (Sailflow embed vs. custom, coarse weather apps vs. hyper-local KPDX data). She brought in a US Sailing PDF to ground the conversation in domain expertise (Chris Bedford's "Delete Your Weather Apps").

**Decision-making:** Deliberate. She considers alternatives explicitly before choosing. The wind slide design discussion is a good example — three options were on the table, she didn't rush to pick one, she wanted Pete's input before committing. She also made a clear-eyed call about Claude Code: recognized it was better suited for her workflow, but chose to defer until she was more comfortable with terminal work. Then she did it anyway over a weekend.

**Quality bar:** High. The dashboard aesthetic is specific — amber instrument panel, no dim text, readable from across the room. She flagged this constraint repeatedly and it's non-negotiable. If something looks generic or doesn't fit the aesthetic, it's wrong even if it's technically functional.

**Communication patterns:** Direct. When Claude got confused about which project we were working on (tried to scope it to Lingua Ink instead of the dashboard), she corrected it cleanly without irritation. She gives clear corrections and moves on. She doesn't over-explain.

**How she gives instructions:** Usually scenario-first. "Pete uses wind data to make sailing decisions" before "here's what I want the slide to show." She provides context that helps you understand intent, not just spec.

**What she responds well to:** Options with clear tradeoffs. Concrete examples. Being treated as a peer, not a student.

**What she finds unhelpful:** Over-structured responses with excessive headers and bullets. Generic praise. Assumptions about where she's headed.

---

## 3. Tools, Systems, and Conventions

**Dashboard stack:**
- Python fetchers → JSON files → JavaScript frontend
- Hosted locally on a headless Windows 11 mini-PC
- Accessible remotely via RustDesk
- Development happens on Maya's Windows 11 laptop
- Claude Code runs via WSL (Ubuntu) — native Windows shell had Git Bash detection issues

**Typography:**
- Body text: Aptos Display
- Headers / structured labels: IBM Plex Mono (uppercase, letter-spaced)

**Color palette:**
- Primary text (bright amber): `#fffad8`
- Secondary text (warm gold): `#ffeabf`
- Totals/positive highlights: green-teal
- Bills/amounts due: red-coral
- Background: full-bleed moody ocean/water photograph with semi-transparent panels over it

**APIs confirmed working:**
- KPDX METAR: aviationweather.gov (real-time observed conditions)
- KPDX TAF: same source (structured wind forecast)
- NWS Gridpoint: hourly wind/temp predictions
- NOAA CO-OPS: Vancouver, WA tide station, Station ID **9440083**
- USGS Water Services: Columbia River gauge (height, velocity, turbidity, discharge, water temp)
- Bonneville Dam fish passage counts (Army Corps of Engineers)

**Layout:**
- Left panel ~35%: persistent clock (day of week, time-of-day label, large time, date)
- Right panel ~65%: rotating slide content
- Slide indicator dots: upper right
- Guest mode toggle: lower right

**ClickUp usage:** Maya tracks time on dashboard tasks. Time estimates in minutes (e.g., 1380 for 23 hours). Time entries added in hour format ("9h", "7h") with dates and descriptions. Task IDs used for direct updates.

**GitHub:** repo is `stephbairey/local-dashboard`, active development on `v2` branch.

---

## 4. Preferences and Opinions

**Communication style:** Conversational, direct, warm. She explicitly said: "Talk to me like a friend who happens to have expertise." Match her energy. Don't be formal or clinical.

**Formatting:** Minimal. She dislikes excessive bullet points and headers. Prose that flows. Formatting only when it genuinely helps clarity.

**On Claude Code:** Initially hesitant due to terminal comfort level, then committed fully and had a productive 16-hour sprint with it. Prefers WSL over native Windows for Claude Code.

**On third-party widgets:** Rejected Sailflow embed for the wind slide. Prefers custom implementations that match the aesthetic over convenient-but-generic embeds. This is a design philosophy, not just a one-time call.

**On the dashboard aesthetic:** The amber instrument panel look is a feature, not a constraint. She's been iterating on this for 15 years — it's a design identity.

**On distance legibility:** Non-negotiable constraint. Everything must be readable from across the room. No dim text. Ever. If you're building something for this dashboard and text is subtle or low-contrast, it's wrong.

**On local-first architecture:** Core principle. No cloud dependencies. The fetcher → JSON → frontend pipeline is clean and intentional — don't propose cloud-based alternatives.

**On creative feedback:** [From user preferences] When she shares writing, she wants emotionally engaged responses tied to specific lines. Generic praise lands flat. Gentle on drafts, honest always. Goal is skill growth.

---

## 5. Key Relationships and Contexts

**Pete** — Maya's partner, co-inhabitant of the floating home. Primary user of the wind slide. Sails regularly, often solo 4-hour trips on Sundays. His decision-making process around sailing (when to go, when to bail) is the UX driver for the wind slide design. We don't have detailed data on his specific usage patterns yet — that's still an open question.

**Nicole** — An attorney who is a client of Lingua Ink. She surfaced the pain diary app idea — a mobile app for personal injury clients to log daily pain levels via push notifications and voice-to-text. Maya is exploring this as a potential SaaS opportunity (attorneys pay for client seats). Separate from the dashboard project entirely.

**Lingua Ink Media** — Maya's web development and marketing consulting business. Separate professional context from the dashboard, which is a personal project. The two have different voices and tones.

---

## 6. Challenges and Friction Points

**Claude Code on Windows:** Native Windows installation had persistent Git Bash detection issues. Multiple troubleshooting attempts failed. Resolution: switch to WSL (Ubuntu). This is now the established path for this project — don't suggest native Windows Claude Code.

**Context window limitations:** The codebase grew large enough that chat-based development hit context limits. This was a driver for adopting Claude Code. If conversations are getting long and complex, Maya may need to break them up or use Claude Code for file-heavy work.

**Project confusion across contexts:** At least once, Claude started talking about the wrong project (Lingua Ink instead of the dashboard). The SKILL.md file exists specifically to prevent this. Always read it before doing anything on the dashboard.

**Bank balance integration:** Was described as an "authentication challenge" in earlier conversations but was apparently solved — the accounts slide is listed as working in the final build. The implementation details are in the codebase, not documented in the skill file.

**Wind slide design finalization:** Pete's usage patterns haven't been fully documented. The timeline approach was chosen and implemented, but whether it's the *right* approach is still pending Pete's feedback. [INFERRED] Maya may be waiting for a sailing season feedback loop.

---

## 7. Decisions Made and Why

**Custom wind visualization over Sailflow embed**
- Alternatives: embed Sailflow widget, build custom
- Decision: custom
- Reasoning: Sailflow would look out of place with the amber aesthetic; custom lets them show exactly the data Pete needs; Chris Bedford's research validated that hyper-local data (KPDX airport) is more useful than generic weather apps

**KPDX as wind data source over other options**
- Decision: KPDX METAR + TAF via NOAA Aviation Weather
- Reasoning: Airport is very close to their home location; data is hyper-local; APIs are public and confirmed working; the Columbia River Gorge weather is intense enough that coarse forecasts are genuinely misleading

**Timeline layout for wind slide over compass rose**
- Alternatives: instrument/compass rose approach, timeline sparkline, hybrid
- Decision: timeline
- Reasoning: Pete's usage is trend-oriented (is wind building or dropping? when is the window?) rather than orientation-oriented; timeline better serves the actual decision he's making [INFERRED: compass rose may resurface if Pete finds directional data more important]

**WSL for Claude Code over native Windows**
- Alternatives: native Windows, Git Bash workarounds, WSL
- Decision: WSL (Ubuntu)
- Reasoning: Shell compatibility issues were intractable on native Windows; WSL provided reliable POSIX environment; git operations and shell commands work without workarounds

**Fetcher → JSON → frontend pipeline (preserved from legacy)**
- Decision: keep the pattern from the original system
- Reasoning: It's clean, it works, separation of concerns is clear; Python fetchers run on schedule, frontend just reads JSON, no tight coupling

**Local-first, no cloud dependencies**
- Decision: maintain as core principle
- Reasoning: Explicitly stated preference; [INFERRED] privacy, reliability, and avoiding service dependencies on household data

---

## 8. Things You'd Tell the Next Claude

**Always read the SKILL.md file first.** It's in the project context for a reason. The dashboard project has specific constraints, data sources, and aesthetic rules that aren't obvious. Don't assume you know what she wants based on general web dev experience.

**The aesthetic is not negotiable.** Amber text on dark background, warm instrument panel feel, readable from across the room. If you suggest something that breaks the amber palette or introduces dim/subtle text, she'll redirect you. Save time and do it right the first time.

**She knows what she's doing.** Don't over-explain basic concepts. She runs a web dev consulting business. Treat her as a peer. The learning edge is Claude Code and specific API quirks, not fundamentals.

**Don't suggest Sailflow or cloud dependencies.** Both have been explicitly rejected. Local-first is a design principle.

**WSL is the established Claude Code environment.** If the topic of running Claude Code comes up, the answer is WSL on her Windows 11 laptop, not native Windows.

**Pete is the wind slide's real user.** Any changes to that slide should be evaluated against whether they help him make sailing decisions faster and more confidently. If you don't know his usage patterns well, ask before redesigning.

**The accounts slide is guest-mode sensitive.** So is bills. Guest mode toggle exists to hide these when visitors are present. Don't forget this constraint when redesigning layouts.

**The pain diary app is a separate thread.** Nicole's idea, Lingua Ink opportunity, HIPAA considerations, SaaS model — that's a different project that got discussed here but doesn't belong in dashboard conversations.

**She prefers prose over bullets.** In responses, err toward flowing paragraphs. Use structure sparingly. Match her energy — direct and warm, not formal.

**When in doubt about direction, ask.** She gives good context when prompted. She'd rather answer a clarifying question than redirect a completed draft.
