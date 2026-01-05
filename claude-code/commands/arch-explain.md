---
description: Summarize architecture and responsibilities of repo/service
allowed-tools: Read, Grep, Glob, Task
model: sonnet
argument-hint: <optional: specific area to focus on>
---

# /arch-explain — Architecture overview

You are running the /arch-explain workflow.

## Inputs
Use $ARGUMENTS as optional FOCUS area. If empty, explain entire repo.

## Hard constraints
- Do NOT edit any files
- Focus on helping new contributors ramp up quickly
- Be concise but thorough
- Use diagrams (ASCII or mermaid) where helpful

## Process
1. Scan project structure (package.json, Cargo.toml, go.mod, etc.)
2. Identify entry points and main modules
3. Map dependencies and data flow
4. Document key patterns and conventions
5. Note any unusual architecture decisions

## Output format
### Project overview
[One paragraph summary]

### Tech stack
[Languages, frameworks, key dependencies]

### Directory structure
```
[Key folders and their purposes]
```

### Core components
[Main modules and their responsibilities]

### Data flow
[How data moves through the system]

### Key patterns
[Design patterns, conventions used]

### Entry points
[Where to start reading code]

### Quick start for contributors
[How to run, test, and make first change]
