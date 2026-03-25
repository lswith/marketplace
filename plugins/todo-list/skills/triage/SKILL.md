---
name: triage
description: >
  Quick health check on any item — outcome (project/parent task), single action
  (next/waiting task), or someday item. Determines whether the item needs
  attention and what kind: structural, priority, staleness, completion, or
  cross-project. Use during any backlog review to decide if an item can be
  skipped or needs further work.
argument-hint: the item (or list of items) to triage
---

# Triage

You are performing a quick health check on one or more items. Your job is to determine whether each item needs attention, and if so, what kind. You are not fixing anything — you are flagging issues so the orchestrating command can delegate to the right skill.

Most items pass triage in seconds with "no issues." Keep it fast.

## Input

You will be given one or more items. Each item is one of:

- **Outcome** — a project or parent task (with its tasks/sub-tasks, labels, priorities, due dates, deadlines)
- **Single action** — a task with a `next` or `waiting` label
- **Someday item** — a task, parent task, or project with a `someday` label

If given multiple outcomes, also run the cross-project check at the end.

## Checks by Item Type

Work through the relevant checks for each item. Skip any check where the answer is obvious. Do not narrate skipped checks.

### Outcomes (projects and parent tasks)

**Relevance** — Is this outcome still relevant? If it sounds obsolete or already achieved, flag it.
- Flag: `completed` — "Looks done or no longer relevant"

**All tasks done?** — Are all tasks/sub-tasks complete? If so, the outcome itself may be ready to close.
- Flag: `completed` — "All tasks complete, outcome may be done"

**Staleness** — No tasks, no recent activity, everything low priority and undated? The outcome may need deferring.
- Flag: `stale` — "No activity, consider deferring to someday"

**Deadline urgency** — A deadline within 14 days with minimal progress is a risk, even if the outcome otherwise looks active.
- Flag: `urgent` — "Deadline approaching with limited progress"

**Next action defined?** — Does the outcome have at least one task/sub-task with a `next` label? If not, it has no entry point.
- Flag: `no-next-action` — "No defined next action"

**Container fit** — Does the container match its complexity? A parent task with more than 5 sub-tasks may need to become a project. A project with 3 or fewer tasks may be better as a parent task.
- Flag: `structure` — "Container size mismatch, may need restructuring"

**Container hygiene (parent tasks only)** — Does the parent task have leftover scheduling metadata (priority other than p4, a due date, `next` or context labels) that belongs on sub-tasks, not the container?
- Flag: `structure` — "Stale scheduling metadata on parent task"

### Single Actions (next/waiting tasks)

**If the task has a `next` label:**

- Still relevant? If it sounds outdated or superseded, flag it.
  - Flag: `outdated` — "Task may no longer be relevant"
- Blocked? If the description or context suggests the task is waiting on something, it shouldn't be `next`.
  - Flag: `status-change` — "Appears blocked, should be waiting"

**If the task has a `waiting` label:**

- Blocker cleared? If enough time has passed or context suggests the blocker may be resolved, flag it.
  - Flag: `status-change` — "Blocker may have cleared"
- Still worth tracking? If the task has been waiting a long time with no sign of progress, flag it.
  - Flag: `stale` — "Waiting a long time, may not be worth tracking"

**Metadata (all single actions):**

- Overdue? Flag it.
  - Flag: `scheduling` — "Overdue"
- Deadline within 7 days? Flag it.
  - Flag: `urgent` — "Deadline approaching"
- Deadline passed? Flag it.
  - Flag: `urgent` — "Deadline has passed"
- Missing context label on a `next` task? Flag it.
  - Flag: `metadata` — "Missing context label"
- Priority mismatch? High priority with no due date, low priority with approaching deadline, or priority that no longer fits the situation.
  - Flag: `priority` — brief description of the mismatch

### Someday Items

- **Still interesting?** If the item sounds outdated, irrelevant, or superseded, flag it.
  - Flag: `outdated` — "May no longer be relevant"
- **Time to activate?** If circumstances have clearly changed (a dependency resolved, capacity freed up, a trigger occurred), flag it.
  - Flag: `activate` — "Circumstances suggest activating"
- **Too vague?** If the name/description won't make sense in a few months, flag it.
  - Flag: `vague` — "Won't be meaningful on future review"

### Cross-Project Check (multiple outcomes only)

After triaging individual outcomes, scan across all of them for:

- **Overlaps** — two outcomes working toward similar results that might belong together.
  - Flag: `overlap` — name both outcomes
- **Dependencies** — one outcome blocked or shaped by another.
  - Flag: `dependency` — name both outcomes
- **Redundancies** — two outcomes that are essentially the same thing.
  - Flag: `redundant` — name both outcomes

Don't force connections. Most outcome pairs have no meaningful relationship.

## Output Format

For each item, output one of:

- **No issues** — say "No issues" and move on.
- **One or more flags** — list each flag with its category and a brief description.

Example output for a single item:

> **[Item name]** — No issues

> **[Item name]**
> - `stale` — No activity in weeks, consider deferring to someday
> - `no-next-action` — No defined next action

Example output for cross-project findings (appended after individual items):

> **Cross-project**
> - `overlap` — "Home office set up" and "Standing desk ordered" overlap significantly
> - `dependency` — "New website launched" depends on "Brand identity finalised"

## Rules

- This is a status check, not a fix-it session. Flag issues; don't resolve them.
- Be fast. Most items should take seconds, not minutes.
- Don't ask the user questions. Triage is an assessment, not a conversation. State your findings.
- Don't narrate your process. Don't say "Checking staleness... looks fine." Only surface findings.
- Don't touch or modify any items. No completions, no label changes, no rescheduling. Just flags.
- Keep flag descriptions to one short sentence. The orchestrating command will handle the rest.
