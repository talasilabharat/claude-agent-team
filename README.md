# delivery-team (private)

Bharat's Claude Code delivery agent team, packaged as a plugin so the same agents run in every project on every laptop.

## What's inside
- **8 specialist subagents** (`agents/`): architect, ux-cx-lead, frontend-dev, backend-dev, quality-reviewer, test-engineer, security-vapt, acceptance-lead. Each has a persona plus the shared 9-rule operating doctrine (outcome first, ask don't assume, prove never guess, requirements ledger, smallest correct change, challenge wrong premises, safe by default, honest compact report, no build without a confirmed plan).
- **`/orchestrate`** (`skills/orchestrate/`): the master Delivery Director that clarifies requirements, keeps `.claude/project-state.md`, delegates to the right agent/model, verifies results, controls token usage, and produces RAG status reports.
- **`start`** (`skills/start/`, since 1.3.5): the ONE skill for Bharat's whole workspace. Say "Start" (alone, or with a greeting): it greets him, checks sync, sign-ins and agents, fixes what it can, shows the project list, and handles an existing project, a new project, how things work, fixing problems, and setting up a new laptop or a new Claude account. Its reference files are `reference/guide.md`, `new-project.md`, `fix-issues.md`, `bootstrap.md` and `credentials.md`; the always-on pointer is `context/workspace-pointer.md`. Works in Claude Code, Cowork and Chat (what each can do is in the guide).

## Always-on working style
A small startup hook (`hooks/hooks.json` -> `context/working-style.md`) adds Bharat's working-style rules (explain like to a beginner, never guess, ask before assuming) to every session on every laptop where this plugin is installed. To change those rules, edit `context/working-style.md`.

## Git sync check
A second startup hook runs `git fetch` and `git status -sb` in the folder where a session starts. If the folder is a Git repository, Claude is told whether it is behind or ahead of GitHub and follows the Git sync rules in `context/working-style.md` (pull with fast-forward only; saving to GitHub is automatic where the project has the sync hooks, so it does not ask). Outside a Git folder it prints nothing.

## Save skill
Say **Save** (or `/delivery-team:save`) and Claude checks whether it is a good moment, writes confirmed progress into the project's state file (MIS_HANDOFF.md or .claude/project-state.md), and clears the chat when worthwhile (GitHub saving is automatic where the project has the sync hooks) (the app asks for approval). It cannot run `/compact`; Claude Code compacts automatically at the size set by `autoCompactWindow` in settings.

## Never lose decisions
Write-through rule (every confirmed decision or correction goes into the state file immediately), a checkpoint at about 70 percent of the auto-compact point, agents report a `Decisions:` line that the master records, and re-reading the state file after any clear or compact. Where it works: Claude Code (everything), Cowork (skills and agents; hooks run on the computer), Chat (skills only).

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
2. Bump `version` in `.claude-plugin/plugin.json` (always 1.3.x: 1.3.1 -> 1.3.2; 1.0.x is Timesheet Compliance and 1.2.x is the MIS, so never use those).
3. Commit and push.
4. The update chain (tested 27 Oct 2026): claude.ai does NOT follow this repository by itself, even with "Sync automatically" on. Press "Check for updates" (Customize > Plugins > Add > Manage marketplaces > claude-agent-team > its menu); the `start` skill does this itself whenever the plugin is older than GitHub. Chat and Cowork then have it at once; the Claude desktop app picks it up by itself within about an hour. A new version is only picked up when `version` in `plugin.json` changes.

## Release checklist (every new version)
1. **Discuss** the change with Bharat until there is a conclusion. No edits yet.
2. **Confirm the plan**: show what will change, where, and the exact wording of any rule text; build only after an explicit yes.
3. **Build**: make only the confirmed changes and bump `version` (1.3.x). Never change existing agent rules, personas or working style unless that exact change was confirmed.
   - Also update the version number and date in `skills/version/SKILL.md` (the `/version` command), so it matches `plugin.json`.
4. **Show the exact differences** (`git diff`) to Bharat.
5. **Test**: one token check (agent start cost) plus one small real task with an agent.
6. **Second yes** from Bharat before pushing.
7. **Push** to `talasilabharat/claude-agent-team` (secrets scan first; never force-push; repository stays private). Add one line to `CHANGELOG.md`.
8. **No zip and no upload any more** (27 Oct 2026): claude.ai does not follow this repository by itself (see step 4). Keep exactly ONE `plugin.json` in the repository (at `.claude-plugin/plugin.json`): a second one anywhere, such as an old copy in a `history/` folder, makes claude.ai refuse the whole sync ("plugin failed validation"). Old versions live in `history-archive.zip`. After pushing, press "Check for updates" in Manage marketplaces: it must say "Updated to <the new commit>".
