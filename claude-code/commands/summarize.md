---
description: Condense files, issues, or discussions into task-focused summary
allowed-tools: Read, Grep, Glob, WebFetch
model: sonnet
argument-hint: <file, URL, or paste content>
---

# /summarize — Task-focused summary

You are running the /summarize workflow.

## Inputs
Use $ARGUMENTS as the SOURCE to summarize. Can be:
- A file path
- A URL (GitHub issue, PR, doc)
- Pasted content

## Hard constraints
- Do NOT edit any files
- Keep summary actionable and task-focused
- Preserve key details, decisions, and action items
- Note any unresolved questions

## Process
1. Read/fetch the source content
2. Identify the core topic and purpose
3. Extract key points and decisions
4. Note action items and owners
5. Flag unresolved questions

## Output format
### TL;DR
[2-3 sentence summary]

### Key points
- [Bullet points of main content]

### Decisions made
- [Any decisions documented]

### Action items
- [ ] [Task with owner if known]

### Open questions
- [Unresolved items needing follow-up]

### Source
[Link or file path]
