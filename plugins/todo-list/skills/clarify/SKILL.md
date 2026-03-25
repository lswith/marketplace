---
name: clarify
description: >
  Clarify a task that is genuinely vague — where the name and description don't
  give enough context to determine what the task actually is. Use ONLY when a
  task is a bare word or topic ("Website?", "Finances"), uses question format,
  or is so ambiguous that no reasonable person could act on it. Do NOT use when
  the task is merely imprecise but the intent is obvious.
argument-hint: <task name, description, and any metadata>
---

# Clarify

You are helping the user clarify a single task that is genuinely vague. Your job is to get the minimum human context needed, then produce a clear name and description and determine actionability. This should take about 20 seconds.

## Input

You will be given a task (name, and optionally description/metadata).

## Step 1: Decide Whether Clarification Is Needed

Read the task name and description. Ask yourself: **could a reasonable person figure out what to do with this?**

- **Skip clarification entirely** if the intent is obvious, even if the name is imprecise. "Sort out finances" is broad but clearly actionable — you know it's about finances. "Call dentist" is perfectly clear. "Buy present for Mum" needs no clarification. These tasks may benefit from sharpening later, but they don't need human input to understand.
- **Clarification is needed** only when you genuinely cannot determine what the task is about. Single words, bare topics, question-mark items, or things that could mean completely different things. Examples: "Website?", "Google workspace", "James", "That thing".

If clarification is not needed, say so and stop. Do not ask questions for the sake of asking questions.

## Step 2: Ask One Question

If you genuinely need clarification, ask **one** question. Pick the most useful:

- "What were you thinking when you added this?"
- "What specifically needs to happen here?"

Ask one question, then wait. Do not ask multiple questions, present options, or speculate about what the task might mean.

## Step 3: Determine Actionability

Once the user responds, determine which category the task falls into. This is usually obvious from their answer — don't ask if you already know.

- **Actionable** — it's a real task someone can act on. This is the default assumption.
- **Trash** — no longer relevant, already done, or doesn't make sense. Examples: "Oh, I already did that", "never mind".
- **Reference** — not a task, just information worth keeping. Examples: "That's just the Wi-Fi password for the office", "It's a reference number for the insurance claim".

If ambiguous, assume actionable and move on. Don't interrogate.

## Step 4: Propose and Confirm

**For actionable tasks**, sharpen the name and write a description based on what the user told you.

Name guidelines:
- Specific enough to act on without needing to remember context
- Plain language, starts with a verb ("Call...", "Buy...", "Research...")
- Under 10 words — push qualifiers and extra context into the description
- If the user's original name was already fine post-clarification, keep it

Description guidelines:
- 1-3 sentences capturing context the name can't hold: why, how, who, background
- Don't pad with filler — if the name says it all, one sentence is fine
- Don't restate the name in longer form

Present the proposal:

> How about:
> - **Name:** [new name]
> - **Description:** [description]
>
> Does that capture it?

**For trash**, confirm deletion:

> Sounds like this one's no longer needed. OK to delete it?

**For reference**, ask where it belongs:

> This looks like reference info rather than a task. Which task should I attach it to as a comment?

## Step 5: Update

Once the user confirms (or gives changes), update the task name and description — or delete/move as appropriate.

## Rules

- Only change the task **name** and **description**. Don't touch project, labels, priority, due date, or anything else.
- Aim for **0-1 questions** total. If the task is clear enough to work with, ask zero.
- Be decisive. Most tasks don't need this skill at all — it exists for the genuinely ambiguous ones.
- Keep the conversation tight. This is a 20-second interaction, not a planning session.
- Someday/maybe is NOT handled here — that's decided elsewhere.
