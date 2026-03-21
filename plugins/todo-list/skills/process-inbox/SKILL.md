---
name: process-inbox
description: >
  Process the Todoist inbox one task at a time using GTD methodology. Orchestrates
  clarify-task, route-task, enrich-task, and setup-project into a smooth loop.
  Use when the user wants to process their inbox or says something like "let's
  process", "clear my inbox", or "what's in my inbox".
---

# Process Inbox

You are helping the user process their Todoist inbox from top to bottom, one task at a time, using GTD principles. You orchestrate the other skills in sequence — your job is to keep the flow moving, not to duplicate their logic.

## Process

### 1. Fetch the Inbox

Get all tasks currently in the user's Todoist inbox (tasks with no project). Count them and tell the user:

> You have **[N] tasks** in your inbox. Let's work through them one at a time.

If the inbox is empty, say so and stop.

### 2. Process Each Task

For each task, starting from the top:

**a) Show the task.** Display the task name (and description if it has one) so the user knows what they're looking at:

> **[task name]**
> [description, if any]

**b) Clarify** — run `clarify-task`. This sharpens the name/description and checks actionability.
- If the result is **trash** → task is deleted, move to the next one.
- If the result is **reference** → task is filed as a comment on another task, move to the next one.
- If the result is **actionable** → continue to routing.

**c) Route** — run `route-task`. This decides where the task goes.
- If **2-minute task** → user does it now, task gets completed, move to the next one.
- If **project** → run `setup-project`, then move to the next one.
- If **single action** → task moves to One-Off Tasks, then `enrich-task` runs automatically as part of routing. Move to the next one.

**d) Transition.** After each task is processed, give a brief status and move on:

> Done — [N] left. Next up:

### 3. Wrap Up

When all tasks are processed:

> Inbox zero! You processed **[N] tasks**.

Give a quick summary of what happened — how many were actioned, trashed, filed as reference, turned into projects, etc. Keep it to 2-3 lines.

## Rules

- **One task at a time.** Never batch or skip ahead. The user should only think about one task at any moment.
- **Top to bottom.** Process in the order the inbox returns them. Don't re-sort or prioritise.
- **Don't duplicate skill logic.** When you run clarify-task, follow its process — don't re-implement clarification inline. Same for route-task, enrich-task, and setup-project.
- **Keep transitions tight.** Between tasks, one line is enough. Don't recap what just happened in detail.
- **Respect the user's pace.** If they want to skip a task ("come back to that one"), leave it in the inbox and move on. Don't push.
- **Handle interruptions gracefully.** If the user wants to stop mid-way ("that's enough for now"), acknowledge it, tell them how many are left, and stop.
- **No re-processing.** If a task has already been clarified or routed in this session, don't run those skills again.
- The inbox may change during processing (tasks deleted, moved, completed). Always fetch the next task fresh rather than working from a stale list.
