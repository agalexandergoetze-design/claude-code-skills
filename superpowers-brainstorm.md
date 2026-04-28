---
name: brainstorming
description: Use when exploring a new feature or problem — structured dialogue to turn ideas into a design before any implementation
---

# Brainstorming

## Overview

Turn ideas into designs through structured dialogue. **No code until the user approves a written design.**

**HARD GATE:** Do NOT invoke any implementation skill, write any code, or scaffold anything until you have presented a design and the user has approved it.

## The 9-Step Workflow

1. **Explore project context** — read relevant files, docs, recent commits
2. **Offer visual companion** — suggest a diagram if it would help clarify the design
3. **Ask clarifying questions** — ONE question at a time, prefer multiple choice over open-ended
4. **Propose 2-3 approaches** — with trade-offs for each, never jump straight to one solution
5. **Present design in sections** — architecture, components, data flow, error handling, testing
6. **Write design documentation** — save to `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`
7. **Self-review the spec** — check for placeholders, contradictions, missing requirements
8. **Get user approval** — present written spec and wait for explicit sign-off
9. **Invoke writing-plans skill** — only after approval, this is the only allowed next step

## Rules

- **One question per message** — never stack multiple questions
- **Always propose alternatives** — minimum 2-3 options before settling on one
- **Incremental validation** — get feedback on each design section before moving to the next
- **Scope assessment** — flag if the project needs to be decomposed into sub-projects
- **No implementation until approved** — this is non-negotiable

## Design Section Format

Each section: brief for simple items, up to 300 words for nuanced ones.

Cover:
- Architecture (overall structure)
- Components (what each part does)
- Data flow (how data moves through the system)
- Error handling (what can go wrong and how)
- Testing (how we verify it works)
