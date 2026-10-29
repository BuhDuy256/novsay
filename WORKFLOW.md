# Build workflow

Reference for building use cases from spec to working code. Every session that starts
a UC build reads this document.

## Trigger and scope

The workflow starts when the user requests a build. The scope is flexible:

| User says | Scope |
|---|---|
| "Build UC-001" | Full UC — all steps and alternatives |
| "Build the fetch flow from UC-001" | Steps S1-S2, alternatives A1-A3 |
| "Build just the link validation" | FR-001 only |
| "Build the error handling for fetch failure" | Alternative A3 only |
| "Build UC-001 S1-S3 without save" | Steps S1-S3, skip S6 and save-related alternatives |

The first action is always Phase 1, never jumping to implementation. The scope
determines which FRs/NFRs are included in research, testing, and implementation.

### Scope definition

Every build starts by defining its scope in the plan folder:

- **Folder name:** `plans/UC-XXX-short-label/` (e.g., `plans/UC-001-fetch-flow/`)
- **Scope fields** (in every plan template):
  - Use case: UC-XXX
  - Steps included: S1-S2 (or "all")
  - Alternatives included: A1, A3 (or "all")
  - FRs in scope: FR-001, FR-002
  - NFRs in scope: NFR-001

A full UC build uses `plans/UC-XXX/` with "all" for steps and alternatives.

### Multiple builds for the same UC

Different scopes of the same UC coexist:
- `plans/UC-001-fetch-flow/` — S1-S2
- `plans/UC-001-save-flow/` — S6 + A8, A11
- `plans/UC-001-audio-prep/` — S4-S5 + A6

Each has its own flow tracker issue and its own tickets.

## Resuming

When the user says "continue UC-XXX" (or a scoped build name), read the flow
tracker issue on GitHub first. It shows which phase is active and which tickets
are open.

## Phases

### Phase 1 — Research

**Goal:** answer every technical unknown before planning.

**Input:** the UC file, its FRs, NFRs, BRs.

**Process:**

1. Run skill `research-questions` on the UC to generate a research checklist.
2. Create the checklist at `plans/UC-XXX/research-checklist.md`.
3. Create GitHub Issues for each question using the `research-ticket` template.
   Label: `phase:research`, `uc:XXX`.
4. For technical questions, provide options with a tradeoffs table.
5. The user researches (with agent help). Each answered question produces either:
   - An update to the research file in `docs/research/`, or
   - A decision record in `docs/decisions/DEC-NNN-topic.md`.
6. Close each research ticket when its question is answered or decided.

**Gate:** all research tickets for this UC are closed.

### Phase 2 — Testing plan

**Goal:** define every test before writing any implementation.

**Input:** FRs with ACs, NFRs, decisions from Phase 1.

**Process:**

1. Run skill `testing-plan` on the UC's FRs/ACs and decisions.
2. Create the plan at `plans/UC-XXX/testing-plan.md`.
3. Create GitHub Issues for pre-implementation test stubs using the `test-stub-ticket`
   template. Label: `phase:test-stubs`, `uc:XXX`.
4. Test types and their phases:

   | Type | When written | Phase label |
   |---|---|---|
   | Acceptance tests | Before implementation | `phase:test-stubs` |
   | Security tests | Before implementation | `phase:test-stubs` |
   | Unit tests | Bundled into implementation tickets | `phase:impl` |
   | Integration tests | After the modules they test | `phase:post-impl` |
   | E2E tests | After all implementation | `phase:post-impl` |
   | Smoke tests | After all implementation | `phase:post-impl` |
   | Recovery / resilience tests | After the modules they test | `phase:post-impl` |
   | Regression tests | Grows over time with bug fixes | `phase:post-impl` |
   | Performance tests | After implementation, when NFRs exist | `phase:post-impl` |

5. Close each test stub ticket when the test file exists and the stub runs (red).

**Gate:** all `phase:test-stubs` tickets for this UC are closed.

### Phase 3 — Implementation plan

**Goal:** produce an ordered list of implementation steps tied to tests.

**Input:** testing plan, decisions, research answers.

**Process:**

1. Create the plan at `plans/UC-XXX/implementation-plan.md`.
2. Each step references:
   - What to build (module, function, file path).
   - Which tests it makes pass.
   - Which decisions it depends on.
