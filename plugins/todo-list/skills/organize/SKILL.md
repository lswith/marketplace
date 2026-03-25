---
name: organize
description: >
  Determine where a task goes and what form it should take. Handles the full
  GTD organizing decision: 2-minute rule, single action vs multi-step, container
  type (parent task or project), area routing, container setup, and first action.
  Works for new tasks during inbox processing AND existing items whose scope has
  changed during backlog review. Use whenever a clarified task needs organizing
  or an existing outcome's structure feels wrong for its content.
argument-hint: task name or outcome name
---

# Organize

You are helping decide where a task goes and what form it should take. This skill handles two contexts:

- **New items** — a clarified, actionable task that needs routing, container setup, and area assignment.
- **Existing items** — an outcome whose scope has changed and may need a different container type.

Determine which context you're in from the input and follow the appropriate path.

---

## Path A: New Item

The task has already been clarified (clear name, useful description, confirmed actionable). Walk through these steps in order.

### A1. Two-Minute Rule

Could the user knock this out right now in under two minutes?

- If **obviously quick** (e.g. "Reply to Sarah's email about Friday", "Text Mike the address"), suggest skipping it: "This seems like a 2-minute job — want to just do it now?"
- If the user says **yes** — leave the task in the inbox for them to do and move on. Don't wait for them to complete it.
- If the user says **no** or it's clearly not quick — move to A2.
- Don't ask the 2-minute question for tasks that are obviously not quick.

### A2. Complexity Check

Does this task require more than one step to complete?

- If **obviously single-step** (e.g. "Buy running shoes", "Pay electricity bill") — go to A3.
- If **obviously multi-step** (e.g. "Plan holiday to Japan", "Set up new accounting system") — go to A4.
- If **ambiguous**, ask: "Could you knock this out in one step, or would it take a few?"

### A3. Route Single Action

This is a single-action task. Route it to its area.

1. Fetch the user's existing top-level projects (areas).
2. Suggest the most likely area: "This looks like it belongs under [area] — sound right?"
3. If the user disagrees, let them pick.
4. Move the task to the chosen area.
5. Confirm: "Moved to [area]." Don't ask about priority, labels, due dates, or any other metadata — that's a separate step.

Done. Stop here for single actions.

### A4. Container Decision

Most multi-step items are lightweight. Default to parent task. Only escalate to a project when scope genuinely demands it.

- **Parent task** (default): Few steps (2-5), mostly sequential, bounded. You can see the finish line from here. Examples: getting a car serviced, renewing a passport, fixing a leaky tap.
- **Project**: Many independent actions across different contexts, needs ongoing management and review over weeks or months, would benefit from sections or grouping. Examples: planning an overseas holiday, launching a consulting business.

If the container type is obvious, state it confidently:
- "This needs a few steps — I'd set it up as a parent task."
- "This has lots of moving parts across different contexts — it's a project."

If ambiguous, ask: "Can you see the handful of steps to get this done, or is this bigger — something you'd want to track as an ongoing project?"

### A5. Define the Outcome

The outcome name should describe a finished state, not an activity. If the task name already implies a clear outcome, propose it directly. Only ask when the outcome is genuinely unclear.

Good outcome names answer "what does done look like?":
- "Japan holiday booked" not "Plan holiday to Japan"
- "New accounting system live" not "Set up accounting"
- "Kitchen tap fixed" not "Fix kitchen tap"
- "Car serviced and roadworthy" not "Get car serviced"

### A6. Check for Existing Outcomes

Search the user's existing projects and parent tasks for similar or overlapping outcomes.

- If a match exists, propose merging: "You already have an outcome called [name] — should this go there, or is it separate?"
- If merge — add the first action (A9) to the existing outcome. Skip area and container creation.
- If separate — continue to A7.

### A7. Assign an Area

Outcomes live under top-level projects that act as areas. Suggest an area based on context and the user's existing top-level projects.

- "This looks like it belongs under [area] — sound right?"
- If the user disagrees, let them pick.

### A8. Create the Container

Act on the container decision from A4 — don't re-ask.

- **Parent task**: Create a task in the chosen area. The task name is the outcome name from A5.
- **Project**: Create a sub-project under the chosen area. The project name is the outcome name from A5.

**Strip scheduling metadata.** If the original inbox task has a priority other than p4, a due date, or `next`/context labels, remove them silently. These are leftovers from when it was a single action — they don't belong on an outcome container.

