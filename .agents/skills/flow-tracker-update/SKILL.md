---
name: flow-tracker-update
description: Update the flow tracker issue for a UC. Reads current issue statuses from GitHub and updates the tracker's phase checklists. Used after any ticket closes.
---

# Flow tracker update

Update the flow tracker issue to reflect current ticket statuses.

## Input

- The UC identifier (e.g., UC-001).
- The flow tracker issue number.

## Process

### 1. Get current ticket statuses

```bash
gh issue list --milestone "UC-XXX" --state all --json number,title,state,labels
```

### 2. Group by phase

Using the `phase:*` labels, group tickets into their phases.

### 3. Update the flow tracker issue

For each ticket:
- `[x]` if the issue state is `closed`
- `[ ]` if the issue state is `open`

```bash
gh issue edit TRACKER_NUMBER --body "..."
```

### 4. Check phase gates

- **Phase 1 gate:** all `phase:research` tickets closed → note "Phase 1 complete"
- **Phase 2 gate:** all `phase:test-stubs` tickets closed → note "Phase 2 complete"
- **Phase 3 gate:** implementation plan ticket closed → note "Phase 3 complete"
- **Phase 4 gate:** all `phase:impl` tickets closed → note "Phase 4 complete"
- **Phase 5 gate:** all `phase:post-impl` tickets closed → note "Phase 5 complete"

### 5. Update the local mirror

Update `plans/UC-XXX/flow-tracker.md` to match the GitHub issue.

## Rules

- Do not close tickets — only update the tracker display.
- Do not change ticket labels or assignments.
- Report the current phase and any blocked tickets in the output.
