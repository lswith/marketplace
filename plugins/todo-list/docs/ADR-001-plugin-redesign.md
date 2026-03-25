# ADR-001: Todo-List Plugin Redesign

**Status:** Proposed
**Date:** 2026-03-25
**Deciders:** Luke

## Context

The todo-list plugin currently has 10 skills and 3 commands implementing a GTD workflow for Todoist. After real-world usage, several structural problems have emerged:

1. **Skill boundaries don't match decision flow.** Clarify, route, set-priority, and enrich run sequentially on the same task during inbox processing, but they're separate skills with awkward handoffs. Meanwhile, the same "is this well-defined?" judgment is needed during both creation and review, but uses different skills for each.

2. **Clarification is a human bottleneck, not a Claude task.** Claude can't meaningfully clarify a vague task like "Website?" without human context. Once the human provides context, Claude is good at routing (single action vs parent task vs project) and enriching metadata. The current design treats clarification as a Claude-driven skill when it's fundamentally a human-input moment.

3. **Priority and next-action decisions need human judgment.** These are the two moments where human input matters most, but they're buried in a sequence of skill loads rather than being elevated as the key decision points.

4. **Weekly review is exhausting and misnamed.** It's structured as a comprehensive GTD "reflect" phase with 4 phases and granular per-item review. In practice, it should be a **backlog review** — checking if priorities have shifted and whether items should move in/out of someday. The current design loses momentum.

5. **No "plan my day" workflow.** There's no way to pull work from the backlog based on current priorities and dates. The system organizes but doesn't help with daily execution.

6. **Skills don't compose well.** The command orchestration (loading skills one-by-one via the Skill tool) feels mechanical. Skills are self-contained by design, but this means each skill re-reads context and re-asks questions that a unified flow would handle once.

## Decision

Redesign the plugin around two principles:

- **Organize skills by decision type** (human-input vs Claude-judgment), not by GTD phase
- **Unify creation and review** — the same skill that ensures a task is well-defined during inbox processing should also check it during backlog review

## Options Considered

### Option A: Unified Skills (fewer, dual-purpose)

Collapse 10 skills into 5 that work for both creation and review contexts:

| New Skill | Replaces | Question it answers | Decision by | Purpose |
|-----------|----------|-------------------|-------------|---------|
| **clarify** | clarify-task | "What is this?" | Human | Get context for vague items. Only triggers when Claude genuinely can't determine intent from the task name/description. |
| **organize** | route-task, setup-outcome, restructure-outcome | "Where does this go and what form should it take?" | Claude | Given a clear task, determine if it's a single action, parent task, or project. Set up the right container. Route to the correct area. Works for new tasks AND existing items that have changed scope. |
| **prioritize** | set-priority | "How important/urgent is this?" | Human | Assess urgency/importance, assign priority, connect to scheduling. Codifies a clearer decision framework for the key human judgment call. |
| **enrich** | enrich-task | "What metadata does this need?" | Claude | Apply metadata (context labels, due dates, deadlines, waiting-for). Runs after human decisions are made. |
| **triage** | review-outcome, review-task, review-someday-maybe, review-project-relationships | "Does this need attention?" | Claude | Quick health check on any item type: stale? complete? priority shifted? should move in/out of someday? Flags issues, then the command delegates to organize/prioritize as needed. |

Commands become:

| Command | Replaces | Purpose |
|---------|----------|---------|
| **process-inbox** | process-inbox | Streamlined: clarify (if needed) -> organize -> prioritize -> enrich. Fewer skill loads, faster per-task. |
| **backlog-review** | weekly-review | Renamed and refocused: have priorities shifted? Should anything move in/out of someday? Are outcomes still healthy? Uses triage skill, delegates to organize/prioritize when issues found. |
| **plan-day** | (new) | Pull from backlog: look at today's dates, priorities, and context to suggest what to work on. |
| **setup-gtd** | setup-gtd | Unchanged — one-time bootstrap. |

| Dimension | Assessment |
|-----------|------------|
| Complexity | **Low** — fewer moving parts, clearer boundaries |
| Skill reuse | **High** — organize works in both creation and review contexts |
| Human decision points | **Clear** — clarify and prioritize are the two human moments; organize, enrich, and triage are Claude-driven |
| Migration effort | **Medium** — rewrite 10 skills into 5, update 3 commands |
| Eval coverage | **Medium** — existing evals need remapping but test scenarios are reusable |

