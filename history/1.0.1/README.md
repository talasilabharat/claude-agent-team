# delivery-team (private)

Bharat's Claude Code delivery agent team, packaged as a plugin so the same agents run in every project on every laptop.

## What's inside
- **8 specialist subagents** (`agents/`): architect, ux-cx-lead, frontend-dev, backend-dev, quality-reviewer, test-engineer, security-vapt, acceptance-lead. Each has a persona plus the shared 8-rule operating doctrine (outcome first, ask don't assume, prove never guess, requirements ledger, smallest correct change, challenge wrong premises, safe by default, honest compact report).
- **`/orchestrate`** (`skills/orchestrate/`): the master Delivery Director that clarifies requirements, keeps `.claude/project-state.md`, delegates to the right agent/model, verifies results, controls token usage, and produces RAG status reports.

## Agent names
Because this is a plugin, every agent appears with the label `delivery-team:` (for example `delivery-team:architect`) and the master skill as `delivery-team:orchestrate`. The master (`/orchestrate`) already uses these names.

## Install (once per laptop)
Prerequisites: Git installed, and a GitHub login stored for git on that laptop (the install never prompts for one).

Desktop app (Code tab): click **+** next to the prompt box -> **Plugins** -> **Add marketplace** -> enter `talasilabharat/claude-agent-team` -> add **delivery-team**.

Terminal:
```
claude plugin install delivery-team --marketplace talasilabharat/claude-agent-team
```

## Changing an agent or rule
1. Edit the file in `agents/` or `skills/orchestrate/` in this repository.
2. Bump `version` in `.claude-plugin/plugin.json` (e.g. 1.0.0 -> 1.1.0).
3. Commit and push.
4. On each laptop: `claude plugin update delivery-team`, then `/reload-plugins` (or start a new session).
