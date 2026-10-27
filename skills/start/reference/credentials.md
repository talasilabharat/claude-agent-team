# Sign-ins and tokens: what is remembered, what is not, and what to do

Bharat cannot recall old tokens and should never have to recreate them. Rules: never ask him for a token or password in chat; never type, store, print or describe one; never ask him to "make a new token" before you have PROVEN the stored sign-in is really missing.

## 1. What is remembered (proven 27 Oct 2026)
- Sign-ins live in Windows Credential Manager, per Windows user, NOT in Claude. Git reads them by itself. So every new Claude session, and every other Claude account on the same Windows user, reuses them with nothing to do. Proof: a brand-new process with no Claude and prompts switched off reached the private GitHub repository using the stored entry `git:https://github.com`. The GitLab entry is `git:http://192.168.1.76:8009`.
- Check, without ever showing a secret: `cmdkey /list` (names only) and a read test with prompts off: `git ls-remote <url> HEAD`. If the read works, the sign-in is fine: do nothing.

## 2. A new laptop (or a new Windows user)
Credentials do not travel between laptops. Do not try to copy them.
- **GitHub:** a browser sign-in through Git Credential Manager: one click on Authorize, nothing to type or remember (`reference/bootstrap.md` step 5).
- **GitLab (office network only):** an old token cannot be recovered (GitLab shows a token once). Use one of these, in this order:
  1. **SSH key for this laptop (no token at all) - PROPOSED, to be proven on the office network.** `ssh-keygen -t ed25519 -N "" -f $env:USERPROFILE\.ssh\id_ed25519_workspace -C "<label>"` (OpenSSH is part of Windows; the private key stays on the laptop and is never shown). Add the PUBLIC key (it is not secret) in GitLab > Preferences > SSH Keys using the browser pane, where Bharat is already signed in. Read the project's SSH address from the GitLab project page (or `/api/v4/projects/<id>` field `ssh_url_to_repo`), test `ssh -T git@192.168.1.76` (port from that address) and `git ls-remote <ssh url>`, then point the backup remote at the SSH address (the sync's remote is named `backup`; `projects.json` field `gitlab`). Prove it with a real sync before relying on it. If the server does not offer SSH, use 2.
  2. **One personal access token per laptop** named `laptop-<label>` (scope `write_repository`, with an expiry date). Open the page in the browser pane and guide the clicks; the token is shown once and only Bharat saves it into Credential Manager (`git:http://192.168.1.76:8009`, user `bharat.talasila`). You never read, copy or repeat it. Then record the NAME and EXPIRY (never the value) in `projects.json` (`gitlab.tokenName`, `tokenExpires`).
- Plain http to the office GitLab also needs `git config --global credential.http://192.168.1.76:8009.allowUnsafeRemotes true`; you run it.

## 3. The MIS extension's own GitHub token
The MIS extension keeps its own GitHub token inside the browser profile (Admin > Change log & backup), per laptop. On a new laptop or browser profile it is a new fine-grained token (only the `mis-project` repository, Contents read and write), created and entered by Bharat in the extension, never in chat. The extension's data is safe meanwhile: the Admin settings and years are on GitHub and are taken back automatically once the token is entered.

## 4. Tokens that exist (names and expiry only; never values)
- GitLab `laptop-backup` (L1): expires 27 Oct 2027 (`projects.json`). Bharat is warned 30 days before. Add every new token here and in `projects.json`.
