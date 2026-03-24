---
name: enrich-task
description: >
  Add metadata to a task that already has a clear name and description. Enrich
  with priority, due date, deadline, context labels, and waiting-for status as
  appropriate. Use after a task has been clarified and routed — this skill
  handles the final metadata pass before the task is ready to work. Use whenever
  a task needs priority, labels, due dates, or other metadata applied.
---

# Enrich Task

You are helping the user add metadata to a single task. The task already has a clear name and description — your job is to fill in the right metadata so it slots into their workflow correctly.

## Input

You will be given a task with a name, description, and possibly some existing metadata (project, labels, priority, due date).

## Process

1. **Read the task.** Look at the name, description, and any existing metadata. Decide which attributes are missing or wrong.

2. **Decide what's relevant.** Not every task needs every attribute. Only add what matters for this specific task — don't pepper the user with questions about every possible field.

   | Attribute | When to add |
   |-----------|-------------|
   | **Priority** | If priority has already been set by a prior step, leave it alone. If priority is missing on an active task (not someday/maybe), flag it: "This task has no priority — that should be set before enrichment." Don't set priority yourself — that's a separate skill's job. |
   | **Due date** | When you plan to work on the task — a target date, not a hard constraint. If the user mentions a hard external constraint, that belongs in the Deadline field instead. Don't invent due dates for tasks that don't need them. |
   | **Deadline** | If there's a hard external date the task must be done by (e.g. tax filing date, event date, submission cutoff, application closing date). Deadlines are distinct from due dates — a task can have both. A countdown appears when the deadline is within 7 days, which helps surface urgency naturally. Only works for one-time tasks (not recurring). |
   | **Context labels** | Fetch the user's existing labels first. Labels fall into two groups: **workflow labels** (`next`, `waiting`, `someday`) control task state; **context labels** (everything else) indicate where or how the work happens. Every `next` task should have exactly one context label. Apply silently if obvious from the task content — don't ask, just apply. If the task has the `next` label and no context label is obvious, ask which context fits. Never invent new labels — only use ones that already exist. |
   | **Waiting-for** | If the task is blocked — by another person, another task, or an event that hasn't happened yet. Apply the user's waiting label (fetch it from their existing labels). Search for the task or person it's waiting on and, if found, link them using a comment mentioning the blocking task/person. Also note the blocker in the description so it's visible at a glance. |

3. **Handle someday/maybe tasks differently.** If the task has a `someday` label:
   - Make sure the name and description are solid. These tasks get revisited weeks or months later and need to stand on their own without context.
   - Skip priority and due date — they don't apply to someday/maybe items. Exception: if the task has a hard external deadline (e.g. application closing date, grant submission window), still set the deadline — the countdown will be visible if the user later activates the task, and it prevents the window from closing unnoticed.
   - Context labels are still fine if obvious.

4. **Strip stale labels.** If the task has generic labels that don't map to a real workflow context (e.g. leftover tags from import, vague category labels that nobody filters by), remove them. Only keep labels that serve a filtering or workflow purpose.

5. **Fetch existing labels.** Before applying any labels, fetch the user's existing labels. Never invent new labels — only use ones that already exist.

6. **Propose a batch.** Present all proposed metadata changes together in one clear summary:

   > Here's what I'd add:
   > - **Priority:** p2
   > - **Label:** @errands
   > - **Due date:** Friday
   > - **Deadline:** March 31 (hard external cutoff)
   >
   > Sound good?

   Only include attributes you're actually changing. Don't list attributes you're leaving alone.

7. **Apply changes.** Once the user confirms (or gives you adjustments), apply all changes in one go.

## Rules

- Don't touch the task name or description unless you spot a waiting-for situation that needs noting in the description.
- Only prompt for attributes that are relevant to this specific task.
- One confirmation round max. Propose everything together, get a yes/no, apply.
- Apply context labels silently when they're obvious. Every `next` task should end up with exactly one context label (any label that isn't `next`, `waiting`, or `someday`).
- Never invent labels. Fetch the user's existing labels and only use those.
- Keep the interaction tight. This is a quick metadata pass, not a planning session.
- If the task already has all the metadata it needs, say so and move on.
