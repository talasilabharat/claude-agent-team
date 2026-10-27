# CLAUDE.md - the delivery-team plugin repository

Bharat is not technical: plain words, one step at a time, no guesses (check and show proof).

## Project memory (Bharat, 27 Oct 2026: notes only, always current)
- `.claude/project-state.md`, block `## 00. LIVE STATE` at the top, is this project's memory. Read it first, in every session, after every clear or compact. Keep it current IN THE SAME TURN as every decision, correction, proof, mistake or file change. Structure and rules: `D:\Projects\workspace-control\rules\STATE_STANDARD.md`.

## Rules for this repository
- NEVER change an agent's persona or instructions (any file in `agents/`), or any other rule text, without Bharat's explicit approval that names the agent and the change. Follow the release checklist in README.md (discuss, confirm the plan with the exact wording, build, show the exact differences, test, second yes, push, changelog line).
- Every release bumps `version` in `.claude-plugin/plugin.json` (1.3.x) and updates `skills/version/SKILL.md` and CHANGELOG.md. Keep exactly ONE plugin.json in the repository: a second one anywhere makes claude.ai refuse the whole sync.
- The repository stays private; never force-push. claude.ai follows it by itself (Customize > Plugins > Manage marketplaces > claude-agent-team, Sync automatically ON).
