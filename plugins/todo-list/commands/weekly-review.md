---
description: Weekly review of all projects and tasks — ensure the system is current and trusted (GTD Reflect)
allowed-tools:
  [
    "Read",
    "Skill",
    "AskUserQuestion",
    "mcp__claude_ai_Todoist__find-tasks",
    "mcp__claude_ai_Todoist__find-projects",
    "mcp__claude_ai_Todoist__find-labels",
    "mcp__claude_ai_Todoist__find-sections",
    "mcp__claude_ai_Todoist__add-tasks",
    "mcp__claude_ai_Todoist__update-tasks",
    "mcp__claude_ai_Todoist__complete-tasks",
    "mcp__claude_ai_Todoist__delete-object",
    "mcp__claude_ai_Todoist__add-comments",
    "mcp__claude_ai_Todoist__add-projects",
    "mcp__claude_ai_Todoist__reschedule-tasks",
    "mcp__claude_ai_Todoist__fetch-object",
    "mcp__claude_ai_Todoist__get-overview",
    "mcp__claude_ai_Todoist__update-projects",
    "mcp__claude_ai_Todoist__find-completed-tasks",
  ]
---

# Weekly Review

Review all outcomes and tasks to ensure the system is current and trusted. The goal is confidence that nothing is slipping through the cracks.

## Setup

1. Fetch the full overview (project hierarchy and task counts).
2. Fetch all projects to identify areas and active outcomes (sub-projects).
3. Fetch existing labels.
4. Fetch all tasks with the `next` label.
5. Fetch all tasks with the `waiting` label.
6. Fetch all tasks and projects with the `someday` label.
7. Fetch parent tasks (tasks with sub-tasks) across all area projects — these are lightweight outcomes that need reviewing alongside projects.
8. Check the Inbox count.
9. Present a summary:

> **Weekly Review**
> - Inbox: N items
> - Active outcomes: N (projects + parent tasks)
> - Next actions: N
> - Waiting for: N
> - Someday/maybe: N
>
> Let's get started.

## Phase 0: Get Clear

If the inbox is not empty, tell the user: "You have N items in your inbox. Want to process those first with `/process-inbox`, or skip to the review?"

- If they want to process the inbox, tell them to run `/process-inbox` and come back. Don't re-implement inbox processing here.
- If they want to skip, continue.

## Phase 1: Outcome Review

Loop through each **active outcome** — both sub-projects and parent tasks (not top-level area projects). For each:

1. Present: **Outcome 1 of N:** [name] ([type: project/parent task], [X tasks, Y next actions])
2. Load the `review-outcome` skill using the Skill tool.
3. Act on the skill's output (complete outcome, create next action, defer to someday, update name, or confirm).
4. **If the outcome name or scope changed**, the outcome's existing next action may no longer be the right one. Load the `clarify-task` skill on the outcome's current next action to re-clarify it before moving on.
5. Fetch the outcome's completed tasks, then **always** load the `restructure-outcome` skill using the Skill tool — passing both active and completed task counts. Do not skip this step or pre-assess fit yourself; the skill makes the determination.
6. Move to the next outcome.

Skip top-level area projects themselves (Baby, Personal, Zoe, Work, Finance) — only review the outcomes under them.

## Phase 1.5: Outcome Relationships

After reviewing all individual outcomes, step back and look at the full landscape:

1. Load the `review-project-relationships` skill using the Skill tool.
2. Work through any overlaps, dependencies, or redundancies it surfaces — one at a time.
3. Act on the user's decisions (merge outcomes, add notes, complete redundant ones, or skip).

This phase is quick when outcomes are well-separated. Skip it entirely if fewer than 3 active outcomes remain after Phase 1.

## Phase 2: Task Review

Loop through ALL tasks with the `next` or `waiting` label. For each:

1. Present: **Task 1 of N:** [name] (in [project/parent task], [label], [priority], [due date or "no date"])
2. Load the `review-task` skill using the Skill tool.
3. If the task name is vague, question-shaped, or lacks a clear outcome/action, load the `clarify-task` skill to sharpen it.
4. If the review flags a priority issue (wrong level, missing due date on P1/P2, P3/P4 with a date), load the `set-priority` skill to re-evaluate and fix it.
5. If the task is missing metadata (no priority, no context label, or a P1/P2 without a due date), load the `enrich-task` skill to fill in the gaps.
6. Act on any remaining output from the review.
7. Move to the next.

## Phase 3: Someday/Maybe Review

Loop through all items with the `someday` label — tasks, parent tasks, and projects. For each:

1. Present: **Someday 1 of N:** [name]
2. Load the `review-someday-maybe` skill using the Skill tool.
3. If an item is activated, optionally load the `enrich-task` skill on the new next action.
4. Move to the next.

## End

When all phases are done, give a brief summary:

> Done! Weekly review complete:
> - Outcomes: X reviewed, Y completed, Z deferred to someday
> - Tasks: X reviewed, Y rescheduled, Z completed/deleted, W unblocked
> - Someday/maybe: X reviewed, Y activated, Z deleted

## Rules

- **One item at a time.** Present one, finish it, move on. Don't show the full list or batch items.
- **Don't get ahead of the user.** Wait for their response at each decision point before moving forward.
- **Keep momentum.** Each item should take 10–60 seconds. If something is getting bogged down, suggest parking it.
- **Always load skills via the Skill tool.** When a step says to load a skill, you must call the Skill tool — never skip a skill call because you've already assessed the situation yourself. The skill makes the determination, not you. Follow the skill's instructions — don't inline your own version of their logic.
- **Track progress.** Keep a mental count of what happened in each phase so you can give the summary at the end.
