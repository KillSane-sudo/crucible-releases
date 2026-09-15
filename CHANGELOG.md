# Changelog

Every version of Crucible, newest first: what was added, what changed, and where the build and the documentation of that version are kept. Builds live in `release/<version>/` (local, not in git); documentation snapshots in [`docs/versions/`](docs/versions/).

Dates are the day the version was built. Version numbers are in `package.json`, `src-tauri/tauri.conf.json`, `src-tauri/Cargo.toml` and `src/brand.ts`; git tags `v*` mark the commit.

---

## 0.7.0 — 2026-09-15 · reading & focus

Built for days when reading is hard and days when starting is hard. Nothing here changes what Crucible does with a project; it changes how it reads and how much of it is on screen at once.

**Added**
- Project Settings → Reading & focus: font (system, Atkinson Hyperlegible, OpenDyslexic; both bundled, open-licensed), text size 90–145 %, line spacing, letter spacing, theme (dark, warm, paper), calm labels (no capital-letter section labels), reduced motion. Applied everywhere at once, remembered per PC.
- Focus mode: `F` anywhere, the Focus button on Today, or Focus in any item window. One item full screen: title, description, steps with "just the next one", a timer (Space pauses). Log & close rounds the timer to quarter hours; under three minutes logs nothing. Mark done → next, Switch to next, Esc leaves without logging.
- Low-energy day: a switch at the top of Today. Hides the numbers and the tables and shows one small thing (least time left, preferably under half an hour) with Start in Focus and Something else.
- Capture key: `C` on any screen opens a one-line box; Enter files it in the backlog, unscheduled.
- Break it down: in the item window's Steps tab (and in Focus mode when an item has no steps) proposes five or six small ordered steps by item type, editable as a list before adding. Pasted lists work too.

**Changed**
- Every colour token is a CSS variable now, so themes switch without touching a component.
- Keyboard table in the manual and on the site: F and C added. Manual chapter 23 (Reading & focus) with two new screenshots.

**Files**: `src/prefs.ts`, `src/usePrefs.ts`, `src/focus.ts` (+ tests), `src/ui/FocusMode.tsx`, `src/ui/CapturePopup.tsx`, `src/fonts/`.

---

## 0.6.0 — 2026-09-15 · first public release

**Added**
- First-run welcome screen: start your project, explore the sample, or import a file.
- About box in Project Settings: version, licence, privacy line, links to the documentation and the issue tracker.
- A corrupt project file shows a clear message with the backup hint instead of silently opening the sample.
- Public releases repository with the website (GitHub Pages), documentation, changelog and issue templates; releases ship a portable zip (exe + connector + manuals + README), the installer, `crucible-mcp.cjs` and `SHA256SUMS.txt`.

**Changed**
- Installer metadata (publisher, description, category).
- Builds are not code-signed yet (no budget); the download page explains the SmartScreen prompt and lists checksums.

**From the unreleased list after 0.5.0**
- Item window: the left column (name, description, comments) is resizable with a drag handle between the two halves; the width is remembered, double-click resets it. Build: `release/0.5.0/Crucible-0.5.0-portable-resize.exe`.
- Screenshot tab: zoomable viewer. Click the image to zoom in at that point (click again to fit), mouse wheel zooms at the cursor, drag to pan, + / − / fit buttons with the percentage, "open" (system viewer) and "reveal" (folder) are separate buttons. Build: `release/0.5.0/Crucible-0.5.0-portable-zoom.exe`.

---

## 0.5.0 — 2026-09-12 · several projects + Claude connector

**Added**
- Several projects side by side. Each project has its own folder (`projects/<id>/`), its own screenshots and backup. Switch from the project name at the top of the rail or from the new Projects table in Project Settings. Delete moves a project to `projects/_trash`, never destroys it.
- One-time migration of the single 0.4 project into the new layout on first launch; old screenshots keep working.
- The New Project wizard adds a project and keeps the current one; "Replace the current project instead" is a checkbox.
- The Claude connector: `crucible-mcp.cjs`, a local MCP server for Claude Code, the Claude desktop app and Cowork. 18 tools: list/get/set current project, create project, recommend and add departments, search, get item, create item (tasks, assets with pipeline, bugs; with checklist and dependencies), update, set status, set progress, log time, add comment, plan (open/all, optionally pulling the backlog in), health, next steps, today. Everything it writes is marked with author "Claude" and tag `via-claude`. No delete.
- Project Settings → Claude connector: the two setup snippets (Claude Code, desktop app) with Copy, and whether the connector file is next to the exe.
- Saves carry the file's change stamp; a save over a file changed by the connector is refused and the app reloads instead. The app polls for connector writes every 1.5 s while idle.
- Documentation set in `docs/`: index, quick start, user guide (Markdown + PDF, chapters 21 and 22 new), connector guide (Markdown + PDF), prompts, owner notes, this changelog.
- Setup scripts that build a whole project from a written handbook through the connector; `scripts/mcp-smoke.mjs`: protocol smoke test.

