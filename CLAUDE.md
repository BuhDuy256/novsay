# Claude Code adapter

@AGENTS.md
@WORKFLOW.md

## Known mistakes — do NOT repeat

### Glob patterns must match depth

**Wrong:** `.agents/skills/*` — only matches files directly in the folder, misses
all subdirectories.
**Right:** `.agents/skills/**/*` — matches files at any depth.

When listing skills, files in nested directories, or any tree structure, always use
`**/*` to recurse. A single `*` only matches one level.

### Skills exist — use them

All skills listed in AGENTS.md are installed at `.agents/skills/<name>/SKILL.md`.
Before saying "skill not found", glob with `**/*` or check `.agents/skill-manifest.json`.
When the user says `/commit-push` or any skill name, invoke it via the Skill tool — do
not fall back to manual steps.

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
