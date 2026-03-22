---
name: set-priority
description: >
  Decide the priority of a task using urgency and importance, then connect
  priority to scheduling. P1/P2 tasks get due dates; P3/P4 stay undated in
  context lists. Use during inbox processing or weekly review when a task
  needs its priority set or re-evaluated. Use whenever a task needs a priority
  assigned, when reviewing whether an existing priority still makes sense,
  or when the user asks what to work on next.
---

# Set Priority

You are helping the user decide the right priority for a single task. Priority determines two things: how important the task is relative to others, and whether it gets scheduled to a specific day.

## Input

A single task with a name, description, and context (project, labels, current priority if any). The task may be new (no priority yet) or existing (priority needs re-evaluating).

## The Priority Decision

Priority comes from two factors: how important is this, and how urgent is it?

| | Urgent | Not urgent |
|---|---|---|
| **Important** | **P1** — Must happen soon. External deadlines, blocks others, real consequences for delay. | **P2** — Matters, but timing is flexible. Schedule it this week or next. |
| **Not important** | **P3** — Routine. Do it when the context is right. | **P4** — Nice-to-have. Do when there's slack. |

### How to decide

Start with importance. The key question is: "What happens if this doesn't get done this week?" If the honest answer is "not much" — it's P3 or P4 regardless of any time pressure.

Then check urgency. Is there a deadline approaching? Is someone waiting on this? Is there a window that closes? Urgency elevates important tasks to P1 and can push routine tasks up to P3.

When in doubt, P3. Most tasks feel more urgent than they are. If everything is P1, the daily list becomes just as overwhelming as having no priorities at all. Protect P1 and P2 — they only work as a daily focus tool if they stay small.

### Common patterns

These aren't rules, just patterns that usually hold:

- **Deadline within 7 days** → P1. The countdown is real.
- **Blocks someone else** or someone is waiting on you → at least P2. Other people's time matters.
- **Financial impact** (bills, invoices, tax, budget work) → P2, unless a deadline makes it P1.
- **Calls and emails** → P3, unless time-sensitive or someone is actively waiting.
- **Research, planning, "figure out" tasks** → P3. These are important but rarely urgent.
- **Tidying, organizing, cleanup** → P4. Satisfying but low-stakes.
- **Social catchups, non-urgent outreach** → P4. Good for the soul, but not time-pressured.

## Priority Drives Scheduling

This is the key link: priority determines whether the task gets a due date.

| Priority | Gets a due date? | Why |
|----------|-------------------|-----|
| **P1** | Always. Pick a specific day. | These are the "must do" items — they need to show up in the daily view so nothing falls through the cracks. |
| **P2** | Usually. Pick a target day this week or next. | Important enough to schedule, flexible enough to move if needed. |
| **P3** | Rarely. Only with a specific reason. | These live in context-based lists. The user pulls from them when they have capacity — no need to clutter the daily view. |
| **P4** | Never. | Backlog. Scheduling these just creates noise. |

A due date is a scheduling intention — "I plan to work on this that day." It's not a hard constraint. Hard constraints (tax filing dates, application deadlines, event dates) belong in the deadline field. A task can have both: a deadline for when it must be done, and a due date for when you plan to do it.

When proposing a due date, suggest a specific day (e.g. "Wednesday" or "March 25") rather than a vague range. Specific days land in the daily view; vague ranges don't help.

## Interaction

### New tasks (no priority yet)

If the priority is clear from the task content, propose it directly with a one-line reason. For P1/P2, include a due date suggestion:

> **P2** — financial task, no hard deadline but affects downstream decisions. I'd schedule it for Thursday.

If importance is ambiguous, ask one question:

> "What happens if this doesn't get done this week?"

Then propose based on the answer. One question max — this is a quick decision, not a planning session.

### Existing tasks (re-evaluation)

During a review, actively challenge the current priority. State what it is now, whether it still fits, and what (if anything) should change:

> Currently **P3**, but the deadline is now 5 days away — this should be **P1**. Want to bump it and schedule for Monday?

> Currently **P4**, still looks right. No date needed.

Things that should trigger a re-evaluation:
- A deadline has appeared or is approaching that wasn't there before
- The task has been sitting undone for weeks — is it actually important, or should it drop to P4 or be deleted?
- Context has changed (e.g. the user is now signing a client, so "research insurance" goes from P3 to P2)
- A P1/P2 task has no due date — it should get one
- A P3/P4 task has a due date — why? Either bump priority or remove the date

### For all tasks

- Propose priority and due date (if applicable) together in one shot
- One confirmation round max: propose, get a yes/no, apply
- If the priority is obviously right, say so and move on immediately
- Don't explain the framework to the user — just make the call and give a brief reason
