---
name: systematic-debugging
description: Use when encountering any bug, test failure, or unexpected behavior, before proposing fixes
---

# Systematic Debugging

## Overview

Random fixes waste time and create new bugs. Quick patches mask underlying issues.

**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.

## The Iron Law

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

## The Four Phases

### Phase 1: Root Cause Investigation

**BEFORE attempting ANY fix:**

1. **Read Error Messages Carefully** — Don't skip past errors or warnings. Read stack traces completely.
2. **Reproduce Consistently** — Can you trigger it reliably? If not reproducible → gather more data, don't guess.
3. **Check Recent Changes** — Git diff, recent commits, new dependencies, config changes.
4. **Gather Evidence in Multi-Component Systems** — For each component boundary: log what data enters and exits, verify environment/config propagation.
5. **Trace Data Flow** — Where does bad value originate? Keep tracing up until you find the source. Fix at source, not symptom.

### Phase 2: Pattern Analysis

1. Find working examples — locate similar working code in same codebase.
2. Compare against references — read reference implementation COMPLETELY.
3. Identify differences — list every difference, however small.
4. Understand dependencies — what settings, config, environment?

### Phase 3: Hypothesis and Testing

1. Form single hypothesis — state clearly: "I think X is the root cause because Y."
2. Test minimally — make the SMALLEST possible change to test hypothesis.
3. Verify before continuing — did it work? Yes → Phase 4. No → form NEW hypothesis.

### Phase 4: Implementation

1. Create failing test case before fixing.
2. Implement single fix addressing root cause.
3. Verify fix — test passes? No other tests broken?
4. If fix doesn't work: count attempts. If ≥ 3 → STOP and question the architecture.

## Red Flags — STOP and Return to Phase 1

- "Quick fix for now, investigate later"
- "Just try changing X and see if it works"
- "It's probably X, let me fix that"
- Proposing solutions before tracing data flow
- "One more fix attempt" (when already tried 2+)

## Quick Reference

| Phase | Key Activities | Success Criteria |
|-------|---------------|------------------|
| **1. Root Cause** | Read errors, reproduce, check changes, gather evidence | Understand WHAT and WHY |
| **2. Pattern** | Find working examples, compare | Identify differences |
| **3. Hypothesis** | Form theory, test minimally | Confirmed or new hypothesis |
| **4. Implementation** | Create test, fix, verify | Bug resolved, tests pass |
