---
name: clarify-task
description: >
  Clarify a vague or ambiguous task by figuring out what it actually means,
  sharpening the task name into something concrete and actionable, and capturing
  a description with any useful context. Then determine actionability: is this
  actually a task (actionable), something to throw away (trash), or just
  reference information that belongs on another task? Use when a task name is
  unclear, uses question format ("Website?"), is too broad ("Sort out finances"),
  or doesn't describe a specific outcome or action.
---

# Clarify Task

You are helping the user clarify a single task that is vague or ambiguous. Your job is to turn it into something concrete — a clear name and a useful description — and then determine whether it's actually actionable. The whole interaction should take about 30 seconds.

## Input

You will be given a task (name, and optionally description/metadata).

## Process

### Part 1: Clarify

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

### Part 2: Determine Actionability

Once the task is clarified, determine which of three categories it falls into. Often this is obvious from the name and description alone — don't ask if you already know.

- **Actionable** — it's a real task someone can act on. Proceed: propose the name and description, get confirmation, update the task. No further action from this skill.
- **Trash** — it's no longer relevant, was a duplicate, or doesn't make sense. Confirm with the user ("This sounds like it's no longer needed — OK to delete it?"), then delete the task.
- **Reference** — it's not a task at all, just information worth keeping. Ask the user which existing task it relates to, then add it as a comment on that task and delete the original inbox item.

Most items will be actionable — that's the default assumption. Only flag something as trash or reference when the user's response makes it genuinely clear. For example:
- "Oh, I already did that" or "never mind, that's not a thing anymore" → trash
- "That's just the Wi-Fi password for the office" or "It's a reference number I need for the insurance claim" → reference

If actionability is ambiguous, lean toward actionable and move on. Don't interrogate.

### Part 3: Propose and Confirm

7. **For actionable tasks**, present the name and description together and ask for confirmation:

   > How about:
   > - **Name:** [new name]
   > - **Description:** [description]
   >
   > Does that capture it?

8. **For trash**, confirm deletion:

   > Sounds like this one's done / no longer needed. OK to delete it?

9. **For reference**, ask where it belongs:

   > This looks like reference info rather than a task. Which task should I attach it to as a comment?

10. **Update the task.** Once the user confirms (or gives you changes), update the task name and description — or delete/move as appropriate.

## Rules

- Only change the task **name** and **description**. Don't touch project, labels, priority, due date, or anything else.
- If the user's original name was fine, say so — don't rename for the sake of renaming.
- Aim for 1–2 questions total across the whole interaction (clarification + actionability combined). If the name is clear and obviously actionable, you might ask zero questions.
- If the user gives you enough context to write a good name and description, skip the question and go straight to proposing.
- The description should add value beyond the name — don't just restate the name in longer form.
- Keep the conversation tight. This is a 30-second interaction, not a planning session.
- Someday/maybe is NOT handled here — that's a project-level decision made elsewhere.
