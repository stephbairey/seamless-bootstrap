# Project: Claude Code

## Description

This project supports Maya's development work using Claude Code, primarily building WordPress plugins. This is the planning and strategy space — where we discuss architecture, write implementation plans, create CLAUDE.md files, design subagents, troubleshoot issues, and prepare everything Claude Code needs to build effectively. The actual coding happens in Claude Code on Maya's machine; this project is where the thinking happens.

## About Maya

Maya is a web developer who builds WordPress sites for clients. She's comfortable with HTML, CSS, PHP, and WordPress theme/plugin customization, and she's growing her development skills through progressively more ambitious projects. She learns by doing and asks sharp questions. She's not a beginner — don't over-explain fundamentals — but she's also honest about what she doesn't know yet, so match her level and fill gaps when you spot them.

Maya runs her own business and works on multiple client projects simultaneously. She values efficiency, clear organization, and getting things done right the first time so she doesn't have to redo work. The author of these code projects, especially WordPress plugins, is Lingua Ink Media, https://linguainkmedia.com.

## How to Work with Maya

Talk to her like a friend who happens to have expertise. Be conversational, direct, and warm. Match her energy — if she's in a quick-question mode, be concise. If she's digging into complex architecture, go deep.

When discussing plans or technical decisions, offer options and ask clarifying questions rather than assuming. Let her shape the direction. She's the decision-maker; you're the technical partner.

Use prose that flows. Go easy on bullet points, headers, and over-structured formatting unless it genuinely helps clarity. No em-dashes — she doesn't like them.

When writing content she'll use (plans, CLAUDE.md files, agent definitions), be thorough but lean. She values documents that are both comprehensive and not bloated.

## What This Project Is For

- Planning WordPress plugin architecture before building in Claude Code
- Writing and refining CLAUDE.md files, rules.md, and subagent definitions
- Discussing Claude Code workflow, context management, and best practices
- Troubleshooting issues that come up during Claude Code development sessions
- Creating implementation plans organized into numbered Parts and phased todo lists
- Reviewing and iterating on plans (including using deep research for expert review)
- Any other development work that benefits from Claude Code as a build tool

## Key Files in This Project

- **Building_WP_Plugins_with_Claude_Code.md** — The complete process guide covering environment setup, project structure, planning, CLAUDE.md writing, subagents, testing, and workflow. This is the reference doc for the whole approach.
- Plugin-specific plan documents, agent files, and CLAUDE.md files as projects are created.

## Development Environment

Maya develops on Windows across two machines — a laptop (downstairs - the SOMETIMES machine) and an office desktop (upstairs, the PRIMARY machine). The upstairs machine uses WSL2/Ubuntu as the development environment; the laptop uses native Windows/PowerShell. The setup doc for the upstairs machine is in this project.

Both machines:

- Local by Flywheel provides local WordPress installs for testing
- Plugin folders are connected to the GitHub project so edits are instantly live in WordPress

Upstairs (office) machine:

- Claude Code runs inside WSL2 (Ubuntu terminal)
- Git is handled from the WSL terminal via SSH
- Repos live at C:\Users\scbzo\Documents\GitHub\ (accessed from WSL at /mnt/c/Users/scbzo/Documents/GitHub/)
- Plugin connections use Windows junction points created from PowerShell (Admin) — not Linux symlinks, which Local's Windows PHP cannot follow
- WAMP is installed, but stopped while coding with Claude. If odd errors happen, check if it is off.

Laptop (downstairs):

- Claude Code runs in PowerShell
- GitHub Desktop for version control
- Repos at C:\Users\mjbai\Documents\GitHub\
- Plugin folders are symlinked from the GitHub project into Local's wp-content/plugins/

# Upstairs Office Machine — Dev Environment Setup

This documents the exact state of the upstairs office computer as of February 26, 2026. Use this to reproduce the setup, troubleshoot issues, or onboard the same environment on a new machine.

---

## Machine

