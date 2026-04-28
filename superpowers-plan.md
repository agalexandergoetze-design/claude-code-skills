---
name: writing-plans
description: Use when you need to create a detailed implementation plan for a multi-step development task
---

# Writing Plans

## Overview

Create detailed, actionable implementation plans for multi-step engineering tasks. Each task is bite-sized (2-5 minutes), following TDD. Plans must include actual code — never placeholders.

## Plan Structure

### Header (required)
- Goal: what will be built
- Architecture: key design decisions
- Tech stack: languages, frameworks, tools

### File Map
Map files by responsibility before defining tasks. Keep files focused with clear boundaries.

### Tasks
Each task follows this structure:
1. Write failing test (with exact code)
2. Verify it fails (with expected output)
3. Implement minimal code to pass
4. Verify all tests pass
5. Commit

## Rules

- **No placeholders** — never write "TBD", "add validation", "handle errors". Every step must have actual code.
- **Exact file paths** — always specify the full path.
- **Expected outputs** — include what the test/command output should look like.
- **One thing per task** — each task must be completable in 2-5 minutes.
- **Self-review** — after writing, scan for missing requirements and placeholder patterns.

## Anti-Patterns to Avoid

- "Add error handling" without specifying what errors and how
- "Refactor X" without specifying the exact change
- Tasks longer than 5 minutes
- Missing file paths
- Code blocks with `// TODO` or `...`

## After Writing

Offer two execution paths:
1. **Subagent-driven** — fresh agent per task with review checkpoints (higher quality)
2. **Inline** — execute sequentially using the executing-plans skill

Save plan to `docs/plans/YYYY-MM-DD-<topic>.md`.
