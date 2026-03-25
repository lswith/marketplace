---
name: enrich
description: >
  Apply metadata to a task — context labels, deadlines, due dates, and
  waiting-for status. Runs after priority has already been decided. Be
  opinionated: apply obvious metadata without asking, and only confirm
  when genuinely ambiguous.
argument-hint: <task name or ID>
---

# Enrich

You are applying metadata to a single task. Priority has already been set — your job is context labels, deadlines, due dates, and waiting-for status.

## Input

A task with a name, description, priority, and possibly some existing metadata (project, labels, due date).

## Process

1. **Read the task.** Look at the name, description, project, and existing metadata. Decide what's missing or wrong.

2. **Fetch existing labels.** Before applying any labels, fetch the user's existing labels. Never invent new labels — only use ones that already exist.

3. **Apply metadata.** Be opinionated. If the answer is obvious from the task content, just apply it — don't ask.

   | Attribute | When to apply |
   |-----------|---------------|
   | **Context label** | Every `next` task needs exactly one context label (e.g. `desk`, `calls`, `home`, `errands`). Apply silently when obvious. Only ask if genuinely ambiguous. Never invent new labels. |
   | **Deadline** | Only for hard external constraints — tax filing dates, event dates, submission cutoffs, application closing dates. Not for self-imposed targets. Only works on one-time tasks (not recurring). A countdown appears within 7 days, which surfaces urgency naturally. |
   | **Due date** | A scheduling intention ("I plan to work on this that day"), not a hard constraint. Driven by the task's priority: P1 = always set a specific day. P2 = usually set a target day this week or next. P3 = rarely — lives in context lists. P4 = never. Don't invent due dates that the priority level doesn't call for. |
   | **Waiting-for** | If the task is blocked by another person, task, or event. Apply the `waiting` label, note the blocker in the description, and if possible find and link the blocking task or person via a comment. |

4. **Handle someday tasks differently.** If the task has a `someday` label:
   - Skip due dates — they don't apply.
   - Still set a deadline if there's a hard external constraint (e.g. application closing date). The countdown prevents the window from closing unnoticed if the task is later activated.
   - Context labels are fine if obvious.
   - Make sure the name and description are solid — these tasks get revisited weeks or months later and need to stand on their own.

5. **Strip stale labels.** Remove generic labels that don't serve a filtering or workflow purpose — leftover import tags, vague categories nobody filters by. Only keep labels that map to a real workflow context.

6. **Propose changes.** Present all proposed metadata changes together in one summary:

   > Here's what I'd add:
   > - **Label:** @desk
   > - **Deadline:** March 31 (grant submission cutoff)
   >
   > Sound good?

   Only include attributes you're actually changing. Don't list attributes you're leaving alone. If you already applied obvious metadata silently (e.g. a context label), mention what you applied so the user can correct it if needed.

7. **Apply.** Once confirmed (or adjusted), apply all changes in one go.

## Rules

- Don't touch the task name or description unless noting a blocker for waiting-for.
- Be opinionated — apply obvious metadata without asking. Only confirm when genuinely ambiguous.
- One confirmation round max. Propose everything together, get a yes/no, apply.
- Every `next` task must end up with exactly one context label.
- Never invent labels. Only use the user's existing labels.
- If the task already has all the metadata it needs, say so and move on.
- Keep it tight. This is a quick metadata pass, not a planning session.
