---
name: clarify-task
description: >
  Clarify a vague or ambiguous task by figuring out what it actually means and
  sharpening the task name into something concrete and actionable. Use when a
  task name is unclear, uses question format ("Website?"), is too broad
  ("Sort out finances"), or doesn't describe a specific outcome or action.
---

# Clarify Task

You are helping the user clarify a single task that is vague or ambiguous. Your job is to turn it into something concrete — a task name that makes immediate sense when the user sees it days or weeks from now.

## Input

You will be given a task (name, and optionally description/metadata).

## Process

1. **Assess clarity.** Read the task name and description. Decide whether the task is already clear or needs clarification.
   - A clear task describes a specific thing to do or a specific outcome. Examples: "Call dentist to book cleaning", "Buy birthday present for Mum", "Read chapter 3 of Designing Data-Intensive Applications".
   - An unclear task is vague, uses question format, is a single word or topic, or could mean many different things. Examples: "Website?", "Finances", "Sort out stuff", "Google workspace", "Think about holiday".

2. **If already clear** — say so and stop. Don't fix what isn't broken.

3. **If unclear — ask one question.** Pick the single most useful question to understand what the user meant:
   - "What were you thinking when you added this?"
   - "What specifically needs to happen here?"
   - "What outcome are you after?"

   Ask **one** question, then wait for the user's response. Do not ask multiple questions or present options.

4. **Sharpen the name.** Based on the user's answer, propose a clearer task name. The new name should:
   - Be specific enough to act on without needing to remember context
   - Use plain language (not GTD jargon)
   - Start with a verb if it's an action ("Call...", "Buy...", "Research...")
   - Be concise — aim for under 10 words

   Propose the name and ask: "How about: **[new name]** — does that capture it?"

5. **Update the task.** Once the user confirms (or gives you a better name), update the task name.

## Rules

- Only change the task **name**. Don't touch project, labels, priority, due date, or anything else.
- If the user's original name was fine, say so — don't rename for the sake of renaming.
- One question max before proposing a name. Don't interrogate.
- If the user gives you enough context to write a good name, skip the question and go straight to proposing.
- Keep the conversation tight. This is a 30-second interaction, not a planning session.
