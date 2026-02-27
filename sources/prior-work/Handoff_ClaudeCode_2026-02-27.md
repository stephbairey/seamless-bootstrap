# Handoff: Claude Code (WordPress Plugin Dev) — February 27, 2026

---

## 1. What We Worked On Together

This project is Maya's planning and strategy space for building WordPress plugins using Claude Code. The actual coding happens in Claude Code on her machine; this project is where architecture gets designed, plans get written, CLAUDE.md files get drafted, and subagents get defined.

The primary deliverable documented in this project is the **Let's Meet booking plugin** — a WordPress plugin for client scheduling. The project contains a complete process guide (Building_WP_Plugins_with_Claude_Code.md) that captures the full workflow Maya developed, from environment setup through testing.

The project also contains detailed documentation of Maya's **upstairs office machine setup** (the primary dev machine, as of February 26, 2026), including every installation decision, file path, and gotcha discovered along the way.

Current status: The process guide is finalized and the upstairs machine is fully configured. Let's Meet appears to be in active development (it's symlinked into Local as of the setup doc date). This handoff document is being produced as part of a "Seamless Bootstrap" initiative to extract and systematize everything about how Maya works.

---

## 2. How Maya Works (as observed here)

Maya is methodical about process design but not precious about it — she thinks through systems carefully, documents them thoroughly, and then wants to get moving. She doesn't want to revisit settled decisions unless something broke.

She learns by doing and iterates based on what actually happens, not what should theoretically happen. The upstairs machine setup doc is a perfect example: it documents real gotchas (Apache conflicting with Local, Linux symlinks not working for Windows PHP, the `--config core.filemode=false` clone flag) that she hit and solved, not hypothetical issues. She keeps records of the actual solution, not just the intended one.

She makes decisions deliberately and documents the reasoning. The process guide doesn't just say "use junction points on Windows" — it explains why (WSL Linux symlinks are invisible to Local's native Windows PHP). That reasoning-first documentation style shows up consistently.

She values efficiency and right-first-time quality because she runs her own business and can't afford rework. This shows up in the emphasis on thorough planning before coding starts, using deep research to review plans twice, and the explicit convention of resolving every ambiguous decision before Claude Code touches a file.

Her communication style in instructions is clear and concrete. She doesn't hedge. When she writes process docs, they read like something she'd actually hand to a contractor — specific enough to follow without hand-holding.

[INFERRED] She's more comfortable with the planning and architecture layer than the implementation layer, which is part of why the Claude Code workflow appeals to her — she can stay at the level where she's strongest (defining what needs to be built and why) and let Claude Code handle the implementation mechanics.

---

## 3. Tools, Systems, and Conventions

**Dev Environment — Upstairs (Primary)**
- OS: Windows 11, username: scbzo
- WSL2 + Ubuntu (username: linguainkmedia)
- Node 24.14.0 via nvm 0.40.3, npm 11.9.0
- Claude Code 2.1.59, installed globally in WSL
- Git 2.43.0 (Ubuntu built-in), configured as stephbairey / stephbairey@gmail.com
- SSH key: ed25519, label "WSL2 Upstairs", stored at `~/.ssh/id_ed25519`
- WP-CLI 2.12.0 at `/usr/local/bin/wp`
- PHP installed via apt (required for WP-CLI; installing it also triggers Apache, which must be stopped and disabled)
- Local by Flywheel (Windows app)

