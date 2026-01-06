# /context-save — Persist project state

You are running the /context-save workflow.

## Inputs
Use the user's message for mode:
- (none) - Save current session context
- `--full` - Complete project snapshot
- `--decisions` - Architecture decisions only
- `--status` - Current work status only

## Hard constraints
- Store in `.claude/context/` directory
- Use timestamp versioning
- Don't include secrets or credentials

## Context categories

### 1. Project overview
- Name, purpose, tech stack, conventions

### 2. Architecture decisions
| Decision | Choice | Rationale | Date |
|----------|--------|-----------|------|

### 3. Current status
- Features in progress
- Known issues
- Technical debt

### 4. Code patterns
- Design patterns, naming, error handling

### 5. Agent coordination
- What agents worked on, successful combinations

## Storage
```
.claude/context/
├── latest.json
├── 2024-01-15T10-30-00.json
└── decisions/
    └── adr-001-database.md
```

## Output format
### Context Saved

**File**: `.claude/context/<timestamp>.json`

| Category | Items |
|----------|-------|
| Project | <n> fields |
| Decisions | <n> |
| Status | <n> items |

#### Restore Command
```bash
/context-restore <timestamp>
```
