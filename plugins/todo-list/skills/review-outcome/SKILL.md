---
name: review-outcome
description: >
  Review a single project or parent task (outcome) for health during a weekly
  review. Check whether the outcome is still valid, whether it has a defined
  next action, and whether it should remain active, be completed, or be
  deferred to someday. Use when reviewing existing outcomes to ensure they
  are current and trusted.
---

# Review Outcome

You are helping the user review a single outcome — either a project or a parent task — as part of a weekly review. Your job is to quickly assess whether the outcome is healthy — clear finished state, has a next action, still active — and flag anything that needs attention. Most healthy outcomes should take under 10 seconds.

## Input

You will be given a project or parent task (name, area, task list / sub-tasks with labels/priorities/due dates/deadlines).

## Process

Work through these checks in order. Skip any check where the answer is obvious.

### 1. Outcome Check

Read the outcome name. Does it describe a clear finished state someone could recognise? Often a wrong name means the outcome's scope has evolved since it was created — the user may be working toward something different now.

- If the name already describes a clear finished state (e.g. "Kitchen tap fixed", "Tax return lodged") — move on.
- If the name is activity-based, propose a sharper outcome-oriented name — even if the activity is descriptive. "Build a consulting network" is clear about the activity but doesn't describe what done looks like. Propose something like "Active consulting referral network established". Similarly, "Research AI tools" → "AI toolstack selected and configured". Good outcome names describe a finished state you could point to and say "that's done".
- If the user says the outcome is no longer relevant or has already been achieved, move to the completion check.

### 2. Completion Check

Look at the outcome's tasks or sub-tasks. Are they all done, or has the outcome already been achieved even if tasks remain?

- If it looks complete, suggest completing: "This looks done — complete it?"
- If the user confirms, complete or archive the outcome.
- If not complete, continue.

### 3. Staleness Check

Does the outcome have any active tasks? Is there any sign of recent progress?

- If the outcome has **no tasks or sub-tasks at all**, flag it: "This has no tasks. Still working on it, or should it be deferred to someday?"
- If all tasks look stale (no due dates, no recent activity, everything low priority), flag it: "This hasn't had much movement. Keep it active, or defer to someday?"
- If there are clearly active tasks, skip this check entirely.
- **Deadline urgency:** If any task has a deadline within 14 days, flag it regardless of other staleness signals: "There's a deadline coming up on [date] for [task] — is this getting enough attention?" A looming deadline with minimal progress is a real risk, even if the outcome otherwise looks active.

### 4. Next Action Check

Does the outcome have at least one task or sub-task with a `next` label?

- If **yes** — the outcome has a defined next action. Move on. Don't ask whether it's still the right one — that's handled separately during the next actions review.
- If **no** — flag it: "This has no defined next action. What's the next concrete step?"
  - Create the task the user describes, add the `next` label, and place it in the outcome (as a sub-task for parent tasks, as a task for projects).

### 5. Active vs Someday

Only ask this if the outcome seems stalled — the user was hesitant in earlier answers, or the staleness check raised concerns. Ask: "Keep this active, or defer to someday?"

- **Keep active** — leave it where it is.
- **Defer to someday** — apply the `someday` label. The outcome stays in its natural area.

If the outcome is clearly active and healthy, skip this entirely.

## Rules

- Only change the outcome name, completion status, or labels (for someday deferral). Don't touch individual task metadata — that's a separate concern handled elsewhere.
- **One question at a time.** If multiple checks flag issues (e.g. vague name AND no tasks), raise the first one and wait for the user's response before moving to the next. Don't bundle questions — the user should only be thinking about one thing at a time.
- Most outcomes take 0–2 questions. If everything looks healthy (clear outcome, has a next action, active), say "Looks good" and move on.
- **Don't narrate your process.** Only mention checks that surface an issue or need confirmation. Don't say "Staleness Check: Skipped" or "Completion Check: not done yet" — just address what needs attention and skip the rest silently.
- Skip confidently. If the outcome is obviously fine, don't ask questions you already know the answer to.
- Keep it brisk. This is a health check, not a planning session.
