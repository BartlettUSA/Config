---
description: Analyze and fix GitHub issue with tests
allowed-tools: Bash, Read, Write, Edit, Grep, Glob, Task, WebFetch
model: sonnet
argument-hint: <issue number or URL>
---

# /fix-github-issue — Analyze and fix GitHub issue

You are running the /fix-github-issue workflow.

## Inputs
- $ARGUMENTS: GitHub issue number (e.g., "123") or full URL

## Hard constraints
- Read the full issue before starting
- Reproduce the issue if it's a bug
- Write or update tests covering the fix
- Create atomic commits with conventional messages
- Do NOT close the issue (let PR do that)

## Process

### Phase 1: Analysis
1. Fetch issue details using `gh issue view <number>`
2. Read issue body, comments, and labels
3. Identify: bug vs feature, affected files, acceptance criteria
4. If reproduction steps exist, attempt to reproduce

### Phase 2: Investigation
1. Search codebase for relevant files using Grep/Glob
2. Read affected modules and understand context
3. Identify root cause (for bugs) or implementation approach (for features)
4. Check existing tests for the affected area

### Phase 3: Implementation
1. Create feature branch: `fix/<issue-number>-<short-desc>` or `feat/<issue-number>-<short-desc>`
2. Write failing test that captures the issue (TDD red phase)
3. Implement the fix/feature (TDD green phase)
4. Refactor if needed while keeping tests green
5. Run full test suite to prevent regressions

### Phase 4: Completion
1. Commit changes with message: `fix: <description> (#<issue>)` or `feat: <description> (#<issue>)`
2. Push branch and create PR referencing the issue
3. Summarize changes and verification steps

## Output format
### Issue Summary
- **Number**: #<number>
- **Type**: <bug/feature/enhancement>
- **Title**: <issue title>

### Root Cause / Approach
<explanation>

### Changes Made
- <file>: <what changed>

### Tests Added/Updated
- <test file>: <what's tested>

### Verification
```bash
<commands to verify fix>
```

### PR
<url>
