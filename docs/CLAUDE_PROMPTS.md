# Prompts for driving Crucible from Claude Code

Paste one of these into a fresh Claude Code chat (the `crucible` connector must be registered: see Project Settings → Claude connector). Edit the names, days and assets.

## New project with departments and first work

```
Use the Crucible connector.
Create a new project:
- name: Temple Props Pack
- description: Production-ready Unreal Engine 5 medieval props: high-poly modeling, retopology, UVs, baking, texturing, materials, LODs, collision, engine integration and QA.
- 45 days starting today, 6 hours/day, Monday to Friday.
Let Crucible recommend the departments from the description and keep its templates.
Then create these assets with the full pipeline in the modeling/environment department: Altar, Brazier, Stone Bench, Iron Gate, Broken Column.
Add one task "Reference board and style sheet" (4 h, MUST_HAVE) in the concept or design department.
Run the planner in open mode and tell me the forecast day, variance, capacity vs remaining hours, and any conflicts.
List everything you created with ids.
```

## Set up a whole project from a handbook or brief

This is the heavy one: a written brief becomes a full project with families, dependencies and estimates. Replace the
names, families and numbers with your own. The shape of the prompt matters more than the details.

```
Use the Crucible connector. Read <path to your brief>.pdf (extract the text if you cannot read it directly) and set up a Crucible project from it.

Project: name "Modular Wall Kit", 30 days starting today, 6 hours/day, Monday to Friday, profile ASSET_LIBRARY, engine Unreal Engine 5. Description: summarise the brief's rules (grid size, piece lengths, the material recipe and its variants, which texture sheets exist, LOD budgets, socket naming, and what counts as "finished"). Departments: planning, reference, modeling, texturing, materials, lods, engine, docs. No template items.

Then create the work, one item per real piece, in the brief's build order:
- Setup tasks on day 1 with a checklist (folder structure, grid snap, a test wall in engine, the master material and its first variant); anything that must be drawn or decided once goes on day 2.
- The shared texture sheets as their own items (texturing), and one "variants of the master material" item (materials).
- For every family in the brief: one parent task named "Family N · <name> (<count> pieces)" in modeling, tagged family-N, containing: a 30-minute reference session (reference dept), one MODELING item per piece named with your naming convention and the brief's acceptance checks as its checklist, a "assign the shared sheet" task (texturing), a "LODs, names, collision" task (lods), and a "wall test + screenshot" task (engine) with a three-step checklist. Chain them with dependencies: reference → pieces → sheet pass → LOD pass → wall test, and make each family's reference session depend on the previous family's wall test. Where one piece is the template for the rest, make the others depend on it.
- Give each family its own per-piece estimate in hours. Mark the core families MUST_HAVE and the optional ones NICE_TO_HAVE.
- One "Week N · screenshot + tracker line" task (docs, 0.5 h) on each Friday.

Finally run the planner in open mode with includeBacklog=true and report: item count, capacity vs remaining hours, forecast day, variance, deficit and conflicts, plus what falls after the last day. Do not create anything twice: check list_projects first and stop if a project with that name already exists.
```

## Update tasks and log a day's work

```
Use the Crucible connector on the current project.
1. Find the item "Altar" and its stages.
2. Mark the Reference stage DONE and set the Modeling stage IN_PROGRESS with 60% progress.
3. Log 3.5 hours on the Modeling stage with the note "blockout + primary forms".
4. Raise the estimate of the UV stage to 3 hours.
5. Add a comment on Altar: "Client wants more wear on the top surface."
Then show me today's ranked work and the current health.
```

## Playtest notes into bugs

```
Use the Crucible connector on the current project. Turn these notes into bugs, one per problem, with severity, repro steps, location and the right department. Attach a bug to the asset it belongs to when that asset exists (search first). Then give me a table of what you filed with ids and a count by severity.

Notes:
- fell through the floor next to the altar after jumping twice
- torch flicker is way too fast, looks like strobe
- gate opens the wrong way and clips through the wall
- menu font is unreadable at 1080p
- game froze for 2 s when the second wave spawned
```

## Daily check-in (read only)

```
Use the Crucible connector. What is my next step, what is today's ranked work, and is the project on track? If the forecast is past the end date, explain the reasons Crucible gives and which nice-to-have items it suggests deferring. Do not change anything.
```

## Add a department when the pipeline needs it

```
Use the Crucible connector. Which departments does Crucible recommend adding next and why? Add the first one it marks as suggested next, extend the assets with its stage, and tell me the planner impact (hours added, days added, forecast before and after).
```
