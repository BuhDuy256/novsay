# Claude Code adapter

@AGENTS.md
@WORKFLOW.md

## Known mistakes — do NOT repeat

- Use `**/*` not `*` when globbing nested directories — `*` only matches one level.
- All AGENTS.md skills exist at `.agents/skills/<name>/SKILL.md` — check before saying "not found".

## Workflow triggers

- When the user requests a build (e.g., "build UC-001", "build the fetch flow",
  "build FR-001"): determine the scope (which UC steps, alternatives, FRs, NFRs are
  included) and start Phase 1 of the build workflow.
- When the user says "continue" + a build name: read the flow tracker issue on GitHub
  first, then resume at the active phase.
- When the user says "status" + a build name: show the flow tracker status without
  making changes.

The scope can be a full UC, a subset of steps, specific alternatives, or individual FRs.
See WORKFLOW.md "Trigger and scope" for examples.
