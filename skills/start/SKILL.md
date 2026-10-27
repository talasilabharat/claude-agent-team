---
name: start
description: The ONE skill for Bharat's whole workspace. Use when Bharat's message is just "Start" or "start" (alone, or with a greeting such as hello or good morning), or a session opens with no specific task. Do NOT use it when "start" is part of a specific task (for example "start the build"). Also use it when he wants a NEW project, repo or Git setup; asks how his workspace, sync, GitHub, GitLab, delivery agents, project notes or laptops (L1, L2, L3) work; reports something broken, out of sync or missing; or is on a NEW laptop or a NEW Claude account (it sets everything up, step by step, by itself). It greets him, checks everything and fixes what it can, shows the project list, and takes the path he picks: an existing project, a new project, how things work, or fix a problem. Works in Claude Code, Cowork and Chat (fully in Code and in Cowork linked to his computer; in Chat and unlinked Cowork it guides and hands over).
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

## Step 0: where are you running? (proven by testing on 27 Oct 2026, plugin 1.3.4)
| Surface | This skill | Agents | His computer (files, commands) |
|---|---|---|---|
| Claude Code (desktop app) | works | works | yes: FULL mode |
| Cowork linked to his computer ("Link to this computer" in the desktop app, not on claude.ai web) | not tested | not tested | Cowork says yes; NOT tested: try a command first |
| Cowork not linked (web) | works | CALLABLE (proven: the architect agent really ran and answered) | NO, cloud workspace only |
| Claude Chat | works | NOT callable (proven twice: no agent-starting tool exists) | NO, Anthropic's cloud sandbox only |
- FULL mode = you can run a command on his computer. Test it: run `powershell -NoProfile -Command "Test-Path D:\"` (or the equivalent); if it works and the workspace folder exists, FULL. If the tool does not exist, LIGHT mode (see the end).
- FULL mode but no `workspace-control` folder found: this laptop or account is new: go to `reference/bootstrap.md` (Step 1 below shows when).

## Step 1: greet, check, fix (FULL mode)
- One warm line ("Hi Bharat, ready when you are.").
- No `workspace-control` folder: say "This looks like a new laptop or account. I will set everything up for you; it takes a few minutes. Shall I start?" On yes follow `reference/bootstrap.md`, then come back here.
- Otherwise run `powershell -NoProfile -File <workspace>\scripts\start-check.ps1` (read-only; `<workspace>` is `D:\Projects` on L1).
- For every WARN or FAIL do the automatic fix from `reference/fix-issues.md` yourself, then run the check again. Ask only for what the table says only he can give.
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
- **New laptop or new Claude account:** `reference/bootstrap.md`. Sign-ins and tokens: `reference/credentials.md`.

## LIGHT mode (Chat, Cowork not linked to his computer)
- Say: "I cannot see your files here, so I cannot check sync or read your notes myself." Ask which project. With a GitHub connector read `workspace-control/PROJECTS.md` and the project's notes from GitHub; otherwise ask him to attach or paste the notes (`.claude/project-state.md`, or `MIS_HANDOFF.md` for MIS; block "00. LIVE STATE").
- You cannot sync, install or check sign-ins here. If he wants a laptop or account set up: tell him in two lines to open the Claude desktop app (Code tab, or a Cowork task linked to his computer) and say "Start"; everything else happens there by itself.
- Nothing decided here may be lost: end with a short handoff note in the LIVE STATE style (decisions, proven facts, open items, next step) he can save into the project's notes (the `save` skill helps).
- Ask him to type `/version` so you can tell whether his delivery-team plugin is current.