**Changed**
- Pure search moved to `src/search.ts`, shared by the Search and Bugs screens and the connector.
- GitHub Actions also builds and attaches `crucible-mcp.cjs`.
- README rewritten around the independent-developer description and the docs.

**Files:** `release/0.5.0/` — portable exe, `crucible-mcp.cjs`, User Manual 0.5, Guide for Claude. Docs snapshot: `docs/versions/0.5.0/`. Tests: 116.

---

## 0.4.0 — 2026-09-10 · production system rework, item windows, search, time log

**Added**
- Schema v3: editable per-department pipelines and ignored suggestions. Older files upgrade on load.
- Department catalog extended (Concept, Sculpting, Retopology, Baking, Collision, Technical Art, Cinematics, Programming; UV and LOD split out).
- Pipeline editor per department (add, rename, estimate, type, reorder, skip, remove, reset, save as template); assets created with the pipeline as child stages; stages filed into matching departments.
- Next-step engine: blocker → continue → next stage → start → start department → add department → replan → capture, with reasons and Ignore.
- Department picker modal with recommendations and reasons; adding a department reports its impact (+hours, +days, forecast before → after, critical path, deficit).
- New navigation: PROJECT / PRODUCTION (+) / MANAGEMENT / SETTINGS.
- Dashboard and Today reworked; Bugs / Issues screen; Reports screen; department list, kanban (drag) and checklist views with filters and sort; 5-step New Project wizard with planner preview.
- Item window on the owner's mock: name, description, dated comments on the left; fields, estimate/actual/remaining/progress, slider, "+ hours", Lock, Mark DONE, Save on the right; tabs Screenshot / Children / Steps / Deps & blockers / History. In the desktop app every item opens in its own OS window, kept in sync.
- Global search with filters (type, plan state, priority, department, class, severity, day range, created range, leaves only, sort), remembered per screen; header search bar on every screen.
- Time log screen: hours by day, type, department and item, with a per-day chart against capacity.
- Rows open on double-click; Open buttons removed.
- User manual with screenshots (`docs/manual/`, PDF).
- GitHub repository with Actions building installer + portable on push and Releases on tags.

**Changed**
- Proprietary license (all rights reserved); no build instructions in the README; compiled builds only.
- `Task.location` field for bugs.

**Files:** `release/0.4.0/` — three portable builds in order (base, double-click rows, Time log), the manual 0.4. Docs snapshot: `docs/versions/0.4.0/`. Tests: 108.

---

## 0.3.0 — 2026-09-06 · Crucible production model

**Added**
- Universal work item: types task / asset / design / modeling / gameplay / improvement / bug / polish / QA / future; status, priority, class S–D, severity; estimate, actual, remaining, manual progress; planned start and end; pin, deadline, lock; dependencies; tags.
- Unlimited hierarchy with rollups; bugs attached to the asset where they were found.
- Production thread: timestamped history per item (comments with edit history, progress, time entries, screenshots, file and folder links, status/estimate/schedule/priority/class changes).
- Time logged as entries; progress manual and separate from status.
- Pipeline templates (prop, character, level, bug fix) applied as chained child stages; save your own.
- Planner v2: critical path, priority order (pins → dependencies → critical path → class → priority → gate → deadlines → department order → slack), real capacity from working days × hours/day, multi-day items, deficit with recovery options, conflicts explained, forecast and variance.
- Health and forecast (ON_TRACK / AT_RISK / LATE / CRITICAL) with reasons; scope pressure.
- Profiles (Game, Asset library, Level, Minimal, Custom) and rule-based description → structure.
- Backlog screen; weekly report with Markdown, HTML and CSV export; JSON export and import.
- Schema v2 with migrations from the v1 handoff files.
- One clean template item per department, seeded on new projects; Reset to defaults.
- Dashboard redesign round 1 (Grid direction) and app-wide design tokens; rail department picker with next-department suggestions; design brief for the redesign.
- Version shown in the window title and the rail.

**Files:** `release/0.3.0/` — portable exe. Tests: 97.

---

## 0.2.0 — 2026-09-06 · renamed to Crucible

**Added**
- Variable project length, 1 to 365 days, with presets; start date; hours per day; working days; follow-the-real-calendar.
- Checklist steps with day and note; tags.
- Auto-scheduler (deterministic: department order, dependencies, balanced hours).
- Departments: park and un-park, catalog, presets (game, asset library, minimal), reorder, reweight, normalise.
- Rule-based advisor with one-click apply.
- Git repository, `.gitattributes`, overview document for external review.

**Changed**
- Renamed from "Forgotten Temple Dashboard" to Crucible; "Forgotten Temple" becomes the sample project.

**Files:** `release/0.2.0/` — installer and portable exe.

---

## 0.1.0 — 2026-09-05 · Forgotten Temple Dashboard

**Added**
- Port of the design handoff: department and project progress rules, production gates, readiness, engine health, recommendation ranking (`src/engine.ts`, kept unchanged since).
- Dashboard, departments, days, tasks with checklists, bugs, performance fields.
- Tauri 2 desktop shell with JSON storage in the app-data folder; installer and portable builds.

**Files:** `release/0.1.0/` — installer and portable exe under the original name.
