# Changelog - delivery-team plugin

Version family: 1.3.x is this plugin (1.0.x is Timesheet Compliance, 1.2.x is the MIS, so never use those).
Old builds 1.0.0 - 1.3.0 were made before the renumbering; exact copies are kept in `history/<version>/` for reference only (they are not loaded by Claude).

| Version | What changed | Why |
|---|---|---|
| 1.0.0 | First release: 8 agents (persona + 8-rule operating doctrine) and the `/orchestrate` master skill. | One delivery team usable in every project. |
| 1.0.1 | `/orchestrate` and README: agents must be called as `delivery-team:<name>`. | Inside a plugin every agent name carries the plugin label; short names were not found. |
| 1.1.0 | Added `context/working-style.md` and a SessionStart hook that loads it in every session. | Bharat's working style (beginner explanations, never guess, ask before assuming) on every laptop. |
| 1.2.0 | Working style: Git sync section; second startup hook runs `git fetch` + `git status -sb`. | Several laptops: always start from the latest GitHub copy, never lose work. |
| 1.3.0 | Added the `save` skill; working style and `/orchestrate`: "Starting after a clear, and saving". | Save progress to the state file and clear the chat safely to cut token use. |
| 1.4.0 | All 8 agents report a `Decisions:` line; write-through rule and a checkpoint at about 70 percent of auto-compact; save skill works in Chat/Cowork. | A compact summary can drop small decisions; files cannot. |
| 1.3.1 | Same content as 1.4.0, renumbered to 1.3.1; README versioning rule. | 1.0.x / 1.2.x numbers clashed with Timesheet Compliance and the MIS. |
| 1.3.2 | `tools:` line added to frontend-dev, backend-dev, test-engineer, acceptance-lead, ux-cx-lead; "Discuss, plan, confirm, then build" rule (working style, `/orchestrate`, rule 9 in all 8 agents); CHANGELOG, history and release checklist. | Without a tools list each agent loaded every session tool (about 33k extra tokens per start, measured). No build without Bharat's confirmed plan (Bharat, 25 Oct 2026). |
