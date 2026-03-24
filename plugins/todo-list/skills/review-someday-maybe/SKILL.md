---
name: review-someday-maybe
description: >
  Review a single someday/maybe item. Decide if it should be activated,
  kept as someday, or deleted. Use during a weekly review to keep the
  someday list fresh and motivating.
---

# Review Someday/Maybe

You are helping the user review a single someday/maybe item as part of a weekly review. Your job is to quickly check whether the item is still interesting, whether it's time to activate it, or whether it should be removed. This should feel like browsing a wish list, not an interrogation.

## Input

You will be given a task, parent task, or project that has a `someday` label. It will include name, description, and any metadata.

## Process

### 1. Interest Check

Is this item still something the user cares about?

- If the item clearly still has value (a reasonable aspiration, a real want, something that could plausibly be activated later), skip to the activation check.
- If the item sounds **outdated, irrelevant, or superseded** (e.g. references an old job, a passed opportunity, or something the user has already done differently), ask: "Still interested in this, or ready to let it go?"

### 2. Activation Check

Is now the right time to make this active?

- If the item has a clear trigger or reason to activate now (e.g. circumstances have changed, a dependency was resolved, the user has capacity), ask: "Ready to make this active?"
  - **For projects or parent tasks**: remove the `someday` label. The item stays in its current area. If it has no active next action, prompt for one.
  - **For single tasks**: remove the `someday` label, add the `next` label. The task stays in its current area/project.
- If there's no obvious reason to activate, leave it on the someday list and move on. Don't ask unless there's a reason to think now is the right time.

### 3. Sanity Check

Will this item still make sense months from now?

- If the name or description is **vague enough that the user won't remember what it means** when they next review it (e.g. "App idea" with no description, or a project name that's just a person's name), suggest a quick clarification: "This might not make sense in a few months — want to add a note about what you had in mind?"
- If the name and description are self-explanatory, skip this.

## Rules

- This is the fastest skill. Most items take one question or zero.
- Don't enrich activated items — the command handles that after activation.
- Don't narrate your process. Just ask the relevant question or say "Still on the list" and move on.
- Keep it light. The someday list is a holding pen for ideas, not a commitment — treat items accordingly.
