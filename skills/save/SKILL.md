---
name: save
description: Use when the user says "Save", "/save", "save progress" or "wrap up". Checks whether this is a good moment, saves confirmed progress into the project's state file (GitHub saving is automatic in projects with the sync hooks), then clears the chat to save tokens when that is worthwhile.
---
# Save: wrap up safely, then clear

You run this in the main chat because only the main chat has the conversation history. Keep it short and cheap. Follow Bharat's working-style rules (plain words, no jargon).

## 1. Is it the right moment? (check before saving anything)
- Call `mcp__ccd_session_mgmt__get_usage` (session_id "self") if it is available. Note tokens used, percent used, and the "Messages" share. If the tool is not available, say so and use your own judgment from how long the chat has been.
- NOT a good moment to CLEAR (still offer to save) if any of these is true: a task is half done; tests or builds are failing or were not run after the last change; the user has an unanswered question waiting; files have unsaved edits you are about to continue. Say plainly which one applies and what is left.
- Compare tokens used with the point where auto-compact starts (`autoCompactsAtPercent`): past about 70 percent of it, saving matters most.
- Clearing saves little if the "Messages" part is small (under about 40,000 tokens): then save, but say "the chat is small, clearing would save little" and do not clear.

## 2. Save progress to the project's state file
- Find the file: `MIS_HANDOFF.md` (project root or `01_project_docs/`) if it exists; otherwise `.claude/project-state.md` (create it with: Objective, Requirements, Decisions, Corrections from user, Assumptions, Tasks, Open questions).
- Read the project's `CLAUDE.md` rules first and follow them (for MIS: record every confirmed decision in MIS_HANDOFF.md; mark only what the user stated as CONFIRMED and only what was tested this session as PROVEN; anything else is labelled as a proposal).
- Add a dated section such as `## Session log - YYYY-MM-DD`: decisions made, corrections the user gave (so they are never repeated), what was done, what was verified and how, what is open, and the next step. Do not repeat what is already in the file; keep it compact.
- Never write secrets, passwords or tokens into the file. Never copy confidential sections (for MIS: section 9 of 2_About_Bharat_Memory.md).
- Read the section back from disk to prove it was written, then tell Bharat in 3-6 plain lines what was saved.
- Where there is no folder to write to (Claude Chat): write the same handoff text as a downloadable file or document and tell Bharat to add it to the Project's knowledge himself, because you cannot do that for him. In Cowork, write it into the attached folder; if no folder is attached, say so and treat it like Chat.

## 3. GitHub (only if the folder is a Git repository with changes)
- Run `git status --short`. If the project has the automatic sync (its CLAUDE.md says so), do not ask: tell Bharat the changes are saved to GitHub by the sync. If there are changes and no automatic sync, ask: "Save today's work to GitHub?" Only on a yes: scan for secrets, commit with a clear message, push to the approved remote. Never force-push, never make a repository public.

## 4. Clear the chat (only if step 1 said it is a good moment)
- Say in one line what will happen: the chat will be cleared after Bharat approves; everything important is in the state file; the old chat can be restored with "Resume previous session"; the next message can simply be "continue".
- Then call `mcp__ccd_session_mgmt__clear_session` with session_id "self". The app asks Bharat to approve; the clear happens when your reply ends. If the tool is not available, tell Bharat to type `/clear` himself in Claude Code, or to start a new chat (Chat) or a new task (Cowork) and begin with "continue" - there is no clear command in those.

## About /compact
- You cannot run `/compact`. Claude Code compacts automatically at the size set in the user's settings (`autoCompactWindow`).
- If the chat is large (60 percent or more) but it is NOT a good moment to clear because a task is in progress, tell Bharat he can type: `/compact Keep decisions, file paths and the current task` instead.
