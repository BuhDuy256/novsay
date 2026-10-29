# Agents

## Project

Novsay converts web novel text into audio for listening. Product spec is in `docs/spec/`.
Vision: `docs/spec/01-product-vision/VIS-001.md`.

## Build workflow

All use case builds follow `WORKFLOW.md`. The phases are:

1. **Research** — answer technical unknowns, make decisions
2. **Testing plan** — map every AC to a test type and phase
3. **Implementation plan** — ordered steps tied to tests
4. **Implementation tickets** — flash-model-friendly GitHub Issues
5. **Execution and review** — implement, test, review, merge
6. **Verification** — full test suite, E2E, UC acceptance criteria

When the user requests a build, determine the scope first (full UC, specific steps,
specific alternatives, or individual FRs), then start Phase 1. When the user says
"continue" + a build name, read the flow tracker issue first.

## Skill routing

| Task | Skill |
|---|---|
| Write or rewrite a use case | `spec-authoring` |
| Generate UC sequence diagram | `use-case-sequence` |
| Generate research questions for a UC | `research-questions` |
| Generate a testing plan from FRs/ACs | `testing-plan` |
| Create GitHub Issues from a plan | `ticket-writer` |
| Update flow tracker issue | `flow-tracker-update` |
| Implement with TDD | `tdd` |
| Design module structure | `codebase-design` |
| Model domain concepts | `domain-modeling` |
| Diagnose a bug | `diagnosing-bugs` |
| Commit and push | `commit-push` |
| Review code | `open-code-review-delegate` |

## GitHub Issues conventions

- **One milestone per UC build:** named `UC-XXX`.
- **Labels:** `uc:XXX`, `phase:research`, `phase:test-stubs`, `phase:impl-plan`,
  `phase:impl`, `phase:post-impl`, `flow-tracker`, `flash-ready`.
- **Dependencies:** write `Blocked by #N, #N` in the issue body.
- **Flow tracker:** one per UC, created at Phase 1 start. Links to all tickets.

## Flash-model ticket rules

Tickets assigned to flash models (DeepSeek V4.1 Flash, GLM 5.3 Flash) must:

1. Have one concern per ticket — one function, one component, one module.
2. Include exact file paths — not "create a module" but `src/domain/source-validator.ts`.
3. Specify input/output contract — function signature, types.
4. Include a test command — `npm test -- --grep "FR-NNN"`.
5. Include a `Do NOT` section — explicit boundaries.
6. List `Blocked by` prerequisites.
7. Change at most 3 files.

## Decision authority

### Agent decides (no confirmation needed)

- File formatting and style within existing conventions
- Which existing research file to update
- Order of operations within a phase
- Git commit messages (following conventional commits)

### Agent proposes, user decides

- Technology choices (runtime, framework, library, provider)
- Architecture boundaries (module splits, package structure)
- Scope changes (adding or removing requirements)
- Closing a phase gate
- Any change to `docs/spec/`

## Key paths

| What | Where |
|---|---|
| Product spec | `docs/spec/` |
| Research | `docs/research/` |
| Decisions | `docs/decisions/` |
| Plans | `plans/` |
| Plan templates | `plans/_TEMPLATES/` |
| Issue templates | `.github/ISSUE_TEMPLATE/` |
| Coding conventions | `docs/development/` |
| Skills | `.agents/skills/` |
| Workflow reference | `WORKFLOW.md` |