- Reset priority to p4 (default)
- Remove any due date
- Remove `next` and any context labels
- Keep the `someday` label if present (outcome-level state)
- Keep any deadline if present (hard external dates apply to outcomes)
- Keep the description (outcome-level context)

### A9. First Action

Every outcome needs a concrete first step. If the first action is obvious from context, propose it. Otherwise ask: "What's the very first thing you'd need to do?"

The first action should be:
- A single, concrete step (not another multi-step outcome)
- Something the user can do right now or soon
- Specific enough to act on without thinking

Create it in the container:
- **Parent task**: create as a sub-task of the parent.
- **Project**: create as a task in the new project.

If the user mentioned a hard external date during the conversation (e.g. "filing deadline is April 15"), set a **deadline** on the first action. Don't ask about deadlines separately — just pick them up from what was already said.

### A10. Active or Someday

Ask: "Is this something you're tackling now, or more of a someday thing?"

- **Active** — the outcome stays in its area. Done.
- **Someday** — apply the `someday` label to the outcome. It stays in its natural area.

If it's obviously one or the other from context, state it confidently:
- Specific timeframe, date, or hard external deadline — clearly active.
- "Maybe one day", "no rush", "always wanted to" with no timeframe — clearly someday.

### A11. Clean Up

Delete or complete the original inbox task — it's now represented by the outcome and its first action.

---

## Path B: Existing Item (Restructure)

You are given an outcome (parent task or project) with its name, area, container type, and full task/sub-task list including labels, priorities, and due dates. Check completed tasks too — history matters.

### B1. Assess Fit

Silently evaluate the outcome against its current container type. Don't walk through a checklist out loud.

**A parent task may have outgrown its container if:**
- It has more than 5 sub-tasks
- Sub-tasks span different contexts (different context labels)
- Sub-tasks are independent rather than sequential
- The scope would benefit from sections or grouping

**A project may have shrunk past its container if:**
- It has 3 or fewer active tasks
- Tasks are sequential, not parallel
- No sections exist, or sections are empty or hold a single task
- The remaining scope is bounded — you can see the finish line
- It has few or no completed tasks — it was always small, not just winding down

**Completed tasks matter.** A project with 2 remaining tasks but 20 completed ones was genuinely complex — it's just finishing up. A parent task that has churned through many completed sub-tasks may have been a project all along. Look at the full history, not just the current snapshot.

These are signals, not rules. Use judgment — the question is whether the container is creating friction or overhead, not whether it hits some threshold.

**If the container fits** — return silently. Most outcomes will not need restructuring.

**If there's a genuine mismatch** — move to B2.

### B2. Propose the Change

Present the mismatch briefly with the key signal:

- **Parent task -> project**: "[Outcome name]" has grown to N sub-tasks across different contexts — this looks more like a project. Want to convert it?
- **Project -> parent task**: "[Outcome name]" is down to N sequential tasks with no sections — a parent task would be simpler. Want to convert it?

Wait for the user's response.

- If **yes** — proceed to B3.
- If **no** — accept it and move on.

### B3. Migrate

**Parent task -> project:**
1. Create a new sub-project under the same area, using the outcome name.
2. Move all sub-tasks into the new project.
3. Preserve all task metadata (labels, priorities, due dates, deadlines).
4. Delete the old parent task.
5. Confirm: "Converted to a project under [area]."

**Project -> parent task:**
1. Create a new parent task in the same area, using the outcome name.
2. Move all tasks as sub-tasks of the new parent task.
3. Preserve all task metadata (labels, priorities, due dates, deadlines).
4. If the outcome had a `someday` label, apply it to the new parent task.
5. Archive or delete the old project.
6. Confirm: "Converted to a parent task under [area]."

---

## Rules

- One question at a time. Ask, wait, then act.
- Be opinionated. The human provided context during clarify — make confident decisions here. Most routing should take 0-1 questions.
- Default to parent task for multi-step items. Only suggest a project when scope genuinely warrants ongoing management.
- Don't create multiple sub-tasks, sections, or a full plan. Just the outcome and one first action. The user will build it out as they work.
- For restructuring, stay silent when nothing is wrong. Don't say "Restructuring check: no issues found."
- Preserve everything during migration. Don't change names, priorities, labels, due dates, or deadlines. This is a structural change, not a re-plan.
- Look up projects, tasks, and areas by name at runtime — never hardcode IDs.
- Keep it brisk. New items: 60-second setup. Restructuring: 15-second check.
