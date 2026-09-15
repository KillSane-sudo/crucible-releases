# Crucible — Quick start

Ten minutes from download to a planned project.

## 1. Install

1. Get `Crucible-<version>-portable.exe` (no installer, no admin) from the Releases page or from the author. Put it in any folder.
2. If you want the Claude connector, put `crucible-mcp.cjs` in the same folder.
3. Double-click the exe. Windows 10/11 only; WebView2 ships with Windows.

Your data is saved automatically under `%APPDATA%\dev.armaan.crucible\projects\`. Nothing leaves your PC.

## 2. Make your project

1. Project Settings → **New project…**
2. Name it and describe it in a sentence or two. The description drives the department recommendation, so say what kind of thing it is: game, level, asset pack, character, tool.
3. Pick a duration (14 to 365 days), hours per day and working days.
4. Step 2 shows the recommended departments with reasons. Untick what you do not need.
5. Step 3 shows each department's pipeline (the stages every asset in it will get). Edit names and hours if you like. Optionally list your first assets, one per line.
6. Step 4 is the plan preview: capacity, work, forecast. Step 5 creates it.

The project is added next to any others you have; switch between them from the name at the top of the rail.

## 3. Work a day

- **Dashboard** (key `1`) shows the next step, health and forecast.
- **Today** (key `2`) lists ranked work for the day. Log hours and progress in the row, or double-click an item to open its window.
- Found a problem? **+ Bug** on Today or "Create bug" from an item. Bugs land under the asset they belong to.
- Finished a stage? Tick it in the item's checklist or press **Mark DONE**.
- Something slipped? **Replan from today** on Today, or **APPLY PLAN** in the Planner (key `3`). Crucible never cuts work for you; it shows the deficit and options.

## 4. End of the week

- **Time log** (key `6`): where the hours went, by day, type, department and item.
- **Reports**: the weekly report, exportable as Markdown, HTML or CSV.

## 5. Optional: let Claude help

Project Settings → **Claude connector** → Copy the snippet for Claude Code or the Claude desktop app. Then, in any chat: "Create a 45-day asset-pack project called X with the departments you recommend, and add these ten assets." See [claude-connector.md](claude-connector.md).

## Keyboard

`1` Dashboard · `2` Today · `3` Planner · `4` Backlog · `5` Bugs · `6` Time log · `/` search · `+` add department · `Esc` close · double-click a row to open it.
