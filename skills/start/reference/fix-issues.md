# Something is wrong: fix it the workspace way

## The policy (Bharat, 27 Oct 2026)
1. **Do not reinvent the wheel.** Before you build anything new, find how the workspace ALREADY does it: this skill's `guide.md`, `workspace-control\docs\notes\GLOBAL_DECISIONS.md`, the scripts in `workspace-control\scripts`, the project's own notes, and how the other projects handle the same thing (look in 2 or 3 of them). Copy that proven pattern.
2. **No assumptions.** Reproduce or read the problem first (run `start-check.ps1`, read the log or the file). Say what you checked and what came out. After the fix, run the same check again and show the proof. "Probably" is not a finding.
3. **If the problem is general, fix it everywhere.** Change the shared source (template, script, guide, standard block), then run `workspace-control\scripts\sync-standards.ps1` so ALL projects get it, run `sync-standards.ps1 -Check` to prove they all do, and record the decision (date, why) in `GLOBAL_DECISIONS.md` and the affected projects' notes. If it is only this project, fix it only here and record it in this project's notes.
4. **You do the work.** Never hand Bharat a command or a click-through: say in one or two lines what you will do, ask for a clear YES in the chat, and on yes do it yourself and prove it. Never route around a safety block, never force, never overwrite, never delete without his yes (Recycle Bin). Secrets: see `credentials.md` (never ask him to recall or recreate an old token).
5. **Only if nothing in the workspace covers it**, design a new way: explain the plan in simple words, short, get his approval, build it as a script in `workspace-control\scripts` (parse-check it, test it in a sandbox), add it to the table below and the guide, and record it. Then the next session can reuse it.

## Remedy table: what the check reports, what to do automatically, what only Bharat can do
| Check says | You do (automatic) | Only Bharat |
|---|---|---|
| No laptop label | Ask "Is this your second laptop (L2) or a new one (L3)?" Never assume. Then `setup-laptop.ps1 -Label Lx -Root <folder>`. | Say which laptop. |
| Laptop / workspace folder not registered | `setup-laptop.ps1` (registers, downloads every project, syncs). | - |
| Git missing | Ask YES once, then run `winget install --id Git.Git -e --source winget --scope user` and check `git --version`. | The yes. |
| GitHub refused or not signed in | First prove it (`credentials.md` section 1). If really missing: run `git clone` in his terminal tab so Git Credential Manager opens the browser sign-in. | Click Authorize once (no token to type). |
| GitLab sign-in not stored on this laptop | `credentials.md` section 2: SSH key for this laptop (no token) when proven; otherwise a per-laptop token. Never ask him to recall an old token. | Only if a token is used: he saves it himself. |
| GitLab token expiring or expired | Same guidance; after he has saved the new token, update `gitlab.tokenExpires` in `projects.json`, run the sync, check "GitLab up to date". | Make and save the token. |
| GitLab not reachable | Nothing: normal off the office network; the backup catches up later. | - |
| Project behind or ahead of GitHub | `sync-all.ps1 -Only <name>`, then the check again. On an ALERT: read `%LOCALAPPDATA%\WorkspaceSync\ALERT.txt`, run `sync-all.ps1 -DryRun`, explain, change nothing, ask. | Decide on a conflict. |
| Notes missing or no LIVE STATE | `sync-standards.ps1` (adds the skeleton), then fill A, B, C, E from the project's real files; ask him only for what the files do not say. | Answers about purpose. |
| Standards missing in some projects | `sync-standards.ps1`, then `-Check` must say 0. | - |
| Folder in the workspace that is not a project | Ask: register it as a project (choose NEW) or move its files into the right project folder. Never delete. | Which one. |
| Project not on this laptop | The sync downloads it; run `sync-all.ps1 -Only <name>`. | - |
| Delivery agents older than GitHub | In the browser pane (Bharat signed in to claude.ai): Customize > Plugins > Add > Manage marketplaces > claude-agent-team > Check for updates; if it says "Sync failed", hover the badge for the reason (usually a second `plugin.json` in the repository). Then ask for a new session. | Sign in to claude.ai in the pane if asked. |
| Global hooks or global instruction block missing | Run `workspace-control\scripts\install-global-hooks.ps1` yourself (standing permission, 27 Oct 2026; proven to work); run the check again. If the safety check refuses, say so, ask him what he wants; do not hand him a command. | Nothing. |
| Memory hook never ran | After the hooks are installed: ask him to open a NEW session and look for "Project memory loaded"; then the check again (stamp file). | Open a new session. |
| A figure looks wrong | Trace it against the source system's own screen before explaining anything. | - |

## When the table has no row
Do step 1 of the policy for real: search the guide, GLOBAL_DECISIONS, the scripts, and 2 or 3 projects for the nearest existing case. Show Bharat what you found and which pattern you copy. Only then step 5. Add the new row here.
