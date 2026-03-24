---
name: route-task
description: >
  Decide where a clarified, actionable task goes: skip it (2-minute rule),
  flag it as multi-step (parent task or project), or route it as a single
  action to its area. Use after a task has been clarified and confirmed
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
- If the user says **yes** — leave the task in the inbox for them to do and move on to the next task. Don't wait for them to complete it.
- If the user says **no** or it's clearly not quick — move to step 2.
- Don't ask the 2-minute question for tasks that are obviously not quick.

### 2. Complexity Check

Does this task require more than one step to complete?

- If **obviously multi-step** (e.g. "Plan holiday to Japan", "Set up new accounting system"), move to the container decision below.
- If **obviously single-step** (e.g. "Buy running shoes", "Pay electricity bill"), move to step 3.
- If **ambiguous**, ask: "Could you knock this out in one step, or would it take a few?"

**If multi-step — choose the container type:**

Most multi-step items are lightweight — a handful of sequential steps you can see end-to-end. These become **parent tasks** with sub-tasks. Only escalate to a full **project** when the scope clearly demands it.

- **Parent task** (default): Few steps (2–5), mostly sequential, bounded. You can see the finish line from here. Examples: getting a car serviced (book, drop off, pick up), renewing a passport (gather docs, submit, collect), fixing a leaky tap (buy parts, do the repair).
- **Project**: Many independent actions across different contexts, needs ongoing management and review over weeks or months, would benefit from sections or grouping. Examples: planning an overseas holiday (flights, accommodation, activities, insurance — different contexts, done over weeks), launching a consulting business (legal, marketing, finances — parallel workstreams).

If the container type is obvious, state it confidently:
- "This needs a few steps — I'd set it up as a parent task with sub-tasks."
- "This is a bigger effort with lots of moving parts — it's a project."

If it's ambiguous, ask: "Can you see the handful of steps to get this done, or is this bigger — something you'd want to track as an ongoing project?"

Once the multi-step decision is made, stop here. The outcome setup happens separately.

### 3. Route Single Action

This is a single-action task. Route it to its area.

1. Fetch the user's existing top-level projects (areas).
2. Suggest the most likely area based on the task content: "This looks like it belongs under [area] — sound right?"
3. If the user disagrees, let them pick.
4. Move the task to the chosen area project.
5. Confirm: "Moved to [area]." Don't ask about priority, labels, due dates, or any other metadata — that's a separate step.

## Rules

- One question at a time. Ask, wait, then act.
- Most tasks should take 0–1 questions to route. Don't overthink it.
- If the routing is obvious, suggest confidently and ask for quick confirmation rather than asking from scratch.
- Default to parent task for multi-step items. Only suggest a project when the scope genuinely warrants ongoing management.
- Look up projects by name at runtime — never hardcode IDs.
- Keep it brisk. This is a 15-second decision, not a planning session.