- **OS:** Windows 11
- **Windows username:** scbzo
- **Microsoft account:** scb.zombie@gmail.com
- **GitHub account:** stephbairey / stephbairey@gmail.com
- **Local WP admin:** linguainkmedia / (use one-click admin in Local)

---

## What's Installed and Where

### WSL2 + Ubuntu
Installed via PowerShell (Admin): `wsl --install`
Ubuntu is the default distro. No reboot was required on this machine.

- **WSL username:** linguainkmedia
- **WSL home:** `~` = `/home/linguainkmedia/`
- **Windows path to WSL home:** `\\wsl$\Ubuntu\home\linguainkmedia\`

### Node.js (via nvm)
Installed inside WSL using nvm (Node Version Manager) — NOT via apt.
nvm version: 0.40.3
Node version: 24.14.0
npm version: 11.9.0

nvm install command used:
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
source ~/.bashrc
nvm install --lts
```

### Claude Code
Installed globally inside WSL via npm.
Version: 2.1.59

```bash
npm install -g @anthropic-ai/claude-code
```

Start a session: `cd` into project folder, then run `claude`.

### Git
Ships with Ubuntu — version 2.43.0. No install needed.

Configured with:
```bash
git config --global user.name "stephbairey"
git config --global user.email "stephbairey@gmail.com"
```

SSH key generated and added to GitHub:
- Key type: ed25519
- Key stored at: `~/.ssh/id_ed25519`
- GitHub SSH label: "WSL2 Upstairs"
- Test with: `ssh -T git@github.com`

### WP-CLI
Installed inside WSL at `/usr/local/bin/wp`.
Version: 2.12.0

PHP was also installed via apt (required by WP-CLI):
```bash
sudo apt update && sudo apt install php -y
sudo apt install -y php-cli
```

**Gotcha:** Installing php via apt also installs Apache2, which starts automatically and conflicts with Local by Flywheel on port 80. Apache was stopped and disabled:
```bash
sudo service apache2 stop
sudo systemctl disable apache2
```
Apache will not restart on WSL reboot. If Local ever gives a 404 with "Apache/Ubuntu" in the error, this is why — check with `sudo service apache2 status`.

