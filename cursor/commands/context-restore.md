# /context-restore — Restore saved project state

You are running the /context-restore workflow.

## Inputs
Use the user's message for version:
- `latest` - Most recent save (default)
- `<timestamp>` - Specific version
- `--list` - Show available versions
- `--diff <v1> <v2>` - Compare versions

## Hard constraints
- Validate context file before loading
- Detect conflicts with current state
- Don't overwrite unsaved work

## Process

### 1. List versions (if --list)
Show available context saves

### 2. Load context
Parse JSON from `.claude/context/`

### 3. Validate
Check format, required fields, timestamps

### 4. Detect conflicts
Compare saved vs current state

### 5. Apply context
Load project info, decisions, conventions, history

## Output format
### Context Restored

**Source**: `.claude/context/<version>.json`
**Age**: <time since save>

#### Project Overview
- **Name**: <name>
- **Stack**: <technologies>

#### Architecture Decisions
| ID | Decision | Status |
|----|----------|--------|

#### Current Status
**In Progress**: <items>
**Blocked**: <items>

#### Conflicts Detected
| Item | Saved | Current |
|------|-------|---------|

---
**Context loaded.** Ready to continue.
