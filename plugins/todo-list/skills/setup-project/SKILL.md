---
name: setup-project
description: >
  Create or merge a Todoist project for a multi-step task. Assign an area,
  define the first next action, and decide whether it's active or someday/maybe.
  Use when route-task identifies something as a project — this skill handles
  the full project setup.
---

# Setup Project

You are helping the user turn a multi-step task into a proper Todoist project. The task has already been clarified and identified as a project by route-task. Your job is to create the project, slot it into the right area, and define a concrete first action.

## Input

A single task (name, description) that has been identified as requiring multiple steps.

## Process

### 1. Check for Existing Projects

Before creating anything, check if a related project already exists.

- Search the user's projects for anything that overlaps with this task.
- If a **close match** exists (e.g. task is "Set up home office" and there's already a "Home Office" project), ask: "You already have a **[project name]** project — should this go there, or is it a separate thing?"
- If the user says **merge** → move the task into the existing project as a next action. Skip to step 4.
- If **no match** or the user says it's separate → continue to step 2.

### 2. Create the Project

Create a new project with a clear, noun-phrase name.

- Project names should describe the outcome or area, not the action. For example:
  - Task: "Plan holiday to Japan" → Project: "Japan Holiday"
  - Task: "Set up new accounting system" → Project: "Accounting System Setup"
  - Task: "Renovate the bathroom" → Project: "Bathroom Renovation"
- Propose the name and let the user confirm or adjust.

### 3. Assign an Area

Every project needs a parent area (a top-level project used as a folder). Ask the user where it belongs.

1. Fetch the user's existing top-level projects (areas).
2. Suggest the most likely area based on the project's nature: "This feels like it belongs under **[area]** — sound right?"
3. If the user disagrees, let them pick from the list or create a new area.

**Someday/maybe handling:** If the user isn't ready to work on this yet, or explicitly says it's a "someday" thing:
- Place the project under a "Someday / Maybe" area (create it if it doesn't exist).
- Don't ask about priority, due dates, or first actions — just park it.
- Confirm: "Parked under Someday / Maybe. It'll come up in your next review."
- Stop here — skip steps 4 and 5.

### 4. Define the First Action

Every active project needs at least one concrete next action.

- Ask: "What's the very first thing you'd need to do to move this forward?"
- If the user gives a clear action, create it as a task in the new project.
- If the user is unsure, suggest something based on the project's nature:
  - Research projects → "Research [topic] — find 2-3 options"
  - Setup projects → "List what's needed for [project]"
  - Planning projects → "Draft rough plan for [project]"
- The first action should follow the same naming rules as clarify-task: verb-led, specific, under 10 words.

### 5. Enrich the First Action

Run the `enrich-task` skill on the first action to add priority, labels, and due date.

## Output

By the end, the user has:
- A named project in the right area (or a task merged into an existing project)
- A concrete first action (with metadata), unless it's someday/maybe
- The original inbox task deleted or converted

## Rules

- Always check for existing projects before creating new ones. Duplicate projects are a GTD anti-pattern.
- Project names are noun phrases, not action phrases. "Japan Holiday" not "Plan holiday to Japan".
- Every active project must have at least one next action. No empty projects.
- Someday/maybe projects get parked with no actions, priority, or dates.
- Look up areas and projects by name at runtime — never hardcode IDs.
- This skill references `enrich-task` by name but does not inline its logic.
- Keep it conversational but efficient. This is a 1-minute interaction.
