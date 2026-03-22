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

Review all projects and tasks to ensure the system is current and trusted. The goal is confidence that nothing is slipping through the cracks.

## Setup

1. Fetch the full overview (project hierarchy and task counts).
2. Fetch all projects to identify areas, active projects, and Someday/Maybe.
3. Fetch existing labels.
4. Fetch all tasks with the `next` label.
5. Fetch all tasks with the `waiting` label.
6. Fetch all tasks and projects with the `someday` label or in the Someday/Maybe area.
7. Check the Inbox count.
8. Present a summary:

> **Weekly Review**
> - Inbox: N items
> - Active projects: N
> - Next actions: N
> - Waiting for: N
> - Someday/maybe: N
>
> Let's get started.

## Phase 0: Get Clear

If the inbox is not empty, tell the user: "You have N items in your inbox. Want to process those first with `/process-inbox`, or skip to the review?"

- If they want to process the inbox, tell them to run `/process-inbox` and come back. Don't re-implement inbox processing here.
- If they want to skip, continue.

## Phase 1: Project Review

Loop through each **active project** (not top-level areas, not Someday/Maybe). For each project:

1. Present: **Project 1 of N:** [name] ([X tasks, Y next actions])
2. Load the `review-project` skill using the Skill tool.
3. Act on the skill's output (complete project, create next action, move to someday, update name, or confirm).
4. **If the project name or scope changed**, the project's existing next action may no longer be the right one. Load the `clarify-task` skill on the project's current next action to re-clarify it before moving on.
5. Move to the next project.

Skip areas themselves (Baby, Personal, Zoe, Work, Finance, One-Off Tasks, Someday/Maybe) — only review the projects under them.

## Phase 1.5: Project Relationships

After reviewing all individual projects, step back and look at the full landscape:

1. Load the `review-project-relationships` skill using the Skill tool.
2. Work through any overlaps, dependencies, or redundancies it surfaces — one at a time.
3. Act on the user's decisions (merge projects, add notes, complete redundant projects, or skip).

This phase is quick when projects are well-separated. Skip it entirely if fewer than 3 active projects remain after Phase 1.

## Phase 2: Task Review

Loop through ALL tasks with the `next` or `waiting` label. For each:

1. Present: **Task 1 of N:** [name] (in [project], [label], [priority], [due date or "no date"])
2. Load the `review-task` skill using the Skill tool.
3. If the review flags a priority issue (wrong level, missing due date on P1/P2, P3/P4 with a date), load the `set-priority` skill to re-evaluate and fix it.
4. Act on any remaining output from the review.
5. Move to the next.

## Phase 3: Someday/Maybe Review

Loop through projects in the Someday/Maybe area AND tasks with the `someday` label. For each:

1. Present: **Someday 1 of N:** [name]
2. Load the `review-someday-maybe` skill using the Skill tool.
3. If an item is activated, optionally load the `enrich-task` skill on the new next action.
4. Move to the next.

## End

When all phases are done, give a brief summary:

> Done! Weekly review complete:
> - Projects: X reviewed, Y completed, Z moved to someday
> - Tasks: X reviewed, Y rescheduled, Z completed/deleted, W unblocked
> - Someday/maybe: X reviewed, Y activated, Z deleted

## Rules

- **One item at a time.** Present one, finish it, move on. Don't show the full list or batch items.
- **Don't get ahead of the user.** Wait for their response at each decision point before moving forward.
- **Keep momentum.** Each item should take 10–60 seconds. If something is getting bogged down, suggest parking it.
- **Load the right skills.** Use `review-project` for projects, `review-project-relationships` for cross-project analysis, `review-task` for next actions and waiting-for tasks, `set-priority` when a task's priority needs re-evaluating, `review-someday-maybe` for someday items, and `enrich-task` for newly activated items. Load each skill using the Skill tool when needed. Follow their instructions — don't inline your own version of their logic.
- **Track progress.** Keep a mental count of what happened in each phase so you can give the summary at the end.
