---
description: Plan your day by pulling work from the backlog based on priorities, dates, and context
allowed-tools:
  [
    "AskUserQuestion",
    "mcp__claude_ai_Todoist__find-tasks",
    "mcp__claude_ai_Todoist__find-tasks-by-date",
    "mcp__claude_ai_Todoist__find-labels",
    "mcp__claude_ai_Todoist__complete-tasks",
    "mcp__claude_ai_Todoist__delete-object",
    "mcp__claude_ai_Todoist__reschedule-tasks",
    "mcp__claude_ai_Todoist__update-tasks",
    "mcp__claude_ai_Todoist__fetch-object",
  ]
---

# Plan Day

A quick 2-3 minute exercise to decide what you're actually doing today. The backlog is already organized — this is about picking today's work and making fast decisions on anything overdue.

## Setup

Run these fetches in parallel:

1. Fetch tasks due today (use `find-tasks-by-date` with startDate `today` — this includes overdue tasks).
2. Fetch all P1 tasks (use `find-tasks` with filter `p1`).
3. Fetch P2 tasks due this week (use `find-tasks` with filter `p2 & 7 days`).
4. Fetch the user's existing labels (needed for context filtering).

Separate the results into:
- **Overdue** — due before today
- **Due today** — due exactly today
- **P1 undated** — priority 1 but no due date set
- **P2 this week** — priority 2 due within the next 7 days

Then ask the user: **"What's your context today — desk, home, errands, calls?"**

If the user doesn't want to specify, infer from the day of week: weekdays default to `desk`, weekends default to `home`.

## Step 1: Handle Overdue

If there are overdue tasks, present them first. These need decisions before anything else.

Show them as a numbered list:

> **Overdue (need decisions):**
> 1. [task name] — was due [date]
> 2. [task name] — was due [date]

For each overdue task, ask: **"Reschedule to today, pick a new date, complete, or drop?"**

Be opinionated — if a task is only 1-2 days overdue, suggest rescheduling to today. If it's been overdue for a week or more, gently ask if it's still relevant.

Process all overdue items before moving on. Keep it fast — one decision per task, no deep dives.

## Step 2: Present Today's Plate

Show what's already committed for today:

> **Today's plate:**
> - [task name] (P1)
> - [task name] (P2)
> - [task name] (P1, rescheduled from overdue)

Include tasks that were due today from the start, plus any overdue tasks the user just rescheduled to today.

If there are P1 tasks without a due date, flag them:

> **P1 without a date (should probably be scheduled):**
> - [task name]
> - [task name]
>
> Want to schedule any of these for today or this week?

Let the user quickly assign dates or skip. Don't push — just surface them.

## Step 3: Suggest from Context

Based on the user's context for the day, fetch tasks with the matching context label and the `next` label (e.g. filter `@next & @desk`).

From those results, pick the top 3-5 items by priority (P1 first, then P2, then P3) that are NOT already on today's plate. Present them as suggestions:

> **Also consider today** (from your @desk list):
> - [task name] (P2)
> - [task name] (P3)
> - [task name] (P3)
>
> Want to add any of these to today?

The user can accept individual items (reschedule them to today), skip all, or pick specific ones. Don't overwhelm — 3-5 suggestions max.

## Step 4: Gut Check

Count the total items on today's plate. If it's more than 7, say so:

> That's N items — might be ambitious. Want to push anything to tomorrow?

If it's 5-7, confirm the list looks good. If it's under 5, note there's room if anything comes up.

## Step 5: Wrap Up

Present the final plan:

> **Today's plan (N items):**
> 1. [task name] (P1)
> 2. [task name] (P1)
> 3. [task name] (P2)
> 4. [task name] (P3)
> ...
>
> Also handled: X rescheduled, Y completed, Z dropped.

List items in priority order (P1 first). Keep the summary tight.

## Rules

- **This is a 2-3 minute exercise.** If it's taking longer, you're going too deep. No skill loading, no enrichment, no re-prioritizing. Just surface and schedule.
- **Be opinionated.** Suggest a manageable day (5-7 items). Don't present 15 tasks and ask the user to choose — curate the list yourself and let them adjust.
- **Context matters.** A desk day and an errands day look completely different. Filter suggestions accordingly.
- **Don't create tasks.** This command surfaces and schedules existing work. If the user mentions something new, tell them to add it to the inbox.
- **Minimize decisions.** The user has ADHD — every open question is friction. Propose defaults ("I'd reschedule this to today") and let them override, rather than asking what they want to do.
- **Use reschedule-tasks for all date changes.** Never use update-tasks to change due dates — it destroys recurrence on recurring tasks.
- **P1 items always make the list.** Don't suggest skipping P1 tasks. If there are too many P1s, that's a prioritization problem to flag, not a planning problem to solve here.