**Pros:**
- Skills match actual decision flow — fewer awkward handoffs
- organize validates structure during both creation and review (no divergence)
- Clearer contract: "human decides X, Claude decides Y"
- Backlog review is lighter and more focused
- Plan-day fills a real gap in the workflow

**Cons:**
- Larger individual skills (more logic per skill)
- organize skill has broad scope (routing + container setup + restructuring)
- Existing evals need significant rework

### Option B: Micro-skills with smarter orchestration

Keep skills small but fix the orchestration layer. Instead of loading skills one-by-one, commands define decision trees that skip unnecessary skills and batch questions.

| Dimension | Assessment |
|-----------|------------|
| Complexity | **High** — orchestration logic moves into commands, which become complex |
| Skill reuse | **Low** — skills stay single-purpose, reuse happens at command level |
| Human decision points | **Unclear** — still spread across many skills |
| Migration effort | **Low** — skills stay mostly the same, commands get rewritten |
| Eval coverage | **High** — existing evals stay valid |

**Pros:**
- Minimal changes to existing skills
- Evals remain valid
- Each skill stays focused and testable

**Cons:**
- Doesn't fix the fundamental boundary problem — review and creation still use different skills
- Commands become very complex orchestrators
- Doesn't address the "clarify is a human moment" insight
- Still 10+ skills to maintain

### Option C: Workflow-first (derive skills from commands)

Start from the three workflows (inbox, backlog review, plan day) and extract only the skills those workflows need. Bottom-up design.

| Dimension | Assessment |
|-----------|------------|
| Complexity | **Medium** — driven by workflow needs, but may over-fit to current commands |
| Skill reuse | **Variable** — depends on what the workflows surface |
| Human decision points | **Unclear** — emerges from workflow analysis rather than being designed explicitly |
| Migration effort | **High** — full redesign from scratch |
| Eval coverage | **Low** — all new skills need new evals |

**Pros:**
- Skills are guaranteed to be useful (no orphans)
- Workflows drive the design, not abstract principles

**Cons:**
- Risk of over-fitting to current workflows — new commands may need skills that don't exist
- Doesn't start from the key insight about human vs Claude decisions
- Full rewrite with no reuse of existing work

## Trade-off Analysis

The core tension is **skill granularity vs. composability**.

Option B preserves granularity but doesn't fix the real problem: the skill boundaries are wrong, not the orchestration. Option C is a clean-slate approach but throws away the insight that skills should be organized by decision type.

**Option A is the strongest fit** because it directly addresses the two main problems:
1. Skills that work for both creation and review (organize works in both contexts)
2. Clear separation of human-input moments (clarify, prioritize) from Claude-driven automation (organize, enrich, triage)

The risk with Option A is that organize becomes a "god skill" — routing, container setup, and restructuring in one. This can be mitigated by keeping organize focused on a single question: "where does this go and what form should it take?" The container creation is mechanical once the decision is made. Triage stays lightweight — it's a quick status check that flags issues for other skills to handle, not a decision-maker itself.

## Consequences

- **Easier:** Inbox processing is faster (fewer skill loads, fewer questions). Backlog review is lighter and more focused. Daily planning becomes possible.
- **Harder:** Individual skills are larger and need more comprehensive evals. The organize skill needs careful scoping to avoid becoming a catch-all.
- **Revisit:** After implementation, evaluate whether organize should be split back into route + restructure if it proves too broad. Monitor whether plan-day needs its own skills or can work purely as a command.

## Action Items

1. [ ] Review and accept/modify this ADR
2. [ ] Design the 5 new skill interfaces (inputs, outputs, decision points)
3. [ ] Migrate clarify-task evals to new clarify skill
4. [ ] Build organize skill (merge route-task + setup-outcome + restructure-outcome)
5. [ ] Build prioritize skill (evolve set-priority with clearer decision framework)
6. [ ] Build triage skill (merge review-outcome + review-task + review-someday-maybe + review-project-relationships)
7. [ ] Simplify enrich skill
8. [ ] Rewrite process-inbox command for new skill flow
9. [ ] Create backlog-review command (replace weekly-review)
10. [ ] Create plan-day command
11. [ ] Update setup-gtd if needed
12. [ ] Run evals against new skills and benchmark vs old
