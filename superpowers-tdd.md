---
name: test-driven-development
description: Use when implementing any feature or bugfix, before writing implementation code
---

# Test-Driven Development (TDD)

## Overview

Write the test first. Watch it fail. Write minimal code to pass.

**Core principle:** If you didn't watch the test fail, you don't know if it tests the right thing.

## The Iron Law

```
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
```

Write code before the test? Delete it. Start over.

## Red-Green-Refactor

### RED — Write Failing Test
Write one minimal test showing what should happen. One behavior, clear name, real code (no mocks unless unavoidable).

### Verify RED — Watch It Fail (MANDATORY, never skip)
Run the test. Confirm: test fails (not errors), failure message is expected, fails because feature missing.

### GREEN — Minimal Code
Write simplest code to pass the test. Don't add features or refactor beyond the test.

### Verify GREEN — Watch It Pass (MANDATORY)
Run the test. Confirm: test passes, other tests still pass, output pristine.

### REFACTOR — Clean Up
After green only: remove duplication, improve names, extract helpers. Keep tests green.

### Repeat
Next failing test for next feature.

## Red Flags — STOP and Start Over

- Code before test
- Test after implementation
- Test passes immediately (without implementation)
- Can't explain why test failed
- "I'll write tests after"
- "Already manually tested it"
- "Just this once"

**All of these mean: Delete code. Start over with TDD.**

## Verification Checklist

Before marking work complete:

- [ ] Every new function/method has a test
- [ ] Watched each test fail before implementing
- [ ] Each test failed for expected reason (feature missing, not typo)
- [ ] Wrote minimal code to pass each test
- [ ] All tests pass
- [ ] Output pristine (no errors, warnings)
- [ ] Tests use real code (mocks only if unavoidable)
- [ ] Edge cases and errors covered

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Too simple to test" | Simple code breaks. Test takes 30 seconds. |
| "I'll test after" | Tests passing immediately prove nothing. |
| "Already manually tested" | Ad-hoc ≠ systematic. No record, can't re-run. |
| "Deleting X hours is wasteful" | Sunk cost fallacy. Keeping unverified code is technical debt. |
| "TDD will slow me down" | TDD faster than debugging. |
