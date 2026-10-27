# NEW project: set it up the standard way

Plain words, one step at a time. Rules of `SKILL.md` apply (no assumptions, copy what the workspace already does, automate, labels L1/L2/L3).

## 1. Understand the project first (ask, do not assume)
One or two short questions at a time; write the answers down:
- What is it for, in one or two lines? What does done look like?
- A short name (lower-case, hyphens, for example `my-app`).
- Does it touch company or personal data (Zoho exports, employee data, finance)? If yes: private repositories only, data in a git-ignored folder inside the project unless Bharat explicitly approves putting it in Git, secret scan before every push.
- Does it need outside access (Zoho, an API, a token, a service sign-in)? List each one. Bharat enters every secret himself in Windows Credential Manager or an environment variable. Never ask him to paste a token in chat; never write one into a file.
- Will it use the delivery agents? (`delivery-team:<name>`, only when he says so.)

## 2. Check what is needed (FULL mode)
Run `<workspace>\scripts\start-check.ps1` (read-only) and fix what you can (`reference/fix-issues.md`). Tell him in plain words:
- This laptop has its label and the workspace folder; Git is installed.
- GitHub works (the stored sign-in can read a private repository). GitLab: reachable only on the office network and its sign-in is stored; if not reachable now, the backup is added later.
- The delivery-team plugin is the newest; the global hooks are installed; every existing project meets the standard.

## 3. Create it (FULL mode)
1. `powershell -NoProfile -File <workspace>\scripts\new-project.ps1 -Name <name> -Purpose "<one line>"`: creates `<workspace>\<name>` (git init on branch main, `CLAUDE.md` with the workspace standard block, `.claude\project-state.md` with the LIVE STATE block, `docs\notes\`, `.gitignore`, `.gitattributes`, `README.md`) and makes the first commit.
2. The EMPTY PRIVATE GitHub repository (owner `talasilabharat`, no README, no .gitignore, no license): create it in the browser pane if Bharat is signed in to github.com, otherwise he creates it at https://github.com/new and you check it.
3. The GitLab project (private, group `bharat-projects`, same name, no README): create it in the browser pane if Bharat is signed in to the office GitLab (`http://192.168.1.76:8009`) and he is on the office network; otherwise leave it for later and say so.
4. `powershell -NoProfile -File <workspace>\scripts\new-project.ps1 -Name <name> -Github https://github.com/talasilabharat/<name>.git`: checks the repository is reachable and empty, registers the project in `projects.json` (every laptop downloads it by itself), pushes, and runs the sync.
5. Verify with evidence: `start-check.ps1 -Project <name>` is clean; `PROJECTS.md` lists the project; `sync-standards.ps1 -Check` says up to standard.
6. Write what he told you into `.claude\project-state.md` blocks A, B, C, E in the SAME turn (every outside access still missing goes into E). Detail goes into `docs\notes\`.
7. Tell him: open the next session in `<workspace>\<name>`; it starts with "Project memory loaded".

## 4. One place for everything
Every file for the project lives inside its own folder in the workspace: code, notes, data (git-ignored `data\` or `outputs\`), deliverables. Nothing in Downloads or on the Desktop. If a file turns up elsewhere, move it into the project folder and say so. A decision that applies to ALL projects goes into `GLOBAL_DECISIONS.md` and the guide, not only into this project.

## 5. Chat, and Cowork without the folder (LIGHT mode)
You cannot create folders, run scripts or sign in here. Do step 1 (the questions), write the answers as a "new project brief" Bharat can save, list the checks and steps for the laptop, and say: "Say Start in Claude Code on your laptop and choose NEW; I will set it up from this brief."

## Rules
Never overwrite an existing repository or folder; if anything exists already, stop and ask. Never force-push. Repositories are private. Scan for secrets before every push. Secrets are entered by Bharat only.
