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

Work through the Todoist inbox one task at a time. Each task gets organized, prioritized, and enriched before moving to the next. The goal is inbox zero.

## Setup

1. Fetch all tasks from the Todoist Inbox project.
2. Fetch all projects (needed for area routing and existing outcome checks).
3. Fetch existing labels (needed for enrichment).
4. Tell the user how many tasks are in the inbox: "You have N tasks in your inbox. Let's work through them."

If the inbox is empty, say so and stop.

## The Loop

Process one task at a time. For each task:

### 1. Present

Show the task name and description (if any). Keep it brief:

> **Task 1 of N:** [task name]
> [description if present]

### 2. Clarify (conditional)

Look at the task name and description. Decide: **is this genuinely vague?**

- A task is vague if it's a bare word, a topic with no verb, a question mark, or so ambiguous that no reasonable person could figure out what to do. Examples: "Website?", "James", "Google workspace".
- A task is clear enough if the intent is obvious, even if imprecise. "Sort out finances", "Call dentist", "Buy present for Mum" — these don't need clarification.

**If vague** — load the `clarify` skill using the Skill tool. The skill handles actionability (trash/reference) and sharpening the name/description.
- If the skill determines the task is **trash** — delete it and move to the next task.
- If the skill determines it is **reference** — handle as the skill directs, then move to the next task.
- If **actionable** — continue to step 3.

**If clear enough** — skip the skill entirely and continue to step 3.

This is the one decision the command makes on its own. For every other step, always load the skill.

### 3. Organize

Load the `organize` skill using the Skill tool. The skill determines:
- **2-minute task** — leave in inbox for the user to do, move to the next task.
- **Single action** — routed to an area. Continue to step 4.
- **Parent task or project** — container created with a first action. Continue to step 4, targeting the **first action** (not the container).

### 4. Prioritize

Load the `prioritize` skill using the Skill tool. This is the key human decision point — priority determines scheduling. Once priority (and due date if applicable) are confirmed, continue to step 5.

### 5. Enrich

Load the `enrich` skill using the Skill tool. Apply context labels, deadlines, due dates, and waiting-for status as appropriate. Once confirmed, move to the next task.

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
- **Don't get ahead of the user.** Wait for their response at each decision point before moving forward. The rhythm is: present, ask, wait, act, confirm, next.
- **Keep it moving.** Each task should take 30-60 seconds. If a task is getting bogged down, suggest parking it and coming back later.
- **Always load skills via the Skill tool.** When a step says to load a skill, you must call the Skill tool — never skip a skill call because you've already assessed the situation yourself. The skill makes the determination, not you. Follow the skill's instructions — don't inline your own version of their logic.
- **The one exception is clarify.** The command decides whether to load clarify based on whether the task name and description are genuinely vague. If they're clear enough, skip it. For organize, prioritize, and enrich — always load the skill, no exceptions.
- **Track progress.** Keep a mental count of what happened to each task so you can give the summary at the end.
