# Bootstrap: a NEW laptop and/or a NEW Claude account (you do it all, step by step)

Used when `start` finds no `workspace-control` folder on this computer (a new laptop, or a new Windows user), or the account is new. Rules of `SKILL.md` apply: no assumptions, copy what the workspace already does, you do the work, one clear YES from Bharat in the chat before the first change, then you carry on without sending him off to do things. He gave standing permission for this whole setup (27 Oct 2026). After each step run its check and show the proof in one line.

## What he must have done once, himself (the only manual part, 30 seconds)
In claude.ai: Customize > Plugins > Add > Add marketplace > paste `talasilabharat/claude-agent-team`, then Manage marketplaces > claude-agent-team > switch "Sync automatically" ON. (Nothing can do this for him before the plugin exists: it is how this skill reaches the account. The account must be able to read the private GitHub repository: claude.ai asks to connect GitHub if it cannot.) Same laptop, another Claude account on the same Windows user: this is all that is needed (the hooks, the sign-ins and the folders are the laptop's, not the account's); go to step 9.

## Steps (FULL mode, in Claude Code or a Cowork task linked to this computer)
1. **Say what will happen, ask YES once:** "I will check Git, sign this computer in to GitHub, download your projects, give this laptop its label, and install the workspace hooks. You will only need to click Authorize in a browser window once. Shall I start?"
2. **Which laptop is this?** Ask: "Is this your second laptop (L2) or a new one (L3)?" Never assume. Note the answer.
3. **Git:** `git --version`. If missing: `winget install --id Git.Git -e --source winget --scope user`, then check again.
4. **Where do the projects live (one place):** `D:\Projects` if drive D: exists, otherwise `%USERPROFILE%\Projects`. Create it.
5. **GitHub sign-in (no token to type or remember):** first test whether it already works: `git ls-remote https://github.com/talasilabharat/workspace-control.git HEAD` with prompts off. If it fails, run `git clone https://github.com/talasilabharat/workspace-control.git <workspace>\workspace-control` in his terminal tab; Git Credential Manager opens a browser window; tell him to click Authorize (the same GitHub account, talasilabharat). It stores the sign-in in Windows Credential Manager for every future session and account on this Windows user.
6. **Register the laptop and download everything:** `powershell -NoProfile -File <workspace>\workspace-control\scripts\setup-laptop.ps1 -Root <workspace> -Label <L2|L3>` (gives the label, registers it, downloads every project, syncs).
7. **Hooks (standing permission):** `powershell -NoProfile -File <workspace>\workspace-control\scripts\install-global-hooks.ps1`. Check the output lists the three hooks.
8. **GitLab backup sign-in:** follow `reference/credentials.md` (never ask him to recall or recreate an old token). If the office network is not reachable now, skip it, say so, and do it the next time on the office network (the check will remind).
9. **Account and plugin:** run `start-check.ps1`; the "Delivery agents" lines must say this account's Claude has the newest delivery-team. If older: in the browser pane (he is signed in to claude.ai) Customize > Plugins > Add > Manage marketplaces > claude-agent-team > Check for updates; then ask for a new session.
10. **Prove it:** `start-check.ps1` has 0 FAIL, and the WARNs left are explained (for example "GitLab not reachable"). `sync-standards.ps1 -Check` says 0. Write one line into `workspace-control\.claude\project-state.md` (G and J): the label, the date, the surface. Say: "Done. Open a new session and say Start; it will start from your project list."

## How work flows between accounts and laptops (so he can trust it)
- Every account and laptop works in its own copy of each project. At the start of a session, at the end of each turn, and during a long session every 10 minutes, the hooks sync that project: newer work on GitHub is downloaded and replaces older local files; local work is committed (secrets scanned first) and uploaded; nothing is forced. If two sides changed the same lines the sync undoes its merge, raises an ALERT and nothing is lost.
- Work pushed from another laptop or account therefore appears here at the next session start, or within about 10 minutes in a running session. The project's extension files are deployed to the live folder by the project's own sync, and the extension reloads itself.
- The GitLab backup is copied from whichever laptop is on the office network first.
- The delivery agents and the skills update by themselves through claude.ai ("Sync automatically").
