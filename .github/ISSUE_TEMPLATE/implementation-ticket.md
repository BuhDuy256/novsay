---
name: Implementation ticket
about: A single implementation task for a flash model or agent to complete.
title: "Impl: "
labels: phase:impl, flash-ready
---

## Context

<!-- What already exists that the implementer needs to know.
     Include file paths and brief descriptions. Not "see the codebase". -->

**Use case:** UC-XXX
**Decisions:** DEC-NNN (link to docs/decisions/)
**Flow tracker:** #N

### Existing files

<!-- List files the implementer needs to read or depend on. -->

- `path/to/file.ts` — what it contains

## Task

<!-- Exactly what to create or change. File paths, function signatures, types. -->

### Create / modify

- **File:** `src/...`
- **Function:** `functionName(param: Type): ReturnType`
- **Behavior:** what the function does, in one or two sentences

## Tests to pass

<!-- The command that proves this ticket is done. -->

```bash
npm test -- --grep "FR-NNN"
```

**Specific tests:**
- [ ] `tests/.../test-file.ts` — AC-N description

## Do NOT

<!-- Explicit boundaries. What the implementer must NOT touch, refactor, or change. -->

- Do not modify files outside the listed paths.
- Do not add dependencies not listed here.
- Do not refactor existing code.

## Acceptance

- [ ] All listed tests pass
- [ ] No other tests broken
- [ ] Maximum 3 files changed
- [ ] Type checks pass (`npm run typecheck` or equivalent)

## Blocked by

<!-- Prerequisite tickets that must be merged before starting this one. -->

- #N (test stub)
- #N (other module)
