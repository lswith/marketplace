---
description: One-time GTD setup — bootstrap labels, areas, filters, and organize the project hierarchy
allowed-tools:
  [
    "Read",
    "AskUserQuestion",
    "mcp__claude_ai_Todoist__find-tasks",
    "mcp__claude_ai_Todoist__find-projects",
    "mcp__claude_ai_Todoist__find-labels",
    "mcp__claude_ai_Todoist__find-filters",
    "mcp__claude_ai_Todoist__find-sections",
    "mcp__claude_ai_Todoist__find-completed-tasks",
    "mcp__claude_ai_Todoist__add-tasks",
    "mcp__claude_ai_Todoist__update-tasks",
    "mcp__claude_ai_Todoist__add-projects",
    "mcp__claude_ai_Todoist__add-labels",
    "mcp__claude_ai_Todoist__add-filters",
    "mcp__claude_ai_Todoist__update-projects",
    "mcp__claude_ai_Todoist__update-filters",
    "mcp__claude_ai_Todoist__fetch-object",
    "mcp__claude_ai_Todoist__get-overview",
    "mcp__claude_ai_Todoist__project-move",
    "mcp__claude_ai_Todoist__reorder-objects",
  ]
---

# Setup GTD

One-time setup to bootstrap GTD infrastructure in Todoist. Creates workflow labels, infers context labels from the backlog, confirms areas, organizes the project hierarchy, and creates context-based filters. Run this before using `/process-inbox` or `/weekly-review` for the first time.

## Step 1: Data Gathering

1. Fetch the full overview using `get-overview`.
2. Fetch all projects using `find-projects`.
3. Fetch all labels using `find-labels`.
4. Fetch all filters using `find-filters`.
5. Fetch all active tasks using `find-tasks` with a broad filter.
6. Fetch recently completed tasks using `find-completed-tasks` (last 7 days — enough for pattern inference).

## Step 2: Audit

Categorize what exists against the GTD model:

- **Labels:** Which existing labels map to workflow labels (`next`, `waiting`, `someday`)? Which look like context labels? Which are unrelated?
- **Projects:** Which top-level projects are areas (containers like Work, Personal, Finance)? Which are outcomes? Which are orphaned (not under any area)?
- **Filters:** Do any context-based filters already exist?

Present a concise summary:

> **GTD Audit**
> - Workflow labels: `next` exists, `waiting` missing, `someday` missing
> - Context labels: none detected — will infer from tasks
> - Areas: Work, Personal look correct; 3 projects not under any area
> - Filters: none for context views
>
> Here's what I'll set up.

## Step 3: Create Workflow Labels

Create any missing workflow labels: `next`, `waiting`, `someday`. These are non-negotiable — don't ask the user. If they all exist already, skip this step silently.

## Step 4: Infer and Create Context Labels

Analyze all task names and descriptions — both active and recently completed — to infer what context labels would fit the user's actual work patterns.

**Pattern matching:**
- Verb patterns: "call" / "phone" / "ring" → `calls`
- Location signals: "at home" / "house" / "kitchen" → `home`
- Activity type: "buy" / "pick up" / "drop off" / "post" → `errands`
- Tool/mode: "email" / "research" / "review" / "write" / "design" → `desk`

**Rules for inference:**
- Only propose a label if 3+ tasks support it — don't create labels for one-off patterns.
- Cross-reference existing labels. If the user already has a label that serves the same purpose (e.g. they have `phone` and you'd propose `calls`), use theirs.
- Cap at 3–6 context labels. Fewer is better — the user can always add more later.

Present the proposed labels with 2–3 example tasks per label:

> Based on your tasks, I'd suggest these contexts:
> - **desk** — "Research flights", "Update spreadsheet", "Review contract"
> - **calls** — "Call dentist", "Phone accountant"
> - **errands** — "Pick up dry cleaning", "Buy birthday present", "Drop off parcel"
>
> Add, remove, or rename any of these?

One confirmation round. Create the approved labels using `add-labels`.

If there aren't enough tasks to infer patterns (e.g. nearly empty account), propose a sensible default set (desk, calls, errands, home) and let the user adjust.

## Step 5: Confirm Areas

Areas are top-level projects that act as containers — Work, Personal, Finance, Home, etc. They hold outcomes (sub-projects and parent tasks) and single actions.

1. Present the existing top-level projects and propose which ones are areas.
2. Auto-confirm obvious area names (Work, Personal, Finance, Home, Health, etc.) — don't ask about these.
3. For ambiguous top-level projects (e.g. "Random", "Misc", "Project X"), ask: is this an area, or should it go under one?
4. If the user's project structure suggests missing areas (e.g. lots of personal tasks but no Personal project), propose creating them.

Present as a batch:

> I'd confirm these as areas:
> - **Work** (existing)
> - **Personal** (existing)
> - **Finance** (create new)
>
> And these projects need a home:
> - "Holiday Planning" → Personal?
> - "Side Project" → Work?
>
> Sound right?

One confirmation round.

## Step 6: Move Projects Under Areas

For each project not already under an area, move it to the confirmed area using `project-move`.

- Present batch proposals grouped by target area.
- Auto-assign when the mapping is obvious (e.g. "Tax Return" → Finance).
- Ask about ambiguous ones.

Apply moves using `project-move` after confirmation. If a project is ambiguous and the user can't decide, leave it and flag for `/weekly-review`.

## Step 7: Create Filters

For each confirmed context label, create a filter using `add-filters`:
- Filter name: the context label name (e.g. "desk", "calls", "errands")
- Filter query: `@next & @[context]` (e.g. `@next & @desk`)
- Set as favorite for sidebar visibility

Also create:
- **Waiting** filter: query `@waiting`, set as favorite

Don't ask for confirmation — filters are cheap and easy to delete. Just create them and report what was created.

## Step 8: Summary + Handoff

> **Setup complete!**
> - Created X workflow labels, Y context labels
> - Created Z filters
> - Confirmed N areas
> - Moved M projects under areas
>
> Your GTD infrastructure is ready. Run `/weekly-review` to review and label your individual tasks.

## Rules

- **One-time setup.** If labels, filters, or areas already exist, don't recreate them. Skip what's already in place.
- **Batch proposals.** Group related changes and confirm in batches, not one at a time.
- **Never touch individual task metadata.** No labels on tasks, no priority changes, no enrichment, no task renaming. That's `/weekly-review` and `/process-inbox` territory.
- **Keep it moving.** The whole setup should take ~10 minutes. If a decision is getting bogged down, park it and move on.
- **No skills loaded.** This command handles everything directly — don't load any skills.
- **Idempotent.** If the user runs this again, it should detect what already exists and only fill gaps.
