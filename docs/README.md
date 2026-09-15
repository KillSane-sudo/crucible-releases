# Crucible documentation

Crucible is independent project-tracking and bug-tracking software for independent developers and 3D artists. Local only, no account, no cloud. This folder is the documentation for everyone who uses it and for the owner who builds it.

## For users

| Read this | When |
|---|---|
| [User guide](user-guide.md) | You want to know what a screen does, where a button is, or how the planner thinks. 23 chapters with screenshots. Also as a [PDF](manual/Crucible-User-Manual.pdf). |
| [Quick start](quick-start.md) | You have ten minutes and want a project running. |
| [Claude connector](claude-connector.md) | You want Claude (Claude Code, the desktop app or Cowork) to create projects, tasks and bugs and read your plan from any chat. Also as a [PDF](manual/Crucible-Guide-for-Claude.pdf). |
| [Prompts](CLAUDE_PROMPTS.md) | Copy-paste prompts for the connector: new project from a brief, log a day's work, playtest notes into bugs, daily check-in. |

## For the owner

| Read this | When |
|---|---|
| [Owner notes](owner-notes.md) | How Crucible is built, released and versioned; where data lives; the decisions already made; the parked ideas. |
| [Changelog](../CHANGELOG.md) | What every version added, step by step, from 0.1.0 to today. |
| [Versions](versions/) | The documentation as it was for each version (PDF snapshots). Builds are in `release/<version>/`. |
| [Design brief](DESIGN_BRIEF.md) | The visual direction and tokens, written for the UI redesign. |
| [Overview](CRUCIBLE_OVERVIEW.md) | The one-page description written for external review. |
| [Session handoff](../_SESSION_HANDOFF.md) | The running log for Claude Code sessions that work on the code. Read its RESUME HERE block first. |

## Keeping the docs current

The user guide and the connector guide are written once as HTML in `docs/manual/` and rendered to PDF and Markdown from there:

```bash
cd docs/manual && node capture.mjs && node pdf.mjs && node pdf.mjs claude-guide.html Crucible-Guide-for-Claude.pdf "Crucible 0.5 — Guide for Claude" && node to-md.mjs
```

`capture.mjs` needs the dev server running on port 1420 (it screenshots the app with the sample project). Update the manual whenever a screen changes; the Markdown and PDFs are generated, never edited by hand.
