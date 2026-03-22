---
name: setup-project
description: >
  Convert a multi-step task into a Todoist project. Helps define the outcome,
  find or create the right project, assign it to an area, identify the first
  action, and decide if it's a priority or someday/maybe. Use when a task has
  been identified as needing multiple steps to complete — it's a project, not
  a single action.
---

# Setup Project

You are helping the user turn a multi-step task into a properly structured Todoist project. The task has already been clarified and identified as needing more than one step. Your job is to set up the project so the user can start working on it.

## Input

A single task with a clear name and description, already identified as multi-step.

## Process

### 1. Define the Outcome

The project name should describe the outcome, not the activity. Ask: "What outcome are you trying to achieve?"

If the task name already implies a clear outcome (e.g. "Plan holiday to Japan" → the outcome is obvious), propose it directly rather than asking. Only ask when the outcome is genuinely unclear.

Good project names describe a finished state or result — never an activity:
- "Japan holiday booked" not "Plan holiday" or "Plan holiday to Japan"
- "New accounting system live" not "Set up accounting"
- "Kitchen tap fixed" not "Fix kitchen tap"
- "Spare room cleared out" not "Clear out spare room"

Always use outcome-based names. Activity-based names (starting with a verb like "Plan", "Set up", "Fix", "Organise") are for tasks, not projects. A project name should answer "what does done look like?" not "what will I be doing?"

### 2. Check for Existing Projects

Search the user's existing projects for similar or overlapping ones. If you find a match:

- Propose merging: "You already have a project called [name] — should this go there, or is it separate?"
- If the user says merge → add the first action (step 4) to the existing project. Skip area assignment.
- If the user says separate → continue to step 3.

If no similar projects exist, move to step 3.

### 3. Assign an Area

Projects live under top-level parent projects that act as areas (e.g. "Work", "Home", "Health", "Finance"). Suggest an area based on the task's context and the user's existing top-level projects.

- Fetch the user's existing projects to see what areas they have.
- Suggest the most likely area: "This looks like it belongs under [area] — sound right?"
- If the user disagrees, let them pick.
- Create the project under the chosen area.

### 4. First Action

Every project needs a concrete first step. Ask: "What's the very first thing you'd need to do?"

If the first action is obvious from context, propose it instead of asking:
- "Plan holiday to Japan" → "Research flights to Japan for October" is a reasonable first action to suggest.

The first action should be:
- A single, concrete step (not another project)
- Something the user can do right now or soon
- Specific enough to act on without thinking

Create this as a task in the new project.

### 5. Priority or Someday/Maybe

Ask: "Is this something you're tackling now, or more of a someday thing?"

- **Priority (active)** → the project stays in its chosen area. Done.
- **Someday/maybe** → move the project under a top-level "Someday/Maybe" area. Create this area if it doesn't exist. The first action is still there for when the user activates the project later.

If it's obviously one or the other from context, state it confidently rather than asking:
- Any specific timeframe or date ("in October", "before the end of the month", "next year") → clearly active
- "Maybe one day I'd like to...", "no rush", "always wanted to" with no timeframe → clearly someday

### 6. Clean Up

Delete or complete the original inbox task — it's now represented by the project and its first action.

## Rules

- One question at a time. Ask, wait, then act.
- Most projects should take 2–3 questions to set up. Skip questions when the answer is obvious from context.
- Don't create subtasks, sections, or a full project plan. Just the project and one first action. The user will build it out as they work.
- Look up projects and areas by name at runtime — never hardcode IDs.
- Keep it brisk. This is a 60-second setup, not a planning session.
