---
name: ticket-writer
description: Create GitHub Issues from a plan document (research checklist, testing plan, or implementation plan). Uses the issue templates in .github/ISSUE_TEMPLATE/. Sets labels, milestones, and blocked-by references.
---

# Ticket writer

Create GitHub Issues from a plan document.

## Input

One of:
- `plans/UC-XXX/research-checklist.md` → creates research tickets
- `plans/UC-XXX/testing-plan.md` → creates test stub tickets
- `plans/UC-XXX/implementation-plan.md` → creates implementation and post-impl tickets

Also needs:
- The flow tracker issue number for the UC.
- The UC identifier (e.g., UC-001) for labels and milestone.

## Process

### 1. Read the plan document

Extract each item that needs a ticket: questions, test stubs, implementation steps,
or post-impl tests.

### 2. Create issues using `gh`

Use the GitHub CLI to create issues. For each item:

```bash
gh issue create \
  --title "Phase: description" \
  --label "phase:xxx,uc:XXX" \
  --milestone "UC-XXX" \
  --body "..."
```

The body follows the matching template in `.github/ISSUE_TEMPLATE/`:
- Research questions → `research-ticket.md` (includes a Mermaid sequence diagram
  showing the UC flow with the relevant step highlighted)
- Test stubs → `test-stub-ticket.md`
- Implementation steps → `implementation-ticket.md`
- Post-impl tests → `post-impl-test-ticket.md`

For **research tickets**, the flow diagram is generated from the flow model in the
research checklist. The same base diagram is reused across related questions — only
the highlighted `rect` moves to the step each question comes from.

### 3. Set dependencies

Add `Blocked by #N, #N` in the issue body, referencing:
- Research tickets blocked by other research tickets
- Test stub tickets blocked by research decisions
- Implementation tickets blocked by test stubs and other implementation tickets
- Post-impl test tickets blocked by implementation tickets

### 4. Update the flow tracker

Add each created issue to the flow tracker issue body under the correct phase.

### 5. Update the local mirror

Update `plans/UC-XXX/flow-tracker.md` with the new ticket numbers.
Update the source plan document's ticket column with issue numbers.

## Flash-model ticket rules

Implementation tickets must follow these rules (from WORKFLOW.md):

1. One concern per ticket.
2. Exact file paths.
3. Input/output contract with types.
4. Test command as acceptance criteria.
5. Do NOT section with explicit boundaries.
6. Blocked by prerequisites.
7. Maximum 3 files changed.

## Linking convention

All cross-references must be clickable Markdown links (see WORKFLOW.md "Linking
convention"). At the start, derive the repo base URL:

```bash
git remote get-url origin
# https://github.com/{owner}/{repo}.git → base = https://github.com/{owner}/{repo}
```

Apply to every output:

- **Issue bodies — Deliverable section:** use
  `[docs/research/topic.md]({base}/blob/main/docs/research/topic.md)`.
- **Local plan files** (checklist, flow tracker): update Ticket column and `#N`
  references to `[#N]({base}/issues/N)`.
- Issue-to-issue references (`Blocked by #N`) stay as `#N` in issue bodies because
  GitHub auto-links them. Only local `.md` files need full links.

## Rules

- Create the milestone first if it does not exist: `gh api ... -f title="UC-XXX"`.
- Create labels first if they do not exist.
- Always reference the flow tracker issue in every ticket body.
- Number tickets in dependency order so that blocked-by references point to
  lower-numbered issues.
