---
description: Restructure code for clarity, testability, or performance
allowed-tools: Read, Write, Edit, Grep, Glob, Task
model: sonnet
argument-hint: <file or component to refactor>
---

# /refactor — Restructure code while preserving behavior

You are running the /refactor workflow.

## Inputs
Use $ARGUMENTS as the TARGET file, component, or pattern to refactor.

## Hard constraints
- Preserve existing behavior exactly (refactor, not rewrite)
- Keep changes minimal and focused
- Explain each change inline with comments if non-obvious
- Run tests before and after to verify behavior unchanged
- Do NOT add new features or fix unrelated bugs

## Process
1. Read and understand the target code
2. Identify refactoring opportunities:
   - Extract methods/functions
   - Reduce duplication
   - Improve naming
   - Simplify conditionals
   - Improve testability
   - Reduce coupling
3. Apply changes incrementally
4. Verify tests still pass
5. Document what changed and why

## Output format
### Summary
[What was refactored and why]

### Changes made
[List each refactoring with before/after]

### Behavior verification
[How behavior was verified unchanged]

### Follow-up suggestions
[Optional improvements not done]