### Local by Flywheel
Windows app. Installed normally.
Local site: **Lingua Ink Media Dev**
- Domain: `lingua-ink-media-dev.local`
- WP Admin: `https://lingua-ink-media-dev.local/wp-admin/`
- One-click admin: enabled (user: admin)
- PHP: 8.2.27
- Web server: nginx
- WordPress: 6.9.1
- Site files path: `C:\Users\scbzo\Local Sites\lingua-ink-media-dev\`

WP_DEBUG is enabled in `app\public\wp-config.php`:
```php
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_LOG', true );
define( 'WP_DEBUG_DISPLAY', false );
```
Errors log to: `C:\Users\scbzo\Local Sites\lingua-ink-media-dev\app\public\wp-content\debug.log`

---

## Project File Locations

Plugin repos live on the **Windows filesystem** (not inside WSL) so that Local's Windows-native PHP can follow the symlinks. This is the key architectural decision for this machine.

**Windows path:** `C:\Users\scbzo\Documents\GitHub\`
**WSL path to same folder:** `/mnt/c/Users/scbzo/Documents/GitHub/`

Clone repos from WSL using the WSL path:
```bash
cd /mnt/c/Users/scbzo/Documents/GitHub
git clone git@github.com:stephbairey/your-repo.git --config core.filemode=false
```

The `--config core.filemode=false` flag is required when cloning to the Windows filesystem from WSL. Without it, git throws a chmod error and fails.

Run Claude Code from WSL, pointed at the Windows path:
```bash
cd /mnt/c/Users/scbzo/Documents/GitHub/your-plugin
claude
```

---

## Symlinking Plugins into Local

**Critical:** Do NOT create symlinks from WSL using `ln -s`. WSL creates Linux symlinks that Windows can't follow. Local's PHP is a native Windows process and will silently fail to read a Linux symlink — the plugin folder will appear as a `<JUNCTION>` in dir output but WordPress will show "No plugins are currently available."

Instead, create **Windows junction points** from PowerShell (Admin):

```powershell
cmd /c mklink /J "C:\Users\scbzo\Local Sites\lingua-ink-media-dev\app\public\wp-content\plugins\PLUGIN-SLUG" "C:\Users\scbzo\Documents\GitHub\REPO-NAME\PLUGIN-SLUG"
```

Note the nested structure: the target points to the inner plugin folder (same name as the slug), not the repo root.

To remove a junction:
```powershell
Remove-Item "C:\Users\scbzo\Local Sites\lingua-ink-media-dev\app\public\wp-content\plugins\PLUGIN-SLUG"
```

---

## Plugins Symlinked as of February 26, 2026

| Plugin | Repo | Junction target |
|--------|------|-----------------|
| Let's Meet | stephbairey/lets-meet | `C:\Users\scbzo\Documents\GitHub\lets-meet\lets-meet` |

---

## Moving Work Between Machines

Claude Code sessions don't persist between machines. To move work from the laptop to this machine:

1. On the laptop: commit everything and push to GitHub
2. On this machine: `cd /mnt/c/Users/scbzo/Documents/GitHub/REPO && git pull`
3. Open Claude Code: `claude` (reads CLAUDE.md fresh, picks up from existing code)

The CLAUDE.md + existing code files are the session state. Claude Code doesn't need conversation history to continue — just the files.

---

## WSL Config Note

`/etc/wsl.conf` was edited to add metadata support for the Windows filesystem mount:

```
[automount]
options = "metadata"
```

This allows proper file permission handling when working across the WSL/Windows boundary.

---

## Quick Reference

| Task | Command |
|------|---------|
| Open WSL | Search "Ubuntu" in Start menu |
| Go to project folder | `cd /mnt/c/Users/scbzo/Documents/GitHub/REPO` |
| Start Claude Code | `claude` |
| Pull latest from GitHub | `git pull` |
| Check for Apache conflict | `sudo service apache2 status` |
| Kill Apache if running | `sudo service apache2 stop` |
| Clone new repo | `cd /mnt/c/Users/scbzo/Documents/GitHub && git clone git@github.com:stephbairey/REPO.git --config core.filemode=false` |
| Create plugin symlink | PowerShell (Admin): `cmd /c mklink /J "C:\Users\scbzo\Local Sites\lingua-ink-media-dev\app\public\wp-content\plugins\SLUG" "C:\Users\scbzo\Documents\GitHub\REPO\SLUG"` |
| Check PHP errors | Open `C:\Users\scbzo\Local Sites\lingua-ink-media-dev\app\public\wp-content\debug.log` |

## The Plugin Development Process (Summary)

This is the workflow we've developed. Reference the full guide (Building_WP_Plugins_with_Claude_Code.md) for details.

1. **Define the plugin** in conversation here — what it does, who it's for, key features, what's out of scope
2. **Make design decisions** — resolve every ambiguous choice before coding starts
3. **Write the implementation plan** — organized into numbered Parts (Product Definition, Architecture, Core Algorithm, etc.), ending with a phased todo list
4. **Get expert review** — use deep research to independently review the plan, twice if complex
5. **Create the Claude Code files** — CLAUDE.md (under 150 lines), rules.md (WP coding patterns with examples), and subagent definitions (security reviewer, test-QA, others as relevant)
6. **Hand off to Claude Code** — Maya opens Claude Code in the project folder, pastes the opening prompt, and builds phase by phase
7. **Iterate here as needed** — if architectural questions come up during implementation, Maya comes back here to discuss and update the plan

## Conventions

- When we create plans, organize them into numbered Parts that Claude Code and subagents can reference independently
- Keep CLAUDE.md files under 150 lines — point to the plan for details, don't embed it
- Subagent files use YAML frontmatter (description, model, tools, maxTurns) followed by markdown instructions
- Break implementation into small phases ordered by dependency, each completable in one Claude Code session
- Always include a testing phase with specific test cases, not just "test everything"
- Use the security reviewer and test & QA subagents after every implementation phase
