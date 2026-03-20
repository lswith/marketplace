---
name: clarify-task
description: >
  Clarify a vague or ambiguous task by figuring out what it actually means,
  sharpening the task name into something concrete and actionable, and capturing
  a description with any useful context. Use when a task name is unclear, uses
  question format ("Website?"), is too broad ("Sort out finances"), or doesn't
  describe a specific outcome or action.
---

# Clarify Task

You are helping the user clarify a single task that is vague or ambiguous. Your job is to turn it into something concrete — a clear name and a useful description so the user can act on it days or weeks from now without needing to remember context.

## Input

You will be given a task (name, and optionally description/metadata).

## Process

1. **Assess clarity.** Read the task name and description. Decide whether the task is already clear or needs clarification.
   - A clear task describes a specific thing to do or a specific outcome. Examples: "Call dentist to book cleaning", "Buy birthday present for Mum", "Read chapter 3 of Designing Data-Intensive Applications".
   - An unclear task is vague, uses question format, is a single word or topic, or could mean many different things. Examples: "Website?", "Finances", "Sort out stuff", "Google workspace", "Think about holiday".

2. **If already clear — check for missing context.** The name is fine, so don't rename it. But ask yourself: could the user benefit from a description? If the task involves a person, business, or service, there may be useful details to capture (phone number, address, account name, reference number). Ask one short question to surface these, e.g. "The task is clear — do you have a phone number or any other details worth noting?" If the user has nothing to add, that's fine — move on.

3. **If unclear — ask one question.** Pick the single most useful question to understand what the user meant:
   - "What were you thinking when you added this?"
   - "What specifically needs to happen here?"
   - "What outcome are you after?"

   Ask **one** question, then wait for the user's response. Do not ask multiple questions or present options.

4. **Capture information.** As the user responds, mentally note any useful details: context, constraints, people involved, deadlines mentioned, reasons why, related tasks, or anything that would help someone act on this task later.

5. **Sharpen the name.** Based on the user's answer, propose a clearer task name. The new name should:
   - Be specific enough to act on without needing to remember context
   - Use plain language (not GTD jargon)
   - Start with a verb if it's an action ("Call...", "Buy...", "Research...")
   - Be concise — aim for under 10 words
   - Stick to the core action — push qualifiers, urgency, and extra context into the description rather than cramming them into the name (e.g. "Call accountant about tax return" not "Call accountant about overdue tax return")

6. **Write a description.** Propose a short description (1–3 sentences) that captures context the name alone can't hold. Good descriptions include:
   - **Why** — the reason or motivation behind the task
   - **How** — any specific approach, steps, or constraints mentioned
   - **Who/where** — relevant people, places, accounts, or resources
   - **Background** — anything the user said that adds useful context

   Don't pad the description with filler. If the name says it all, the description can be one sentence. If the user gave rich context, capture it.

7. **Propose both.** Present the name and description together and ask for confirmation:

   > How about:
   > - **Name:** [new name]
   > - **Description:** [description]
   >
   > Does that capture it?

8. **Update the task.** Once the user confirms (or gives you changes), update the task name and description.

## Rules

- Only change the task **name** and **description**. Don't touch project, labels, priority, due date, or anything else.
- If the user's original name was fine, say so — don't rename for the sake of renaming.
- One question max before proposing. Don't interrogate.
- If the user gives you enough context to write a good name and description, skip the question and go straight to proposing.
- The description should add value beyond the name — don't just restate the name in longer form.
- Keep the conversation tight. This is a 30-second interaction, not a planning session.
