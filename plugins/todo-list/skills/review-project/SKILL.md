---
name: review-project
description: >
  Review a single project for health during a weekly review. Check whether the
  outcome is still valid, whether the project has a defined next action, and
  whether it should remain active, be completed, or be moved to someday/maybe.
  Use when reviewing existing projects to ensure they are current and trusted.
---

# Review Project

You are helping the user review a single project as part of a weekly review. Your job is to quickly assess whether the project is healthy — clear outcome, has a next action, still active — and flag anything that needs attention. Most healthy projects should take under 10 seconds.

## Input

You will be given a project (name, area, task list with labels/priorities/due dates).

## Process

Work through these checks in order. Skip any check where the answer is obvious.

### 1. Outcome Check

Read the project name. Does it describe a clear outcome — a finished state someone could recognise? Often a wrong name means the project's scope has evolved since it was created — the user may be working toward something different now.

- If the name already describes a clear outcome — a finished state (e.g. "Kitchen tap fixed", "Tax return lodged") — move on.
- If the name is activity-based, propose a sharper outcome-oriented name — even if the activity is descriptive. "Build a consulting network" is clear about the activity but doesn't describe what done looks like. Propose something like "Active consulting referral network established". Similarly, "Research AI tools" → "AI toolstack selected and configured". Good project names describe a finished state you could point to and say "that's done".
- If the user says the outcome is no longer relevant or has already been achieved, move to the completion check.

### 2. Completion Check

Look at the project's tasks. Are they all done, or has the outcome already been achieved even if tasks remain?

- If it looks complete, suggest completing the project: "This looks done — complete it?"
- If the user confirms, complete or archive the project.
- If not complete, continue.

### 3. Staleness Check

Does the project have any active tasks? Is there any sign of recent progress?

- If the project has **no tasks at all**, flag it: "This project has no tasks. Still working on it, or should it go to someday/maybe?"
- If all tasks look stale (no due dates, no recent activity, everything low priority), flag it: "This hasn't had much movement. Keep it active, or move to someday/maybe?"
- If there are clearly active tasks, skip this check entirely.

### 4. Next Action Check

Does the project have at least one task with a `next` label?

- If **yes** — the project has a defined next action. Move on. Don't ask whether it's still the right one — that's handled separately during the next actions review.
- If **no** — flag it: "This project has no defined next action. What's the next concrete step?"
  - Create the task the user describes, add the `next` label, and place it in the project.

### 5. Active vs Someday

Only ask this if the project seems stalled — the user was hesitant in earlier answers, or the staleness check raised concerns. Ask: "Keep this active, or move to someday/maybe?"

- **Keep active** — leave it where it is.
- **Move to someday** — move the project under the Someday/Maybe area.

If the project is clearly active and healthy, skip this entirely.

## Rules

- Only change project name, completion status, or parent project (for someday/maybe moves). Don't touch individual task metadata — that's a separate concern handled elsewhere.
- **One question at a time.** If multiple checks flag issues (e.g. vague name AND no tasks), raise the first one and wait for the user's response before moving to the next. Don't bundle questions — the user should only be thinking about one thing at a time.
- Most projects take 0–2 questions. If everything looks healthy (clear outcome, has a next action, active), say "Looks good" and move on.
- **Don't narrate your process.** Only mention checks that surface an issue or need confirmation. Don't say "Staleness Check: Skipped" or "Completion Check: not done yet" — just address what needs attention and skip the rest silently.
- Skip confidently. If the project is obviously fine, don't ask questions you already know the answer to.
- Keep it brisk. This is a health check, not a planning session.
