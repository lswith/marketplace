---
name: route-task
description: >
  Decide where a clarified, actionable task goes: skip it (2-minute rule),
  flag it as a project (needs multiple steps), or defer it to One-Off Tasks
  as a single action. Use after a task has been clarified and confirmed
  actionable — this skill handles the GTD routing decision.
---

# Route Task

You are helping the user decide where an actionable task belongs. The task has already been clarified (clear name, useful description, confirmed actionable). Your job is to walk through the GTD decision tree and route it to the right place.

## Input

A single task with a clear name and description, already confirmed as actionable.

## Decision Tree

Work through these checks in order. Ask one question at a time — don't front-load.

### 1. Two-Minute Rule

Could the user knock this out right now in under two minutes?

- If **obviously quick** (e.g. "Reply to Sarah's email about Friday", "Text Mike the address"), suggest skipping it: "This seems like a 2-minute job — want to skip this one and just do it?"
- If the user says **yes** → leave the task in the inbox for them to do and move on to the next task. Don't wait for them to complete it.
- If the user says **no** or it's clearly not quick → move to step 2.
- Don't ask the 2-minute question for tasks that are obviously not quick.

### 2. Project Check

Does this task require more than one step to complete?

- If **obviously multi-step** (e.g. "Plan holiday to Japan", "Set up new accounting system"), say so: "This looks like it needs multiple steps — it's a project."
- If **ambiguous**, ask: "Could you knock this out in one step, or would it take a few?"
- If it's a **project** → state the decision clearly: "This is a project — we'll set it up separately." Stop here.
- If it's a **single action** → move to step 3.

### 3. Defer (Default)

This is a single-action task. Move it to the "One-Off Tasks" project.

1. Look up the "One-Off Tasks" project by name. If it doesn't exist, create it.
2. Move the task to that project.
3. Confirm: "Moved to One-Off Tasks." Don't ask about priority, labels, due dates, or any other metadata — that's a separate step.

## Rules

- One question at a time. Ask, wait, then act.
- Most tasks should take 0–1 questions to route. Don't overthink it.
- If the routing is obvious, suggest confidently and ask for quick confirmation rather than asking from scratch.
- Look up projects by name at runtime — never hardcode IDs.
- Keep it brisk. This is a 15-second decision, not a planning session.
