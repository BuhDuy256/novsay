---
name: Test stub ticket
about: Write a test stub (pre-implementation) that defines expected behavior.
title: "Test stub: "
labels: phase:test-stubs
---

## Context

**Use case:** UC-XXX
**FR / AC:** FR-NNN / AC-N
**Testing plan:** plans/UC-XXX/testing-plan.md
**Flow tracker:** #N

## Test type

<!-- One of: acceptance, security -->

## What to test

<!-- The behavior being verified. Reference the AC's Cho truoc / Khi / Thi. -->

## Test file

<!-- Exact path where the test file should be created. -->

`tests/...`

## Skeleton

<!-- The test stub code. describe/it blocks with assertions described but not implemented.
     The test must RUN (red) but not PASS. -->

```typescript
// Example — replace with actual skeleton
describe('FR-NNN: title', () => {
  it('AC-N: description', () => {
    // Arrange: ...
    // Act: ...
    // Assert: ...
    throw new Error('Not implemented');
  });
});
```

## Acceptance

- [ ] Test file exists at the specified path
- [ ] Test runs and fails (red) — not a syntax error, a real assertion
- [ ] Test description matches the AC

## Blocked by

<!-- List prerequisite tickets. Research decisions that affect the test shape. -->
