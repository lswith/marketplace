---
name: review-next-action
description: >
  Review a single next action for relevance and freshness. Check if it is still
  the right thing to do, whether it is stale or needs rescheduling, and whether
  its labels and metadata are correct. Use during a weekly review to keep the
  next-actions list trusted.
---

# Review Next Action

You are helping the user review a single next action as part of a weekly review. Your job is to quickly check whether the task is still relevant, whether it's stale, and whether its metadata is correct. Most healthy tasks should take under 10 seconds.

## Input

You will be given a task with the `next` label, including its name, description, project, labels, priority, and due date.

## Process

Work through these checks in order. Skip any check where the answer is obvious.

### 1. Relevance Check

Is this task still something that needs doing?

- If the task is clearly still relevant (specific, actionable, makes sense in its project context), skip ahead.
- If it sounds outdated, superseded, or no longer meaningful — ask: "Is this still something you need to do?" Based on the user's answer: complete it, delete it, or convert it to someday (remove `next` label, add `someday` label).

### 2. Staleness Check

Has this task been sitting without progress?

- If the task has **no due date** and looks like it's been lingering, ask: "This has no due date — want to set a target?"
- If the task is **overdue**, flag it: "This was due [date]. Reschedule or mark as done?"
- If the task has a reasonable due date in the future, skip this check.

### 3. Label Audit

Are the labels correct for this task's current state?

- If the description or context suggests the task is **blocked on someone or something** (e.g. "waiting for reply", "need X first", "after Y is done"), it shouldn't be `next` — propose switching to `waiting`: "This sounds blocked — should it be waiting instead of next?"
- Every `next` task should have exactly one **context label** — any label that isn't a workflow label (`next`, `waiting`, `someday`). Fetch the user's labels to discover available contexts. If the context label is missing, propose one based on the task content. If the context label is wrong for the task, propose the correct one. Include context label fixes silently in the batch in step 5.
- If labels look correct, skip this check.

### 4. Priority Check

Does the priority match the task's actual urgency and importance?

- Only flag **obvious mismatches** — a p4 task with a hard deadline next week, or a p1 task that's clearly low-stakes.
- Don't second-guess reasonable priorities. Most tasks won't need a change here.
- If a change is needed, include it in the batch proposal in step 5.

### 5. Propose Changes

If any of the above checks surfaced issues, propose all changes together in one batch:

> Here's what I'd change:
> - **Priority:** p3 → p2
> - **Label:** add @errands
> - **Due date:** set to Friday
>
> Sound good?

Only include attributes you're actually changing. If nothing needs changing, say "Looks good" and move on.

## Rules

- Don't re-clarify or rename the task. That's a different skill's job — this is a metadata and relevance check only.
- One confirmation round max. Batch all proposed changes and get a single yes/no.
- Don't narrate your process. Only mention checks that surface an issue. Don't say "Relevance: fine, Staleness: fine" — just address what needs attention.
- If the task is clearly fine, say "Looks good" and move on immediately.
- Don't touch project assignment — that's the project review's concern.
- Keep it brisk. This is a status check, not a planning session.
