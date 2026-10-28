# Cowork guide: what Cowork may do in Bharat's workspace, and how to hand over to Claude Code

Used in FILES mode (Cowork with a folder such as `D:\Projects` connected; it can read and write files but cannot run commands, git or tests: proven 28 Oct 2026). Rules of `SKILL.md` apply. The point: Bharat can work only in Cowork or only in Code; whatever Cowork changes is checked and saved to GitHub by the next Code session.

## 1. First: the folder
If no folder is connected, say in two lines and wait: "To read and edit your projects I need access to your projects folder. Please connect D:\Projects in the folder picker. I will only view, read, create and edit files there: I will not delete anything and I will not touch Git." Never ask for more than D:\Projects.
Say once, plainly: "I can read and write files here but I cannot run commands, so I cannot sync, check GitHub, run tests or set up a laptop. Claude Code does that."

## 2. Before every edit (in this order)
1. Read the project's `CLAUDE.md` and its notes (`.claude\project-state.md`, MIS: `01_project_docs\MIS_HANDOFF.md`, block `## 00. LIVE STATE`). Obey them (for MIS never quote or copy the confidential section 9 of `2_About_Bharat_Memory.md`).
2. Read `<project>\.code-active`. If it says `ACTIVE` and was changed in the last 5 minutes, Claude Code is working in that project: do NOT edit. Say: "Claude Code is working in <project> right now. Please finish there and come back." Wait.
3. Tell Bharat how old this copy is: the modified time of `<project>\.git\FETCH_HEAD` (read only) is the last contact with GitHub; nothing is downloaded from here, so another laptop's newer work may not be in this copy. If it is more than a day old, say so before editing.
4. Create or refresh the marker `<project>\.cowork-editing` (any text, for example the date and time) BEFORE the first edit and after EVERY edit. It tells Claude Code that you are editing; it counts for 5 minutes.

## 3. What you may do
- Read anything in the projects folder. Create and edit files inside the project folders. Update the project's notes (`## 00. LIVE STATE`: what changed, marked "(Cowork, untested)") and the version number ONLY where the project's `CLAUDE.md` says how, marked untested.
- Create files only inside an existing project folder.

## 4. What you must NEVER do
- Write inside any `.git` folder (reading `FETCH_HEAD`'s date is allowed). Edit `workspace-control\scripts`, `workspace-control\templates`, hooks, `.claude\settings*`, anything under the user's `.claude` folder, or the plugin folder `claude-agent-team`.
- Delete, rename or move any file or folder. (If a deletion is wanted, write it in the inbox entry and let Claude Code do it after Bharat agrees.)
- Create a new project, a new top-level folder in `D:\Projects`, or a Git repository (see section 6).
- Put passwords, tokens or keys in any file. Copy company data exports into notes.
- Say a change was tested, pushed or deployed. It was not.

## 5. After every edit session: log it, then warn
1. Append an entry to `<project>\docs\notes\COWORK-INBOX.md` (if the file is missing create it from `workspace-control\templates\COWORK-INBOX.template.md`). Keep `Status: PENDING` and the UNTESTED warning line. List every file you created or changed.
2. Write `DONE` into `.cowork-editing` (delete the marker too if you can; it expires after 5 minutes anyway).
3. End your answer with this warning, filled in:

   > WARNING: these changes were made by Cowork. They are NOT tested and NOT saved to GitHub. They stay on this laptop until Claude Code checks and pushes them. Changed in: <project(s)>.
   > To finish: open the Claude desktop app, go to the Code tab, start a new session (any folder, for example D:\Projects\workspace-control) and paste exactly this:
   > `Start. Run the Cowork check for <project(s)>.`
   > (If the Code session says nothing is waiting, tell it: the notes are in <project>\docs\notes\COWORK-INBOX.md.)

## 6. Things Cowork cannot do: give Bharat the steps for Claude Code
Do not attempt these. Give numbered, plain steps and the exact text to paste. The Code tab buttons may be named a little differently from what is written here; if Bharat sees something else, he tells you and you adjust.
Open Code: 1) open the Claude desktop app; 2) click the Code tab; 3) start a new session; 4) choose the folder `D:\Projects\workspace-control` (or the project's folder); 5) optional, fewer questions: choose a more automatic permission mode in the mode box before you paste; 6) paste the text and press Enter; 7) answer the ONE yes it asks and click Authorize only if a GitHub window opens.

- **A NEW project:** ask Bharat for the name and one line on what it is for (nothing else). Then give him the text: `Start. NEW project: name <name>, purpose <purpose>. Create it as the skill says (new-project.md): folder in D:\Projects, private GitHub repository, notes, register it. Ask me only what you cannot find out.` Tell him he will need an empty private repository `<name>` under his GitHub account; Claude Code says whether it creates it in the browser pane (with his yes) or he does.
- **Setting up a new laptop or a new Claude account:** give him the ONE message from `reference/bootstrap.md` (the same text works in Code and Cowork). Cowork cannot install or sign in; Code does.
- **Sync, GitHub status, GitLab backup, "is it pushed?":** `Start. Check every project against GitHub, run the Cowork check for anything waiting, and tell me what is saved.`
- **Tests, deploy of the MIS extension, MD5 checks:** `Start. Run the Cowork check for <project> and run its checks.` (MIS: after the deploy he presses Reload once, never Remove.)
- **Undo something Cowork changed:** tell him the files from the inbox entry; Claude Code restores them from Git after he agrees.
- **Anything else needing a command:** say so honestly and give the same kind of steps.