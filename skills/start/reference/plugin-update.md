# Plugin older than GitHub: update it yourself (you press "Check for updates"; Bharat does nothing except sign in if asked)

Why this exists: tested on 27 Oct 2026, claude.ai's "Sync automatically" does NOT deliver new GitHub versions by itself; only "Check for updates" does. Chat and Cowork then follow at once, and the Claude desktop app within about an hour (section 7 of `guide.md`).

## When
`start-check.ps1` says the laptop's Claude has delivery-team X but GitHub has Y, or you pushed a release.

## Steps (FULL mode, with the browser pane; Bharat signed in to claude.ai)
1. Open `https://claude.ai/customize/plugins/yours`. If it shows a sign-in page, say so in one line and wait for Bharat to sign in (only he can); then continue.
2. Press **Add**, then **Manage marketplaces**. On the `claude-agent-team` card note "Synced commit". Compare it with GitHub's newest commit: `git ls-remote https://github.com/talasilabharat/claude-agent-team.git HEAD` (first 7 characters).
3. If they differ, open the card's "..." menu and press **Check for updates**. Wait up to 15 seconds. It must say "Updated to <the new commit>" and the card must show the same "Synced commit". If it says "Sync failed", hover the badge and read the reason (usually a second `plugin.json` in the repository, or a failed validation); fix that first.
4. Open the plugin page (`https://claude.ai/customize/plugins/yours`, then Delivery team): it must show the new version.
5. Chat and Cowork read claude.ai's copy: they have it now. For Claude Code on this laptop: run `start-check.ps1`; if its copy is still older, the Claude desktop app checks claude.ai about once an hour (its log shows a full sync every 60 minutes; the quick check at a session start does not look for updates): say it arrives within the hour by itself, then check again; a new session (or `/reload-plugins`) loads it.
6. Record it in the project notes (J, one line): the old and new version and the proof ("Updated to <commit>").

## Rules
- Never press Remove. Do not change the "Sync automatically" switch (it is harmless; it does not deliver new versions by itself).
- Do not guess: after every step read what the page says; after the last step run `start-check.ps1` and show the result.
- If the pane cannot reach claude.ai (offline, sign-in page), say so honestly and do not claim the update happened.