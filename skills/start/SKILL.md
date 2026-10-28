---
name: start
description: The ONE skill for Bharat's whole workspace. This is `delivery-team:start`: use it (never another plugin's start, such as `productivity:start`) when his message is just "Start" or "start" (alone, or with a greeting), or a session opens with no task. Not for "start" inside a task (for example "start the build"). Also use it for a NEW project, repo or Git setup; questions on how his workspace, sync, GitHub, GitLab, delivery agents, project notes or laptops (L1, L2, L3) work; anything broken, out of sync or missing; a NEW laptop or NEW Claude account (it sets everything up); or "Run the Cowork check". It greets him, checks and fixes what it can, shows the project list, and takes his path. Full in Claude Code; in Cowork with a folder it reads and writes files only; in Chat it guides.
---
# Start

## The rules (always, in every path)
1. Plain words, like to a beginner, short. Never use long dashes, only "-".
2. No assumptions. Read the real state first (run the check, open the file) before you say something is fine or broken. After any fix, run the check again and show the proof. If you do not know, ask.
3. Do not reinvent the wheel. When something is wrong or missing, first look at how the workspace ALREADY does it (`reference/guide.md`, `workspace-control\docs\notes\GLOBAL_DECISIONS.md`, the scripts in `workspace-control\scripts`, how the other projects handle it) and copy that proven way. If the problem is general, fix it in the shared place and in ALL projects (`sync-standards.ps1`), then record it. Details: `reference/fix-issues.md`.
4. YOU do the work, not Bharat. Never tell him to run a command, edit a file or click through a setup: do it yourself. When a step needs his approval (the app's safety check, an install, a deletion, anything that changes his computer or accounts): say in one or two plain lines exactly what you will do, ask for a clear YES in the chat, and on yes do it yourself, then run the check and show the proof. Standing permissions already given (27 Oct 2026): installing the workspace hooks and the global instruction block (`install-global-hooks.ps1`), and the whole new-laptop / new-account setup in `reference/bootstrap.md` once he has said yes to it. What only Bharat can give is a secret or a sign-in approval; see `reference/credentials.md` (it removes almost all of that). If the safety check refuses something even after his yes, say so honestly and ask what he wants; never route around it.
5. Laptops have labels, never real computer names: L1 = the i-exceed work laptop, L2 = his second laptop, L3 and up = new ones. The label is in a local file on each laptop. If this laptop has none, ASK which it is (never assume) and run `setup-laptop.ps1 -Label Lx`.
6. Call the delivery agents only when Bharat says so. Never change an agent's persona or instructions without his explicit approval naming the agent and the change.
7. Keep the project notes current IN THE SAME TURN as every decision, correction, proof, mistake or file change (block `## 00. LIVE STATE`).
8. ONE yes, then no more questions. Before the first change, list in ONE message everything you will do (every step, install, browser step, the laptop label question, and what you will need from him), and ask a single clear YES. After it, do all the steps without asking again. Stop only for: his GitHub Authorize click or a sign-in, a secret, the app's own safety refusal, or a failure; say exactly what you need at that moment. Never ask him a question you can answer by checking.

## Step 0: where are you running? (proven by testing on 27 and 28 Oct 2026)
| Surface | This skill | Agents | His computer (files, commands) |
|---|---|---|---|
| Claude Code (desktop app) | works | works | yes: FULL mode |
| Cowork with a folder connected (for example D:\Projects) | works (proven 28 Oct 2026) | not tested in this setup | files: read and write YES; commands: NO (proven: it looked for a way to run commands and found none) = FILES mode |
| Cowork with no folder (web or cloud) | works | CALLABLE (proven: the architect agent really ran and answered) | NO, cloud workspace only |
| Claude Chat | works | NOT callable (proven twice: no agent-starting tool exists) | NO, Anthropic's cloud sandbox only |
- FULL mode = you can run a command on his computer. Test it: run `powershell -NoProfile -Command "Test-Path D:\"` (or the equivalent); if it works and the workspace folder exists, FULL. If the tool does not exist and a workspace folder is connected, FILES mode; if no folder is connected, LIGHT mode (both at the end).
- FULL mode but no `workspace-control` folder found: this laptop or account is new: go to `reference/bootstrap.md` (Step 1 below shows when).

## Step 1: greet, check, fix (FULL mode)
- One warm line ("Hi Bharat, ready when you are.").
- Folder permission, first: if the workspace folder (`D:\Projects`) is not already a working folder of this session, ask for it with the app's folder request (view, read, download, create, edit; Git there) in the same breath as the ONE yes (rule 8). Nothing outside it.
- Work done outside Code: if the session-start message or the check says COWORK CHECK NEEDED or HELD, do `reference/cowork-intake.md` before the menu (also when he says "Run the Cowork check for <project>"). If it says PARALLEL work, tell him to finish it in Cowork and come back, and leave that project alone.
- Check, do not assume, that the delivery-team plugin is in THIS Claude account and is the newest version (`reference/bootstrap.md` Account step, `reference/plugin-update.md`). A new laptop, a new account, or both: `reference/bootstrap.md` does everything after one yes.
- No `workspace-control` folder: say "This looks like a new laptop or account. I will set everything up for you; it takes a few minutes. Shall I start?" On yes follow `reference/bootstrap.md`, then come back here.
- Otherwise run `powershell -NoProfile -File <workspace>\scripts\start-check.ps1` (read-only; `<workspace>` is `D:\Projects` on L1).
- For every WARN or FAIL do the automatic fix from `reference/fix-issues.md` yourself, then run the check again. Ask only for what the table says only he can give. If the plugin is older than GitHub, do `reference/plugin-update.md` yourself.
- Tell him the result in at most 6 plain lines: what is fine, what you fixed (and the proof), what still needs him.

## Step 2: the menu
Read `<workspace>\PROJECTS.md`. Show a numbered list (number, name, one line on what it is, notes last updated, in step or not), then:
"Which one? Type its number, or NEW for a new project, or HOW for how things work, or WRONG if something is wrong."

## Step 3: take the path he picks
- **A number (existing project):**
  1. Sync it: `powershell -NoProfile -File <workspace>\scripts\sync-all.ps1 -Only <name>` (downloads newer work from GitHub and replaces older local files, uploads local changes, backs up to GitLab on the office network). One-line result. On an ALERT: stop, explain, change nothing.
  2. If it is not on this laptop the sync downloads it. If this session is not in the project's folder, open it there with the folder tool if you have it, otherwise tell him in one line; never move files.
  3. Read its notes: `.claude\project-state.md` (MIS: `01_project_docs\MIS_HANDOFF.md`) block `## 00. LIVE STATE`, and the titles in `docs\notes\`. Run `start-check.ps1 -Project <name>` and read anything changed since the notes were last updated (by another laptop or another Claude account).
  4. Brief him in at most 8 lines: what the project is, where we stopped, decisions in force, open items, changes by someone else, any warning. Say "Agents ready: delivery-team <version>" (from the check).
  5. Ask: "What do we do today?"
- **NEW:** follow `reference/new-project.md`.
- **HOW:** answer from `reference/guide.md` (short, plain; open the section he needs).
- **WRONG:** follow `reference/fix-issues.md`.
- **New laptop or new Claude account (or both):** `reference/bootstrap.md` (the ONE MESSAGE and the table of situations). Sign-ins and tokens: `reference/credentials.md`.
- **"Run the Cowork check for <project>":** `reference/cowork-intake.md`.

## FILES mode (Cowork with a folder connected; no commands)
Read `reference/cowork-guide.md` NOW and follow it exactly. It holds the folder step, what you may and may never do, the editing marker, the inbox entry, the warning banner, and the numbered steps to give Bharat for everything that needs Claude Code (a NEW project, a new laptop or account, sync, tests, deploys). Short version:
- First line of every Cowork Start: no folder connected yet? Ask him to connect `D:\Projects` (view, read, create, edit; no deleting, no Git) and wait. Then say once that you can read and write files but cannot run commands.
- Read `<folder>\PROJECTS.md` and show the menu (Step 2) without the "in step with GitHub" column; brief a project from its notes (Step 3, points 3 and 4) and say the copy may be older than GitHub.
- Before an edit: check `.code-active` (Code working there? then wait), keep the `.cowork-editing` marker. After it: log it in `docs\notes\COWORK-INBOX.md` as PENDING and UNTESTED, and end with the warning and the exact text to paste into Code. Never claim a change was tested, pushed or deployed.
- Never: write inside `.git`, touch the workspace scripts, hooks or settings, delete or rename anything, create a project, put secrets in files, or quote the confidential MIS section.
## LIGHT mode (Chat, Cowork with no folder connected)
- Say: "I cannot see your files here, so I cannot check sync or read your notes myself." Ask which project. With a GitHub connector read `workspace-control/PROJECTS.md` and the project's notes from GitHub; otherwise ask him to attach or paste the notes (`.claude/project-state.md`, or `MIS_HANDOFF.md` for MIS; block "00. LIVE STATE").
- You cannot sync, install or check sign-ins here. If he wants a laptop or account set up: tell him in two lines to open the Claude desktop app, go to the Code tab and say "Start"; everything else happens there by itself.
- Nothing decided here may be lost: end with a short handoff note in the LIVE STATE style (decisions, proven facts, open items, next step) he can save into the project's notes (the `save` skill helps).
- Ask him to type `/version` so you can tell whether his delivery-team plugin is current.
