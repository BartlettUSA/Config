---
description: Persist architecture decisions and project state
allowed-tools: Bash, Read, Write, Grep, Glob
model: sonnet
argument-hint: [optional: --full | --decisions | --status]
---

# /context-save — Save project context

You are running the /context-save workflow.

## Inputs
- $ARGUMENTS: What to save
  - (none) - Save current session context
  - `--full` - Complete project snapshot
  - `--decisions` - Architecture decisions only
  - `--status` - Current work status only

## Hard constraints
- Store in `.claude/context/` directory
- Use timestamp versioning
- Include diffable format for tracking changes
- Don't include secrets or credentials

## Context categories

### 1. Project overview
- Project name and purpose
- Tech stack summary
- Team conventions
- Repository structure

### 2. Architecture decisions
| Decision | Options Considered | Choice | Rationale | Date |
|----------|-------------------|--------|-----------|------|
| Database | Postgres, MongoDB | Postgres | ACID compliance | 2024-01-15 |

### 3. Current status
- Features in progress
- Known issues/bugs
- Technical debt items
- Upcoming work

### 4. Code patterns
- Design patterns used
- Naming conventions
- File organization
- Error handling approach
- Testing strategy

### 5. Agent coordination
- What agents have worked on
- Successful agent combinations
- Dependencies between work items

### 6. External integrations
- APIs consumed
- Services deployed to
- Monitoring/logging setup

## Storage structure
```
.claude/context/
├── latest.json           # Current state (symlink)
├── 2024-01-15T10-30-00.json
├── 2024-01-14T15-45-00.json
└── decisions/
    └── adr-001-database.md
```

## Context file format
```json
{
  "version": "1.0",
  "timestamp": "2024-01-15T10:30:00Z",
  "project": {
    "name": "<name>",
    "description": "<desc>",
    "tech_stack": ["<tech>"]
  },
  "architecture": {
    "patterns": ["<pattern>"],
    "decisions": [{"id": "ADR-001", "title": "<title>", "status": "accepted"}]
  },
  "current_status": {
    "in_progress": ["<feature>"],
    "blocked": ["<issue>"],
    "completed_recently": ["<feature>"]
  },
  "conventions": {
    "naming": "<style>",
    "structure": "<description>",
    "testing": "<approach>"
  },
  "agent_history": [
    {"agent": "<type>", "task": "<description>", "outcome": "success"}
  ]
}
```

## Process
1. Gather current project state
2. Read existing context if available
3. Merge new information
4. Save with timestamp
5. Update `latest.json` symlink
6. Generate summary of changes

## Output format
### Context Saved

**File**: `.claude/context/<timestamp>.json`
**Mode**: <full|decisions|status|session>

#### Saved Information
| Category | Items | Status |
|----------|-------|--------|
| Project overview | <n> fields | ✅ |
| Architecture decisions | <n> decisions | ✅ |
| Current status | <n> items | ✅ |
| Code patterns | <n> patterns | ✅ |
| Agent history | <n> entries | ✅ |

#### Changes from Previous
- Added: <list>
- Updated: <list>
- Removed: <list>

#### Restore Command
```bash
# To restore this context in a new session:
/context-restore <timestamp>
```
