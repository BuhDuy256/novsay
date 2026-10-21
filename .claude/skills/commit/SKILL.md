---
name: commit
description: Analyze Git changes, decide whether to create one commit or several ordered commits, and create clear conventional commits when requested. Use for committing changes, planning commit phases, or drafting commit messages.
allowed-tools: Bash(git:*), Read, Grep, Edit
user-invocable: true
---

# Git Commit Skill

Create commits that are easy to understand, review, and revert.

## 1. Determine the requested action

Distinguish between:

- Analyze changes or propose commit phases: inspect and report only.
- Draft commit messages: provide messages without staging or committing.
- Commit changes: analyze, group, stage, verify, and commit.

An explicit request to commit authorizes multiple commits when justified.
Do not ask for confirmation for routine grouping within the requested scope.

A request for a commit message does not authorize creating a commit.
Never push unless explicitly requested.

## 2. Inspect the repository

Read applicable repository instructions.

Run these independent inspections in parallel:

- `git status --short --branch`
- `git diff --cached`
- `git diff`
- `git log --oneline -5`

List untracked files and read relevant contents before including them.
Git diff does not show untracked file contents.

Inspect surrounding code or documentation when the diff is insufficient.
Do not group changes from filenames or diff statistics alone.

Record existing staged changes before staging anything.
The index may contain an intentional partial selection.

If there are no changes, report that and stop.

## 3. Analyze the changes

Identify each distinct purpose:

- What problem does the change address?
- What behavior, contract, documentation, or workflow changes?
- Which edits must remain together?
- Which edits depend on another change?
- Which edits fall outside the requested scope?
- Does the change describe implemented behavior, a specification,
  or a proposal?

Do not describe a specification update as an implemented feature.

Flag apparent secrets, unresolved conflicts, and changes whose purpose
cannot be determined. Do not include them silently.

## 4. Decide whether to split

Prefer one commit when the changes serve one coherent purpose.

Consider separate commits when:

- Changes solve independent problems.
- A prerequisite can stand alone before its dependent change.
- A mechanical change can be separated from a behavior change.
- A change can reasonably be reviewed or reverted independently.

Keep together:

- An implementation change and its necessary regression tests.
- A contract change and the consumers needed to keep it working.
- Documentation changes and their generated artifacts.
- Specification edits that must land together to avoid contradictions.

Do not split merely by:

- File or folder.
- File extension.
- Frontend versus backend.
- Implementation versus tests.
- Number of changed lines.

Each commit must leave a coherent repository state.
Do not create intermediate commits with known broken references,
missing dependencies, or contradictory requirements.

Use the fewest commits that preserve distinct purposes.
Do not invent phases just to make the history look structured.

## 5. Build an ordered commit plan

Before staging, present a short plan.

For each proposed commit, identify:

1. Purpose.
2. Files or hunks included.
3. Dependencies on earlier commits.
4. Proposed commit message.
5. Relevant verification.

Order prerequisites before dependent changes.

For one commit, a short explanation is enough.
For several commits, use a compact numbered list or table.

If the user requested analysis or messages only, return the result
and stop. If committing is authorized, continue.

If a safe split requires rewriting working files or disturbing an
intentional partial staging selection, prefer a coherent combined
commit within the authorized scope. Explain the limitation.

## 6. Stage one commit at a time

Use explicit paths rather than blanket staging commands.

Before each commit:

1. Stage only the files or hunks assigned to that commit.
2. Inspect `git diff --cached`.
3. Run `git diff --cached --check`.
4. Confirm no unrelated changes are included.
5. Confirm all required changes are included.

When a file contains multiple purposes, use selective staging only
when the resulting staged snapshot can be inspected reliably.

Do not rewrite files merely to manufacture a commit split.
Do not unstage pre-existing selections without authorization.

Existing staged changes are evidence of user intent, but do not
automatically authorize unrelated changes to be committed.

If the requested subset cannot be committed without disturbing
unrelated staged changes, explain the concrete conflict and ask.

## 7. Write the commit message

Use this format:

    <type>[optional scope]: <short description>

    <optional body explaining purpose and important effects>

Types:

- `feat`: new implemented capability.
- `fix`: correction to implemented behavior.
- `refactor`: restructuring without intended behavior change.
- `docs`: documentation or specification changes.
- `style`: formatting without semantic changes.
- `test`: test changes.
- `chore`: maintenance, dependencies, or tooling.

Rules:

- Keep the subject under 72 characters.
- Use imperative wording.
- Match repository language and conventions where appropriate.
- Describe this commit's purpose, not all pending work.
- Add a body when it explains a reason or meaningful tradeoff.
- Do not include a file inventory.
- Do not add attribution trailers unless explicitly required.
- Do not claim tests passed without evidence.

## 8. Create and verify each commit

Create the commit using safely quoted arguments or a supported
multiline message mechanism.

Do not interpolate untrusted text into shell commands.

Perform checks appropriate to the change before committing when
the required tools and authorization are available.

Remember:

- `git diff --check` checks whitespace, not correctness.
- Checks against the working tree may include changes excluded
  from the staged snapshot.
- Do not claim a partial commit was tested independently unless
  its exact snapshot was checked.

After each commit:

- Inspect `git log -1 --format=fuller`.
- Inspect `git show --stat --oneline HEAD`.
- Inspect `git status --short`.
- Confirm the commit matches its planned purpose.

If a hook or commit command fails:

- Report the actual failure.
- Inspect the resulting repository state before retrying.
- Do not skip hooks or include unrelated hook edits silently.
- Do not create dependent commits while the failure is unresolved.

## 9. Report the result

For each created commit, report:

- Short hash and subject.
- One sentence describing its purpose.

Also report:

- Verification performed and material limits.
- Changes intentionally left uncommitted.
- Any requested commit that could not be completed.

Do not report success if the commit command failed.

## Safety

- Do not create or update CHANGELOG.md unless explicitly requested.
- Never use force, destructive cleanup, or history rewriting.
- Never amend unless explicitly requested.
- Never skip hooks unless explicitly requested.
- Never discard unrelated changes.
- Never commit secrets or unresolved merge conflicts.
- Never push without an explicit request.