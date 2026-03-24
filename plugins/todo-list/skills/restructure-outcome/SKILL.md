---
name: restructure-outcome
description: >
  Evaluate whether an outcome's container type (parent task vs sub-project) still
  fits its actual scope. A parent task that has grown complex may need to become a
  project; a project that has shrunk may work better as a parent task. Use during
  weekly review after reviewing each outcome's health, or whenever an outcome's
  scope has clearly shifted. Use whenever reviewing outcomes and the structure
  feels wrong for the content.
---

# Restructure Outcome

You are helping the user evaluate whether an outcome's container type still matches its scope. Outcomes start as either a parent task (lightweight, few steps) or a sub-project (complex, many actions). Over time, scope changes — a simple task grows complicated, or a big project simplifies down to a handful of steps. Your job is to spot the mismatch and help migrate if needed.

## Input

You will be given an outcome (either a parent task or sub-project) with its name, area, container type, and full task/sub-task list including labels, priorities, and due dates. You should also check the outcome's completed tasks — the history of what was done matters as much as what remains.

## Process

### 1. Assess Fit

Silently evaluate the outcome against its current container type. Don't walk through a checklist out loud — just determine whether the container still fits.

**A parent task may have outgrown its container if:**
- It has more than 5 sub-tasks
- Sub-tasks span different contexts (different context labels)
- Sub-tasks are independent rather than sequential — they could be worked in any order
- The scope would benefit from sections or grouping

**A project may have shrunk past its container if:**
- It has 3 or fewer active tasks
- Tasks are sequential, not parallel
- No sections exist, or sections are empty or hold a single task
- The remaining scope is bounded — you can see the finish line
- It has few or no completed tasks — it was always small, not just winding down

**Completed tasks matter.** A project with 2 remaining tasks but 20 completed ones was genuinely complex — it earned its project status and is just finishing up. Don't propose converting something that's nearly done. Similarly, a parent task that has churned through many completed sub-tasks may have been a project all along. Look at the full history, not just the current snapshot.

These are signals, not rules. A parent task with 6 tightly sequential sub-tasks is fine as a parent task. A project with 2 tasks but active sections and ongoing scope is fine as a project. Use judgment — the question is whether the container is creating friction or overhead, not whether it hits some threshold.

**If the container fits** — say nothing. Return silently. Most outcomes will not need restructuring.

**If there's a genuine mismatch** — move to step 2.

### 2. Propose the Change

Present the mismatch briefly with the key signal, and propose the new container type:

**Parent task that should be a project:**
> "[Outcome name]" has grown to N sub-tasks across different contexts — this looks more like a project than a parent task. Want to convert it?

**Project that should be a parent task:**
> "[Outcome name]" is down to N sequential tasks with no sections — a parent task would be simpler. Want to convert it?

Wait for the user's response.

- If **yes** — proceed to step 3.
- If **no** — accept it and move on. Don't argue.

### 3. Migrate

**Parent task → project:**
1. Create a new sub-project under the same area, using the outcome name.
2. Move all sub-tasks from the parent task into the new project.
3. Preserve all task metadata (labels, priorities, due dates, deadlines).
4. Delete the old parent task.
5. Confirm: "Converted to a project under [area]."

**Project → parent task:**
1. Create a new parent task in the same area project, using the outcome name.
2. Move all tasks from the project as sub-tasks of the new parent task.
3. Preserve all task metadata (labels, priorities, due dates, deadlines).
4. If the outcome had a `someday` label, apply it to the new parent task.
5. Archive or delete the old project.
6. Confirm: "Converted to a parent task under [area]."

## Rules

- **Silent when nothing is wrong.** Most outcomes don't need restructuring. If the container fits, return immediately with no output.
- **One question only.** This is a single yes/no decision — "should we convert?" Don't ask follow-up questions about sections, grouping, or reorganisation. Just migrate as-is.
- **Preserve everything.** Don't change task names, priorities, labels, due dates, or deadlines during migration. This is a structural change, not a re-plan.
- **Don't second-guess the user.** If they say no, the current container stays. They may have reasons you can't see.
- **Don't narrate your process.** If the container fits, don't say "Restructuring check: no issues found." Just move on silently.
- **Keep it brisk.** This is a 15-second check, not a planning session.