3. The user reviews and approves the plan.

**Gate:** user approves the implementation plan.

### Phase 4 — Implementation tickets

**Goal:** break the plan into flash-model-friendly GitHub Issues.

**Input:** approved implementation plan.

**Process:**

1. Create GitHub Issues using the `implementation-ticket` template.
   Label: `phase:impl`, `uc:XXX`.
2. Each ticket has:
   - `Blocked by` referencing its prerequisite tickets (test stubs, other modules).
   - A test command as acceptance criteria.
   - Explicit `Do NOT` boundaries.
3. Create post-implementation test tickets using the `post-impl-test-ticket` template.
   Label: `phase:post-impl`, `uc:XXX`.
   These are blocked by the implementation tickets they depend on.
4. Update the flow tracker issue with all ticket numbers.

**Gate:** all tickets created and linked.

### Phase 5 — Execution and review

**Goal:** implement all tickets and pass all tests.

**Input:** tickets in dependency order.

**Process:**

1. The user assigns tickets to implementers (DeepSeek/GLM Flash via external tools,
   or Claude sub-agents).
2. Each implementer:
   - Reads the ticket and its linked context.
   - Pushes a branch with the implementation.
   - Runs the test command in the ticket to self-verify.
3. Claude reviews each PR using `/code-review`.
4. Merge when tests pass and review approves.
5. Close the ticket.
6. Update the flow tracker issue.

**Gate:** all `phase:impl` and `phase:post-impl` tickets are closed.

### Phase 6 — Verification

**Goal:** confirm the UC works end-to-end.

**Input:** all code merged, all tests green.

**Process:**

1. Run the full test suite.
2. Run smoke tests.
3. Run E2E tests for the UC's happy path and alternative flows.
4. Run resilience tests for the UC's failure alternatives.
5. Verify against the UC's acceptance criteria.
6. Close the flow tracker issue.

**Gate:** flow tracker issue closed. UC is done.

## Flow tracker issue

Every scoped build has one flow tracker issue — the root issue. It is created at the
start of Phase 1 and links to every other ticket. The scope definition appears at the
top. Template: `.github/ISSUE_TEMPLATE/flow-tracker.md`.

The tracker uses the format:

```markdown
## Phase 1: Research
- [ ] #N question-title (status)

## Phase 2: Testing Plan
- [ ] #N test-stub-title
Blocked by: Phase 1 complete

## Phase 3: Implementation Plan
- [ ] #N plan-review
Blocked by: Phase 2 complete

## Phase 4: Implementation
- [ ] #N module-title
Blocked by: #test-stub, #other-module

## Phase 5: Post-impl Testing
- [ ] #N test-title
Blocked by: #module

## Phase 6: Verification
Blocked by: Phase 5 complete
```

## Ticket rules for flash models

Flash models (DeepSeek V4.1 Flash, GLM 5.3 Flash) need tickets with minimal reasoning
steps. Every implementation ticket must follow these rules:

1. **One concern per ticket.** One function, one component, one module.
2. **Exact file paths.** Not "create a validation module" but "create
   `src/domain/source-validator.ts`".
3. **Input/output contract.** Function signature, parameter types, return type.
4. **Test command.** The command that proves the ticket is done.
5. **Do NOT section.** Explicit boundaries — what NOT to touch, refactor, or change.
6. **Blocked by.** Prerequisites must be merged before starting.
7. **Context section.** What already exists that the implementer needs to know. Include
   file paths and brief descriptions, not "see the codebase".
8. **Maximum 3 files changed per ticket.** If more files need changing, split the ticket.

## Labels

| Label | Meaning |
|---|---|
| `uc:XXX` | Which use case this ticket belongs to |
| `phase:research` | Phase 1 ticket |
| `phase:test-stubs` | Phase 2 ticket |
| `phase:impl-plan` | Phase 3 ticket |
| `phase:impl` | Phase 4 implementation ticket |
| `phase:post-impl` | Phase 5 post-implementation test ticket |
| `flow-tracker` | The root tracker issue for a UC |
| `flash-ready` | Ticket is suitable for a flash model implementer |

## Milestones

One milestone per UC build: `UC-XXX`. All tickets for that UC belong to it.
