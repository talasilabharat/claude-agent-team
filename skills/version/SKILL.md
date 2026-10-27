---
name: version
description: Use when the user types /version or asks which version of the delivery-team plugin (Delivery team, Bharat's agent team) is installed, or when it was released or last updated. Answers from this file only; no tools needed.
---
# Delivery team plugin - installed version

Reply in plain words, short, using only the facts below. Do not search files, GitHub or the web for this.

- Plugin: delivery-team (Bharat's delivery agent team)
- Installed version: **1.3.6**
- Released: 27 Oct 2026
- What this version changed: the `start` skill now keeps the plugin current itself (it presses "Check for updates" in claude.ai when the plugin is older than GitHub), adds the plugin to a new Claude account itself, and the texts that wrongly said claude.ai follows GitHub by itself are corrected (no agent changed).
- Master copy: private GitHub repository `talasilabharat/claude-agent-team` (its CHANGELOG.md lists every version).

If the user expected a newer version than the one above, say that the copy in this app has not been updated yet.
