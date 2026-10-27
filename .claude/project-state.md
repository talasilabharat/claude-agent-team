# Project state - Claude agent team (delivery-team plugin)

Legend: CONFIRMED = Bharat stated it. PROVEN = tested with real output. UNVERIFIED / OPEN = not done or not checked.

## 00. LIVE STATE - READ THIS FIRST (rewritten whenever anything changes)

Last updated: 27 Oct 2026, evening, work laptop L1, Claude Code (desktop app). Structure and rules: D:\Projects\workspace-control\rules\STATE_STANDARD.md. Update the matching block in the same turn as every decision, correction, proof, mistake or file change. CONFIRMED = Bharat stated it; PROVEN = tested. No secrets. Only "-" as a dash.

### A. What this project is
- The "delivery-team" plugin: Bharat's Claude delivery agent team. 8 specialist subagents (architect, ux-cx-lead, frontend-dev, backend-dev, quality-reviewer, test-engineer, security-vapt, acceptance-lead) and 3 commands (/orchestrate = the master Delivery Director, /save, /version), plus a SessionStart hook that loads the working-style rules (context\working-style.md) and shows the folder's Git status. Names appear as delivery-team:<agent>.
- Repository: github.com/talasilabharat/claude-agent-team (private; GitLab backup http://192.168.1.76:8009/bharat-projects/claude-agent-team.git). Current version 1.3.4 (.claude-plugin\plugin.json). Version family: 1.3.x is this plugin (1.0.x is Timesheet Compliance and 1.2.x is the MIS, never use those).
- Files: agents\*.md (8), skills\orchestrate, skills\save, skills\version, hooks\hooks.json, context\working-style.md, .claude-plugin\plugin.json and marketplace.json (marketplace name bharat-agents), README.md, CHANGELOG.md, history-archive.zip (old builds 1.0.0 to 1.3.0, byte-identical copies).

### B. Where we stopped (27 Oct 2026, evening)
- Just finished: released 1.3.4 (the rules and the save/orchestrate commands no longer ask "Save today's work to GitHub?" in projects with the automatic sync; no agent changed); found and fixed why claude.ai never received new versions (see D); claude.ai now shows 1.3.4 and "Sync automatically" is ON.
- Doing now: nothing on the agents; the memory system is being added to all projects.
- Waiting on Bharat: nothing.
- Next steps: at the next session start check that this laptop's own plugin copy updated to 1.3.4 (/version) and that /version works in a NEW Chat and Cowork chat.

### C. Decisions CONFIRMED by Bharat (newest first)
27 Oct 2026
- The agents must update themselves automatically from GitHub on every laptop, with no duplicate teams and no manual upload or copying. (Built: claude.ai syncs this repository itself.)
- Fully automatic sync wording in the rules (1.3.4), wording shown to and approved by Bharat before the change.
- Any change to an agent's persona or instructions, or anything of that kind, needs Bharat's explicit approval that names the agent and the change. Plans for Bharat are in simple language with a short summary.
- Memory: notes only, detailed and structured, updated every time something changes.
Earlier (README): the repository stays private; release checklist: discuss, confirm the plan with the exact wording, build, show the exact differences, test, second yes, push, changelog line.

### D. Proven facts (how it was proven)
- claude.ai (Customize > Plugins > Yours) listed "Delivery team from claude-agent-team 1.3.1" and Manage marketplaces showed claude-agent-team as "Sync failed". The hover text said "1 plugin failed validation: plugin.json must be at .claude-plugin/plugin.json at the plugin root; found nested: history/1.0.0/... to history/1.3.0/...". After the old copies were packed into history-archive.zip (67 files, SHA-256 checked one by one against the folder) and pushed, "Check for updates" said Synced and "Updated to dd94800"; the plugin page then showed 1.3.4, 3 skills, 8 agents. "Sync automatically" was switched ON (account setting, by Claude with Bharat's approval of the plan).
- The same plugin id (plugin_01P1rfG6Wo5V9YXYZ8VSgb6G) is the copy the Claude Code desktop app caches (Claude's rpm folder), so Chat, Cowork and Claude Code share one source.
- claude plugin validate passes (only directory-submission notes about LICENSE and icon, which do not matter here). Exactly 7 files changed for 1.3.4 and none of the 8 agent files.
- The agents' rule 7 ("Safe by default": no git commit or push without explicit approval relayed by the master) stays correct: the automatic save is done by the laptop's hooks, not by an agent.

### E. Open items
1. This laptop's local copy (Claude's cache) still showed 1.3.1 right after the fix; check at the next session start that it updated to 1.3.4.
2. /version did not work in Chat and Cowork before 27 Oct because claude.ai held 1.3.1 (the command arrived in 1.3.3). Check in a NEW chat now. If it still fails, find how skills are invoked in Chat and Cowork.
3. claude.ai showed "1 notice" next to the marketplace after the sync; its text was not read.
4. The plugin's SessionStart hook still prints the git status and the rules ask Claude to pull when behind: harmless next to the automatic sync, but the two overlap.
5. Bharat believes the agents were on the other laptop: which Claude account that laptop uses is unknown (claude.ai shows them on this account).

### F. Rules that must never be broken
- Never change an agent's persona, instructions or any agent file without Bharat's explicit approval naming the agent and the change. Never push a release without the checklist.
- Keep exactly ONE plugin.json in the repository (at .claude-plugin\plugin.json): any other, for example in an old-versions folder, makes claude.ai refuse the whole sync. Bump version in plugin.json for every release (claude.ai only picks up a changed version) and update skills\version\SKILL.md and CHANGELOG.md with it.
- Repository stays private; never force-push.

### G. Where things are
- D:\Projects\claude-agent-team (this laptop). claude.ai: Customize > Plugins > Add > Manage marketplaces > claude-agent-team (menu: Check for updates, Sync automatically, Remove). Plugin page: claude.ai/customize/plugins/yours/id/plugin_01P1rfG6Wo5V9YXYZ8VSgb6G. Claude Code app's cache: %APPDATA%\Claude\rpm\...\plugin_01P1rfG6Wo5V9YXYZ8VSgb6G.

### H. How the automatic systems work
- Release: edit, bump version, push (the workspace sync pushes by itself). claude.ai follows the repository (Sync automatically ON) and the new version reaches Chat, Cowork and the Claude Code app. To force it: Manage marketplaces > Check for updates.
- Changes to this repository are backed up to GitLab by the workspace sync on the office network.

### I. Mistakes to avoid
- The nested plugin.json copies in history\ blocked the claude.ai sync silently for days; the old release step "zip and upload to claude.ai by hand" was manual work and left claude.ai stale.
- Two edits were attempted before reading the file first; always read a file before editing.

### J. Change log (newest first)
- 27 Oct: 1.3.4 (rules and save/orchestrate/README/version text); history\ packed into history-archive.zip; README release steps updated (no zip upload); claude.ai sync repaired and set to automatic.
- 25 Oct: 1.3.3 (/version), 1.3.2 (tools lists, "discuss, plan, confirm, then build"), 1.3.1 (renumbered), earlier 1.0.0 to 1.3.0 (see CHANGELOG.md).

