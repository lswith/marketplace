---
description: Review active outcomes, tasks, and someday items — triage first, fix only what needs fixing
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
  ]
---

# Backlog Review

A lightweight review that triages everything first and only loads heavier skills when issues are flagged. Most items should pass triage quickly.

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

> **Backlog Review**
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

## Phase 1: Triage Outcomes

Loop through each **active outcome** — both sub-projects and parent tasks (not top-level area projects). For each:

1. Present: **Outcome 1 of N:** [name] ([type: project/parent task], [X tasks, Y next actions])
2. Load the **triage** skill using the Skill tool, passing the outcome and its tasks/sub-tasks.
3. If triage returns **no issues** — move to the next outcome. No further action needed.
4. If triage flags issues, act on each flag:
   - `structure` — load the **organize** skill (Path B: Existing Item) to assess and restructure the container.
   - `priority` or `no-next-action` — load the **prioritize** skill on the relevant task, or create a next action if missing.
   - `completed` — confirm with the user and complete the outcome.
   - `stale` — confirm with the user: defer to someday or keep active?
   - `urgent` — surface the urgency to the user and confirm next steps.
5. Move to the next outcome.

Skip top-level area projects themselves (e.g. Baby, Personal, Zoe, Work, Finance) — only review the outcomes under them.

## Phase 1.5: Cross-Project Check

After reviewing all individual outcomes, if **3 or more active outcomes** remain, step back and look at the full landscape:

1. Load the **triage** skill using the Skill tool, passing **all active outcomes together** so it runs the cross-project check.
2. If triage finds overlaps, dependencies, or redundancies — present each finding one at a time.
3. Act on the user's decisions (merge outcomes, add notes, complete redundant ones, or skip).

Skip this phase entirely if fewer than 3 active outcomes remain after Phase 1.

## Phase 2: Triage Tasks

Loop through ALL tasks with the `next` or `waiting` label. For each:

1. Present: **Task 1 of N:** [name] (in [project/parent task], [label], [priority], [due date or "no date"])
2. Load the **triage** skill using the Skill tool, passing the task.
3. If triage returns **no issues** — move to the next task. No further action needed.
4. If triage flags issues, act on each flag:
   - `outdated` or `stale` — confirm with the user: complete, delete, or keep?
   - `status-change` — update the label (`next` to `waiting` or vice versa) after confirming.
   - `scheduling` or `urgent` — load the **prioritize** skill to re-evaluate priority and due date.
   - `priority` — load the **prioritize** skill to re-evaluate.
   - `metadata` — load the **enrich** skill to fill in missing context labels or other metadata.
   - If the task name is genuinely vague (bare word, question-mark, ambiguous) — load the **clarify** skill.
5. Move to the next task.

## Phase 3: Someday Check

Loop through all items with the `someday` label — tasks, parent tasks, and projects. For each:

1. Present: **Someday 1 of N:** [name]
2. Load the **triage** skill using the Skill tool, passing the item.
3. If triage returns **no issues** — move to the next item. Still someday, still relevant.
4. If triage flags issues:
   - `activate` — confirm activation with the user. Remove the `someday` label. Optionally load the **enrich** skill on the item or its first next action.
   - `outdated` — confirm with the user: delete or keep?
   - `vague` — load the **clarify** skill to sharpen the name/description so it still makes sense on future reviews.
5. Move to the next item.

## End

When all phases are done, give a brief summary:

> **Backlog review complete.**
> - Outcomes: X reviewed, Y completed, Z deferred to someday
> - Tasks: X reviewed, Y updated, Z completed/deleted
> - Someday: X reviewed, Y activated, Z deleted

## Rules

- **One item at a time.** Present one, finish it, move on. Don't show the full list or batch items.
- **Don't get ahead of the user.** Wait for their response at each decision point before moving forward.
- **Keep momentum.** Triage is the gatekeeper — most items pass clean. Only load heavier skills when triage flags something. Each clean item should take seconds, not minutes.
- **Always load skills via the Skill tool.** When a step says to load a skill, you must call the Skill tool — never skip a skill call because you've already assessed the situation yourself. The skill makes the determination, not you. Follow the skill's instructions — don't inline your own version of their logic.
- **Track progress.** Keep a mental count of what happened in each phase so you can give the summary at the end.
