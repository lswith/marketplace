---
name: review-project-relationships
description: >
  Analyse relationships between active projects during a weekly review. Identify
  overlaps, dependencies, projects that could be merged, and projects that may
  no longer need to exist given another project's progress. Runs once per review,
  after individual project reviews are complete.
---

# Review Project Relationships

You are helping the user see how their active projects relate to each other. Individual project health has already been checked — this step zooms out to look at the full landscape.

## Input

You will be given the full list of active projects (name, area, task list). Someday/Maybe projects are excluded unless they share obvious overlap with an active project.

## Process

Work through these checks in order. Only surface findings that are genuinely useful — most project pairs have no meaningful relationship.

### 1. Overlap Detection

Look for projects that share the same domain, goal, or deliverable. Common patterns:

- **Duplicate scope**: Two projects that would both be "done" when the same thing happens (e.g. "Set up shared finances with Zoe" and "Update YNAB to new shared account structure" — one is a subset of the other).
- **Shared tasks**: Projects where the next actions could reasonably live in either project.
- **Same domain, different angles**: Projects in the same space that might benefit from being consolidated (e.g. multiple consulting setup projects that are really phases of one larger effort).

For each overlap found, present it simply:

> **Overlap:** [Project A] and [Project B]
> [One sentence explaining the relationship — e.g. "Both are about setting up consulting infrastructure. B looks like a subset of A."]
> Options: Merge into one project / Keep separate / Note the dependency and move on

Wait for the user's response before continuing.

### 2. Dependency Detection

Look for projects where one blocks or feeds into another:

- **Sequential**: Project A needs to finish before Project B can start (e.g. "Consulting finances set up" before "Employ Zoe in the Pty Ltd").
- **Shared prerequisite**: Multiple projects depend on the same thing being done first.
- **Output becomes input**: One project's deliverable is another project's starting material.

For each dependency found:

> **Dependency:** [Project A] → [Project B]
> [One sentence — e.g. "The shared account structure needs to be set up before YNAB can be updated to reflect it."]
> Options: Add a blocking note / Reorder priorities / Already aware, skip

### 3. Redundancy Check

Look for projects that may no longer need to exist:

- **Absorbed**: The project's goal is now covered by another project that has grown in scope.
- **Achieved by side-effect**: Another project's progress has already accomplished what this project set out to do.
- **Superseded**: Circumstances have changed and a different project now addresses the same need.

For each potential redundancy:

> **Possibly redundant:** [Project]
> [One sentence — e.g. "This looks like it's been absorbed into [Other Project]. Still needed separately?"]
> Options: Complete it / Merge into [Other Project] / Keep it

### 4. Cluster Summary

If there are natural groupings of related projects (e.g. "consulting launch" cluster, "household finances" cluster), briefly name them. This helps the user see the big picture.

> **Project clusters I noticed:**
> - **Consulting launch**: [list of related projects]
> - **Household finances**: [list of related projects]
> - [etc.]

Only show clusters with 3+ projects. Don't force groupings that aren't there.

## Rules

- **One finding at a time.** Present one overlap, dependency, or redundancy, wait for the user's response, then continue. Don't dump everything at once.
- **Skip the obvious.** Don't flag relationships the user clearly already knows about and has intentionally structured (e.g. sub-projects under an area).
- **Don't reorganise unprompted.** Present findings and options. Let the user decide. Don't move projects around without confirmation.
- **Be concrete.** Reference specific project names and tasks when explaining relationships. Vague observations ("these seem related") aren't helpful.
- **Quick when clean.** If there are no meaningful overlaps, dependencies, or redundancies, say "No significant overlaps or dependencies — your projects look well-separated" and move on. Don't manufacture findings.
- **Cluster summary is informational only.** Don't ask questions about clusters — just present them as context for the user to reflect on.
