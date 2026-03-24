---
description: Process the Todoist inbox one task at a time using a GTD workflow
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
    "mcp__claude_ai_Todoist__add-sections",
    "mcp__claude_ai_Todoist__reschedule-tasks",
    "mcp__claude_ai_Todoist__fetch-object",
    "mcp__claude_ai_Todoist__get-overview",
  ]
---

# Process Inbox

Work through the Todoist inbox one task at a time. Each task gets clarified, routed, and enriched before moving to the next. The goal is inbox zero.

## Setup

1. Fetch all tasks from the Todoist Inbox project.
2. Fetch all projects (needed to identify areas and check for existing projects/outcomes during routing).
3. Fetch existing labels (needed for enrichment).
4. Tell the user how many tasks are in the inbox: "You have N tasks in your inbox. Let's work through them."

If the inbox is empty, say so and stop.

## The Loop

Process one task at a time. For each task:

### 1. Present

Show the task name and description (if any). Keep it brief:

> **Task 1 of N:** [task name]
> [description if present]

### 2. Clarify

**Always** load the `clarify-task` skill using the Skill tool — even if the task looks clear. The skill handles actionability (trash/reference) and description enrichment, not just renaming. Never skip this step. The task might be:
- **Actionable** → sharpen the name/description, then continue to step 3.
- **Trash** → confirm with the user, delete it, move to the next task.
- **Reference** → ask where to attach it, add as a comment, delete the inbox item, move to the next task.

### 3. Route

Load the `route-task` skill using the Skill tool. The task will be routed to one of these outcomes:
- **2-minute task** → user skips it (leaves in inbox to do themselves), move to next task.
- **Parent task** → load the `setup-outcome` skill, telling it the container type is "parent task". It will define the outcome, assign an area, create the parent task, and add a first sub-task. Then clarify, prioritize, and enrich the first action — run steps 2, 4, and 5 on that sub-task (skip routing, it's already placed).
- **Project** → load the `setup-outcome` skill, telling it the container type is "sub-project". It will define the outcome, assign an area, create the project, and add a first action. Then clarify, prioritize, and enrich the first action — run steps 2, 4, and 5 on that task (skip routing, it's already in the project).
- **Single action** → the route-task skill has already moved it to an area project. Continue to step 4.

### 4. Set Priority

Load the `set-priority` skill using the Skill tool. Decide the task's priority and, for P1/P2 tasks, propose a due date. Once confirmed, continue to step 5.

### 5. Enrich

Load the `enrich-task` skill using the Skill tool. Add labels, due dates, and waiting-for status as appropriate. Once confirmed, move to the next task.

### 6. Next

After each task is fully processed, move to the next one. Don't pause for a summary between tasks — keep the momentum going.

## End

When all tasks are processed, give a brief summary:

> Done! Processed N tasks:
> - X set up as outcomes (parent tasks/projects)
> - Y moved to area projects (single actions)
> - Z deleted (trash/reference)
> - W skipped (2-minute tasks)

## Rules

- **One task at a time.** Never show the full inbox list or process multiple tasks in parallel. Present one, finish it, move on.
- **Don't get ahead of the user.** Wait for their response at each decision point before moving forward. The rhythm is: present → ask → wait → act → confirm → next.
- **Keep it moving.** Each task should take 30–90 seconds. If a task is getting bogged down, suggest parking it and coming back later.
- **Skip confidently within steps, not the steps themselves.** If a question within a step has an obvious answer (e.g. the routing is obvious), state the answer and move on rather than asking. But always load every skill — `clarify-task`, `route-task`, `enrich-task` — for every task. The skills handle more than you might expect from the step name alone.
- **Load the right skills.** Use `clarify-task` for clarification, `route-task` for routing decisions, `setup-outcome` for turning multi-step tasks into outcomes (parent tasks or projects), `set-priority` for deciding priority and scheduling, and `enrich-task` for adding remaining metadata. Load each skill using the Skill tool when needed. Follow their instructions — don't inline your own version of their logic.
- **Track progress.** Keep a mental count of what happened to each task so you can give the summary at the end.
