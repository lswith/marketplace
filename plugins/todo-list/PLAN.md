# Todo-List Plugin — Skill Roadmap

## Goal

A composable GTD inbox-processing pipeline for Todoist. Each skill handles one step; `process-inbox` orchestrates them.

## Skills

### Existing (needs update)

| Skill | Purpose |
|-------|---------|
| **clarify-task** | Sharpen name + description, check actionability (actionable / trash / reference) |

### To Build (in order)

| Skill | Purpose |
|-------|---------|
| **route-task** | GTD decision tree: 2-min skip, project check, or defer to One-Off Tasks |
| **setup-project** | Create/merge Todoist project, assign area, first action, priority vs someday |
| **enrich-task** | Add priority, labels, due dates, waiting-for detection |
| **process-inbox** | Orchestrator: one task at a time through clarify → route → enrich |

### Future (not in scope)

- **allocate-work** — assign next actions to specific days
- **review-backlog** — prune/merge stale projects and tasks

## Key Decisions

- `triage-task` deleted — actionability check folded into `clarify-task`, routing into `route-task`
- Someday/maybe is a project-level decision in `setup-project` — someday projects go under a "Someday/Maybe" area
- Waiting-for lives in `enrich-task` — checks if something blocks the task
- 2-minute tasks get skipped (left in inbox for user to do)
- Reference items get added as comments on related tasks, then deleted
- `enrich-task` is standalone — other skills call it rather than inlining enrichment
- Skills describe behaviour, not MCP tool names
