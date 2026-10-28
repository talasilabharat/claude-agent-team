# CLAUDE.md - the delivery-team plugin repository

Bharat is not technical: plain words, one step at a time, no guesses (check and show proof).

## Rules for this repository
- NEVER change an agent's persona or instructions (any file in `agents/`), or any other rule text, without Bharat's explicit approval that names the agent and the change. Follow the release checklist in README.md (discuss, confirm the plan with the exact wording, build, show the exact differences, test, second yes, push, changelog line).
- Every release bumps `version` in `.claude-plugin/plugin.json` (1.3.x) and updates `skills/version/SKILL.md` and CHANGELOG.md. Keep exactly ONE plugin.json in the repository: a second one anywhere makes claude.ai refuse the whole sync.
- The repository stays private; never force-push. claude.ai does NOT follow it by itself: after a push the start skill presses "Check for updates" (Customize > Plugins > Add > Manage marketplaces > claude-agent-team) whenever the plugin is older than GitHub.

<!-- workspace-standard:begin -->
## Workspace standard (the same in every project; maintained by workspace-control\scripts\sync-standards.ps1 - do not edit inside this block)
- Laptops: L1 = the i-exceed work laptop, L2 = Bharat's second laptop, L3 and up = new ones. Never write a real computer name anywhere (notes, code, commit messages, GitHub, GitLab).
- Memory: read `.claude/project-state.md` (MIS: `01_project_docs/MIS_HANDOFF.md`), block `## 00. LIVE STATE`, FIRST; update it in the SAME turn as every decision, correction, proof, mistake or file change; detail goes into `docs/notes/`. A decision that applies to ALL projects also goes into workspace-control `docs/notes/GLOBAL_DECISIONS.md`.
- Say "Start" to start from the project list: the skill `delivery-team:start` (never `productivity:start`, another plugin's skill with the same name) checks everything, continues an existing project, sets up a new one, explains how things work, and fixes problems. If the skill is not available in this Claude account, read `claude-agent-team/skills/start/SKILL.md` in the workspace and follow it (its first job is to add the plugin to the account).
- When something is wrong: do NOT invent a new way. First find how the workspace already does it (the guide inside `start`, GLOBAL_DECISIONS, the scripts in workspace-control, how the other projects handle it), copy that proven pattern, verify with evidence (no assumptions), and if the problem is general fix it in the shared place and in ALL projects (`sync-standards.ps1`), then record it.
- GitHub is the master (private repositories); the office GitLab is the backup (office network only); never force-push; no secrets in Git; Bharat enters tokens himself; keep every file of the project inside its own folder in the workspace.
- Never change an agent's persona or instructions (delivery-team plugin) without Bharat's explicit approval naming the agent and the change.
<!-- workspace-standard:end -->
