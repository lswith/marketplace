# todo-list Plugin

GTD-powered task management skills for Todoist.

## Structure

The skills assume a specific Todoist structure:

- **Areas** are top-level projects (e.g. Work, Personal, Finance). They are containers, not reviewed themselves.
- **Outcomes** live inside areas as either **sub-projects** (complex, many independent actions) or **parent tasks with sub-tasks** (lightweight, 2-5 sequential steps). Parent task is the default — only use sub-projects for genuinely complex efforts.
- **Single actions** go directly into their area project. There is no catch-all project.
- **Someday/maybe** is a label (`@someday`), not a project or area. Items stay in their natural area with the label applied.

## Skills

Five skills organized by decision type:

| Skill | Question | Decision by |
|-------|----------|-------------|
| **clarify** | "What is this?" | Human — get context for vague items |
| **organize** | "Where does this go and what form should it take?" | Claude — container type, area routing, restructuring |
| **prioritize** | "How important/urgent is this?" | Human — the key judgment call |
| **enrich** | "What metadata does this need?" | Claude — labels, due dates, deadlines, waiting-for |
| **triage** | "Does this need attention?" | Claude — lightweight health check, flags issues |

Skills that say "Claude" are opinionated — they make calls without asking unless genuinely ambiguous. Skills that say "Human" exist because human judgment is essential for that decision.

## Commands

| Command | Purpose |
|---------|---------|
| **process-inbox** | Work through inbox one task at a time: clarify (if needed) -> organize -> prioritize -> enrich |
| **backlog-review** | Triage outcomes, tasks, and someday items. Load heavier skills only when issues are flagged. |
| **plan-day** | Pull from backlog based on priorities, dates, and context. Quick 2-3 minute exercise. |
| **setup-gtd** | One-time GTD infrastructure bootstrap. |

## Labels

Two label types:
- **Workflow labels**: `next`, `waiting`, `someday` — control task state
- **Context labels**: `desk`, `calls`, `home`, `errands` — indicate where/how work happens

Every `next` task gets exactly one context label. Context filters in the sidebar (e.g. `@next & @desk`) let the user pick work by location/mode and work top-down by priority — this reduces decision fatigue.

## Due Date Strategy

Due dates are a scheduling layer driven by priority:
- **P1** — always gets a due date (specific day)
- **P2** — usually gets a due date (target day this week or next)
- **P3** — rarely dated (lives in context lists)
- **P4** — never dated (backlog)

Due dates are scheduling intentions ("I plan to work on this that day"), not hard constraints. Hard constraints use the deadline field. The `prioritize` skill handles priority; the `enrich` skill applies due dates based on the priority set.