**Local Site**
- Name: Lingua Ink Media Dev
- Domain: `lingua-ink-media-dev.local`
- WP admin: `https://lingua-ink-media-dev.local/wp-admin/` (one-click admin enabled, user: admin)
- Site files: `C:\Users\scbzo\Local Sites\lingua-ink-media-dev\`
- PHP 8.2.27, nginx, WordPress 6.9.1
- WP_DEBUG enabled, logging to `C:\Users\scbzo\Local Sites\lingua-ink-media-dev\app\public\wp-content\debug.log`

**Repo Locations**
- Windows: `C:\Users\scbzo\Documents\GitHub\`
- WSL: `/mnt/c/Users/scbzo/Documents/GitHub/`
- Repos cloned from WSL with `--config core.filemode=false` (required for Windows filesystem clone from WSL)
- Claude Code run from WSL, pointed at the Windows path

**Plugin Junction Points**
- Created from PowerShell (Admin) using `cmd /c mklink /J`
- Target: inner plugin folder inside repo (not repo root)
- Currently symlinked: Let's Meet (`lets-meet` repo → `lets-meet` inner folder)
- Do NOT use `ln -s` from WSL — Local's Windows PHP cannot follow Linux symlinks

**Dev Environment — Laptop (Secondary)**
- PowerShell (no WSL)
- GitHub Desktop for version control
- Repos at `C:\Users\mjbai\Documents\GitHub\`
- Symlinks via PowerShell `New-Item -ItemType SymbolicLink`

**GitHub**
- Account: stephbairey / stephbairey@gmail.com
- Repo naming convention: matches plugin slug (e.g., `lets-meet`)

**Project Folder Structure (every plugin)**
```
repo-root/
├── .claude/
│   ├── CLAUDE.md
│   └── agents/
├── notes/
│   ├── plan.md
│   └── rules.md
└── plugin-slug/      ← actual plugin files
```

**Plugin authorship:** Lingua Ink Media, https://linguainkmedia.com

**CLAUDE.md conventions:** Under 150 lines, points to plan.md rather than embedding it, documents what Claude Code actually gets wrong rather than theoretical concerns

**Plan structure:** Numbered Parts (Product Definition, Architecture, Core Algorithm, External Integrations, User-Facing Flow, Email/Notifications, Admin Interface, Security, Privacy, Operational, Implementation Todo)

**Subagent file format:** YAML frontmatter (description, model, tools, maxTurns) + markdown instructions

**Standard subagents:** security-reviewer, wordpress-pattern-scout, test-qa, and API researcher if needed

**WSL config:** `/etc/wsl.conf` has `[automount] options = "metadata"` for proper file permission handling

**WAMP:** Installed on upstairs machine but should be stopped during Claude Code work. If odd errors appear, check whether it's running.

---

## 4. Preferences and Opinions

**Communication style:** Conversational, direct, warm. Prose over bullet points and headers. No em-dashes. Match her energy — concise when she's in quick-question mode, deep when she's doing architecture work.

**Formatting:** Sparse. Formatting only when it genuinely helps clarity. She explicitly does not like over-structured responses.

**Emotional engagement on creative work:** She wants genuine reactions tied to specific choices, not generic praise. "Good use of dialogue" is useless; "the callback to the scissors devastated me" is useful. Be gentle on drafts but honest — her goal is skill growth.

**Planning philosophy:** Thorough plans before any coding. Every ambiguous decision resolved before Claude Code starts. She'd rather spend extra time planning than redo implementation.

**Document quality:** Comprehensive but not bloated. She values documents that are both thorough and lean — not padding, not missing anything important.

**Technical opinions:**
- Prefers custom tables over post meta when the data warrants it (based on plan structure conventions)
- Strong on security patterns — nonce checks, capability checks, sanitization, escaping are non-negotiable
- dbDelta quirks get explicit documentation because they're finnicky enough to cause real problems
- Timezone handling gets explicit attention (wp_date() not date(), DateTimeImmutable with wp_timezone())

**On Claude Code sessions:** `/clear` between phases, not carrying stale context forward. Subagents for research to keep main context clean.

**What she finds unhelpful:** Generic responses, over-explanation of fundamentals she already knows, responses that don't actually answer the question she asked.

---

## 5. Key Relationships and Contexts

**Lingua Ink Media** — Maya's business. She builds WordPress sites for clients. Plugin authorship is attributed to Lingua Ink Media with the URL linguainkmedia.com. [INFERRED] This is her primary professional identity for client-facing work.

**Clients** — She works on multiple client projects simultaneously. Specific client details don't appear in this project's context, but the booking plugin (Let's Meet) is presumably built for client use cases.

**GitHub account:** stephbairey — this is her developer identity separate from the Lingua Ink Media brand identity. [INFERRED] She keeps these distinct.

**Microsoft account:** scb.zombie@gmail.com (upstairs machine login) — this appears to be a personal account used for the Windows machine, distinct from her business and GitHub emails.

---

## 6. Challenges and Friction Points

**The WSL/Windows filesystem boundary** is the main source of friction on the upstairs machine. Three specific problems were solved and documented:

1. Linux symlinks from WSL don't work for Local's Windows PHP — junction points required
2. Cloning to the Windows filesystem from WSL requires `--config core.filemode=false`
3. Installing PHP via apt installs Apache2, which conflicts with Local on port 80

The Apache conflict is particularly sneaky because it's a silent failure mode — it doesn't crash noisily, it just makes Local not work. The fix (stop and disable Apache) is documented, but there's a note that if Local ever gives a "404 Apache/Ubuntu" error, that's the first thing to check.

**Context management in Claude Code** is a recurring concern. The whole CLAUDE.md design philosophy (under 150 lines, `/clear` between phases, subagents for research) exists because context bloat causes Claude Code to become unreliable. This isn't a solved problem so much as a managed one.

**WAMP coexistence** — WAMP is installed on the upstairs machine and needs to be stopped during Claude Code/Local work. This is a potential source of confusing errors if forgotten.

[INFERRED] The two-machine setup (upstairs/downstairs) creates some friction around context continuity. The solution documented is to rely on CLAUDE.md + existing code files as session state rather than conversation history, but this requires discipline about committing and pushing before switching machines.

---

## 7. Decisions Made and Why

**Repos live on the Windows filesystem, not inside WSL**
Decision: Store all plugin repos at `C:\Users\scbzo\Documents\GitHub\` (accessed from WSL via `/mnt/c/...`), not inside the WSL filesystem.
Reasoning: Local by Flywheel is a Windows-native app. Its PHP process reads files from the Windows filesystem. If repos live inside WSL, junction points won't work and the plugin can't be connected to Local.

**Junction points instead of symlinks**
Decision: Use `cmd /c mklink /J` from PowerShell (Admin) to connect plugins to Local.
Reasoning: WSL's `ln -s` creates Linux symlinks that Windows can't follow. Local's PHP is a Windows process. Junction points are Windows-native and work correctly.

**Nested repo structure (outer folder + inner plugin folder)**
Decision: Every repo has an outer folder (git root, planning docs) and an inner folder (actual plugin, same name as slug).
Reasoning: Keeps planning docs, agent files, and git history out of the deployable plugin. The inner folder is clean and production-ready; the outer folder is the development workspace.

**CLAUDE.md under 150 lines**
Decision: Hard limit on CLAUDE.md length, with pointers to plan.md rather than embedded content.
Reasoning: AI models can follow roughly 150-200 instructions reliably. CLAUDE.md shares context space with Claude Code's system prompt. Shorter means the important rules don't get lost.

**Plan before code, always**
Decision: Full implementation plan (400-900 lines) written and reviewed before Claude Code writes a single line.
Reasoning: Claude Code works best following a clear plan, not designing architecture on the fly. Ambiguous decisions resolved upfront prevent mid-implementation derailment.

**Deep research review, twice**
Decision: Run independent plan review via deep research at least twice before finalizing.
Reasoning: Second review catches things the first missed. High confidence in the plan pays dividends during implementation.

**`/clear` between phases**
Decision: Clear Claude Code context between implementation phases rather than carrying it forward.
Reasoning: Stale context from Phase 2 creates confusion in Phase 3. Fresh context with a focused prompt produces better results.

---

## 8. Things You'd Tell the Next Claude

**She's not a beginner.** Don't explain what a symlink is, what a WordPress nonce is, or what dbDelta does. She knows. Fill gaps when you spot them, but don't over-explain.

**The two-machine setup matters.** When she mentions something about her environment, clarify which machine she's on — the solutions are sometimes different. Upstairs (primary): WSL2, junction points, `--config core.filemode=false`. Laptop (downstairs): native PowerShell, standard symlinks.

**The Apache/WP-CLI gotcha is real.** If she's getting weird Local errors on the upstairs machine, Apache running is the first thing to check. `sudo service apache2 status` in WSL.

**She runs a business.** Time is real. When she asks for something, give her the answer she needs to move forward, not a comprehensive survey of everything related to the topic.

**The Seamless Bootstrap project** is a larger initiative she's starting. This handoff is one piece of it. She's trying to extract her working knowledge into a structured system that can be used to build office automation. That context is useful if she continues that work here.

**She will come back with real implementation problems.** When Claude Code does something unexpected, she brings it here to troubleshoot. The answer she needs is usually: what went wrong, why, and the exact fix — not a general discussion of the problem space.

**The process guide is the canonical reference.** Building_WP_Plugins_with_Claude_Code.md is the source of truth for her WordPress plugin workflow. If she asks about conventions, check there first.

**She thinks in systems.** When she's describing a problem, she's already thinking about it structurally. Match that — respond at the system level, not just the immediate symptom.

**Lingua Ink Media vs. Maya Bairey** are different voices for different contexts. The plugin work is Lingua Ink Media. Pay attention to which context she's writing in.

**She uses separate WordPress accounts:** Local WP admin is `linguainkmedia` (one-click admin), GitHub is `stephbairey`. Don't mix these up.

**The `--config core.filemode=false` flag is required** every time a new repo is cloned to the Windows filesystem from WSL. It's easy to forget and the error message isn't obvious about the cause.
