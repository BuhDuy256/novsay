---
name: testing-plan
description: Generate a testing plan from FRs, ACs, and decisions. Maps every acceptance criterion to a test type and phase. Identifies security, resilience, performance, and E2E test needs. Used at the start of Phase 2.
---

# Testing plan

Generate the testing plan for a use case build.

## Input

1. The UC file: `docs/spec/02-use-cases/UC-XXX.md`
2. Every FR referenced by the UC — especially their ACs and `Kiểm` tags.
3. Every NFR referenced by the UC.
4. Decisions from Phase 1: `docs/decisions/DEC-*.md`
5. The research checklist: `plans/UC-XXX/research-checklist.md`

## Process

### Step 1 — Map ACs to test types

For each FR's AC:

- Read the `Kiểm` tag:
  - `tất định` (deterministic) → acceptance test, automatable
  - `đánh giá` (evaluation) → manual test or test with human judgment

- Determine the test type:
  - Pure validation logic → unit test (with implementation)
  - Security-related (SSRF, input validation) → security test (pre-implementation)
  - External integration (fetch, TTS API) → integration test (post-implementation)

### Step 2 — Identify UC-level tests

- **E2E test:** UC happy path (all S steps in order)
- **E2E tests:** each alternative flow that reaches a different end state
- **Smoke tests:** minimal checks that prove the build works
- **Recovery/resilience tests:** each alternative flow tagged with failure conditions
  (A3, A6, A8 in UC-001)

### Step 3 — Identify NFR tests

- For each NFR, determine if it has a measurable target.
- If yes → performance test with the target as the assertion.
- If it describes a behavior (e.g., background playback) → E2E or integration test.

### Step 4 — Phase assignment

| Test type | Phase | Written when |
|---|---|---|
| Acceptance (tất định) | Pre-implementation | Phase 2 tickets |
| Security | Pre-implementation | Phase 2 tickets |
| Unit | With implementation | Bundled into Phase 4 impl tickets |
| Integration | Post-implementation | Phase 4, blocked by impl |
| E2E | Post-implementation | Phase 4, blocked by impl |
| Smoke | Post-implementation | Phase 4, blocked by impl |
| Recovery / resilience | Post-implementation | Phase 4, blocked by impl |
| Performance | Post-implementation | Phase 4, blocked by impl |

## Output

Create `plans/UC-XXX/testing-plan.md` from the template at
`plans/_TEMPLATES/testing-plan.md`.

## Rules

- Every AC must appear in the plan. No AC is skipped.
- Every UC alternative flow with a failure condition gets a resilience test.
- Do not invent test scenarios beyond what the spec defines.
- Manual tests (đánh giá) are listed but marked as manual — they still need a
  description of what the evaluator checks.
- Pre-implementation test stubs must be runnable (red) — they fail on purpose, not
  because of syntax errors.
