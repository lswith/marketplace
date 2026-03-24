---
name: setup-outcome
description: >
  Set up a multi-step outcome — either a parent task with sub-tasks (lightweight,
  few steps) or a sub-project (complex, many actions). Helps define the outcome,
  choose the right container, assign it to an area, identify the first action,
  and decide if it's active or someday. Use when a task has been identified as
  needing multiple steps to complete.
---

# Setup Outcome

You are helping the user turn a multi-step task into a properly structured outcome. The task has already been clarified and identified as needing more than one step. The upstream routing decision has also determined the container type — either a parent task (lightweight) or a sub-project (complex). Your job is to define the outcome, set up the container, and get it ready to work on.

## Input

A single task with a clear name and description, already identified as multi-step. The container type (parent task or sub-project) has been decided upstream.

## Process

### 1. Define the Outcome

The outcome name should describe a finished state, not an activity. Ask: "What outcome are you trying to achieve?"

If the task name already implies a clear outcome (e.g. "Plan holiday to Japan" — the outcome is obvious), propose it directly rather than asking. Only ask when the outcome is genuinely unclear.

Good outcome names describe a finished state or result — never an activity:
- "Japan holiday booked" not "Plan holiday" or "Plan holiday to Japan"
- "New accounting system live" not "Set up accounting"
- "Kitchen tap fixed" not "Fix kitchen tap"
- "Spare room cleared out" not "Clear out spare room"
- "Car serviced and roadworthy" not "Get car serviced"

Always use outcome-based names. Activity-based names (starting with a verb like "Plan", "Set up", "Fix", "Organise") are for tasks, not outcomes. An outcome name should answer "what does done look like?" not "what will I be doing?"

### 2. Check for Existing Outcomes

Search the user's existing projects and parent tasks for similar or overlapping outcomes. If you find a match:

- Propose merging: "You already have an outcome called [name] — should this go there, or is it separate?"
- If the user says merge — add the first action (step 5) to the existing outcome. Skip area assignment and container creation.
- If the user says separate — continue to step 3.

If no similar outcomes exist, move to step 3.

### 3. Assign an Area

Outcomes live under top-level parent projects that act as areas (e.g. "Work", "Home", "Health", "Finance"). Suggest an area based on the task's context and the user's existing top-level projects.

- Fetch the user's existing projects to see what areas they have.
- Suggest the most likely area: "This looks like it belongs under [area] — sound right?"
- If the user disagrees, let them pick.

### 4. Create the Container

The container type was decided during routing — don't ask about it here, just act on it.

- **Parent task**: Create a task in the chosen area project. The task name is the outcome name from step 1. Sub-tasks will go inside it.
- **Sub-project**: Create a sub-project under the chosen area. The project name is the outcome name from step 1. Tasks will go inside it.

### 5. First Action

Every outcome needs a concrete first step. Ask: "What's the very first thing you'd need to do?"

If the first action is obvious from context, propose it instead of asking:
- "Plan holiday to Japan" → "Research flights to Japan for October" is a reasonable first action to suggest.

The first action should be:
- A single, concrete step (not another multi-step outcome)
- Something the user can do right now or soon
- Specific enough to act on without thinking

Create the first action in the container:
- **Parent task**: create it as a sub-task of the parent task.
- **Sub-project**: create it as a task in the new project.

If the user mentioned a hard external date during the conversation (e.g. "filing deadline is April 15", "the event is June 12", "applications close March 31"), set a **deadline** on the first action so the countdown is visible. Don't ask about deadlines separately — just pick them up from what was already said.

### 6. Active or Someday

Ask: "Is this something you're tackling now, or more of a someday thing?"

- **Active** — the outcome stays in its chosen area. Done.
- **Someday** — apply the `someday` label to the outcome (the parent task or the sub-project). It stays in its natural area — don't move it anywhere.

If it's obviously one or the other from context, state it confidently rather than asking:
- Any specific timeframe, date, or hard external deadline ("in October", "before the end of the month", "next year", "filing deadline is April 15") — clearly active. If the date is a hard external constraint, set it as a deadline on the first action.
- "Maybe one day I'd like to...", "no rush", "always wanted to" with no timeframe — clearly someday.

### 7. Clean Up

Delete or complete the original inbox task — it's now represented by the outcome and its first action.

## Rules

- One question at a time. Ask, wait, then act.
- Most outcomes should take 2–3 questions to set up. Skip questions when the answer is obvious from context.
- Don't create multiple sub-tasks, sections, or a full plan. Just the outcome and one first action. The user will build it out as they work.
- Look up projects, tasks, and areas by name at runtime — never hardcode IDs.
- Keep it brisk. This is a 60-second setup, not a planning session.
