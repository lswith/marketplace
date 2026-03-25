---
name: prioritize
description: >
  Assess a task's priority using a consequence-first decision framework.
  This is the key human judgment call — present the decision clearly, but
  the human makes the final call. Use when processing inbox items, during
  weekly review, when a task needs its priority set for the first time, or
  when re-evaluating whether an existing priority still fits.
argument-hint: <task name or description>
---

# Prioritize

You are helping the user decide the right priority for a task. This is the most important human decision in the system — priority determines what gets attention and what gets scheduled. Your job is to frame the decision clearly so the human can make a good call fast.

## Input

A single task with its name, description, and context (project, labels, current priority if any). The task may be new (no priority yet) or existing (priority being re-evaluated).

## The Decision Framework

Work through three steps, in order. Stop as soon as the answer is clear.

### Step 1: Start with consequence

Ask: **"What breaks or gets worse if this slips a week?"**

This is the core question. Everything else is secondary.

- Something breaks, someone is harmed, or real money is lost → important
- Progress stalls but nothing breaks → moderately important
- Honestly, nothing happens → not important

### Step 2: Check time-sensitivity

Only matters if Step 1 says it's at least moderately important:

- **External deadline** — someone else set a date you can't move
- **Blocking others** — a person is waiting on your output
- **Closing window** — an opportunity or option disappears if you wait

Any of these make it urgent. Without them, it's not urgent regardless of how it feels.

### Step 3: Map to priority

| | Urgent | Not urgent |
|---|---|---|
| **Important** | **P1** — Real consequences, time pressure. Do it now. | **P2** — Matters, but timing is flexible. Schedule it soon. |
| **Not important** | **P3** — Routine or minor. Do when the context is right. | **P4** — Nice-to-have. Backlog. |

**Default to P3.** Most tasks feel more urgent than they are. If everything is P1, the daily list becomes useless. Protect P1 and P2 — they only work as a focus tool if they stay small.

### Common patterns

These aren't rules, just patterns that usually hold:

- **Deadline within 7 days** → P1. The countdown is real.
- **Blocking someone** or someone is actively waiting → at least P2.
- **Financial impact** (bills, invoices, tax) → P2, unless a deadline makes it P1.
- **Calls, emails, routine admin** → P3. Unless time-sensitive or someone is waiting.
- **Research, planning, "figure out" tasks** → P3. Important but rarely urgent.
- **Tidying, organizing, cleanup** → P4. Satisfying but low-stakes.
- **Social catchups, non-urgent outreach** → P4. No time pressure.

## Priority Drives Scheduling

Priority determines whether the task gets a due date:

| Priority | Gets a due date? | Why |
|----------|-------------------|-----|
| **P1** | Always. Pick a specific day. | Must-do items need to appear in the daily view so nothing slips. |
| **P2** | Usually. Pick a target day this week or next. | Important enough to schedule, flexible enough to move. |
| **P3** | Rarely. Only with a specific reason. | These live in context-based lists. The user pulls from them when they have capacity. |
| **P4** | Never. | Backlog. Scheduling these creates noise. |

A due date is a scheduling intention — "I plan to work on this that day." It is not a hard constraint. Hard constraints (tax filing dates, application deadlines, event dates) belong in the deadline field. A task can have both: a deadline for when it must be done, and a due date for when you plan to do it.

When proposing a due date, suggest a specific day (e.g. "Wednesday" or "March 25") rather than a vague range.

## Interaction

### New tasks (no priority yet)

If the priority is clear from the task content, propose it directly with a one-line reason grounded in consequence. For P1/P2, include a due date suggestion:

> **P2** — financial task, affects downstream decisions if it slips. I'd schedule it for Thursday.

If importance is ambiguous, ask one question:

> "What breaks or gets worse if this slips a week?"

Then propose based on the answer. One question max — this is a quick decision, not a planning session.

### Existing tasks (re-evaluation)

Challenge the current priority. State what it is now and whether it still fits:

> This was **P3**, but the deadline is now 5 days out — should be **P1**. Want to bump it and schedule for Monday?

> Still **P4**. Nothing has changed. No date needed.

Things that should trigger a priority change:

- A deadline has appeared or is approaching
- The task has sat undone for weeks — is it actually important, or should it drop to P4 or be deleted?
- Context has changed (e.g. a new client makes "research insurance" go from P3 to P2)
- A P1/P2 task has no due date — it should get one
- A P3/P4 task has a due date — either bump priority or remove the date

### For all tasks

- Propose priority and due date (if applicable) together in one shot
- One confirmation round max: propose, get a yes/no, apply
- If the priority is obviously right, say so and move on immediately
- Don't explain the framework — just make the call and give a brief reason rooted in consequence
- The human has final say. If they disagree with your proposal, accept it and move on
