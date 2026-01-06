---
description: Restore saved project state and decision history
allowed-tools: Bash, Read, Grep, Glob
model: sonnet
argument-hint: [version: latest | timestamp | --list]
---

# /context-restore — Restore project context

You are running the /context-restore workflow.

## Inputs
- $ARGUMENTS: Which version to restore
  - `latest` - Most recent save (default)
  - `<timestamp>` - Specific version
  - `--list` - Show available versions
  - `--diff <v1> <v2>` - Compare versions

## Hard constraints
- Validate context file before loading
- Detect conflicts with current state
- Don't overwrite unsaved work
- Flag outdated information

## Process

### 1. List available versions (if --list)
```bash
ls -la .claude/context/*.json | sort -r
```

### 2. Load context file
```bash
cat .claude/context/latest.json  # or specified version
```

### 3. Validate context
- Check file format is valid JSON
- Verify required fields exist
- Check timestamps are reasonable
- Identify any corruption

### 4. Detect conflicts
Compare saved state with current:
| Category | Saved | Current | Conflict? |
|----------|-------|---------|-----------|
| Tech stack | <list> | <list> | ⚠️ Drift |
| Structure | <hash> | <hash> | ✅ Match |

### 5. Apply context
Load into working memory:
- Project overview
- Architecture decisions
- Code conventions
- Agent history
- Current status

### 6. Generate summary
Highlight:
- Key decisions to remember
- Work in progress
- Known issues
- Next steps

## Conflict resolution
| Conflict type | Resolution |
|---------------|------------|
| File moved | Update path in context |
| Dependency changed | Note version change |
| Pattern changed | Flag for review |
| Decision reversed | Update ADR status |

## Output format
### Context Restored

**Source**: `.claude/context/<version>.json`
**Saved**: <timestamp>
**Age**: <time since save>

#### Project Overview
- **Name**: <name>
- **Stack**: <technologies>
- **Purpose**: <description>

#### Architecture Decisions
| ID | Decision | Status |
|----|----------|--------|
| ADR-001 | <decision> | accepted |

#### Code Conventions
- Naming: <style>
- Structure: <pattern>
- Testing: <approach>

#### Current Status
**In Progress**:
- <work item>

**Blocked**:
- <blocker>

**Recently Completed**:
- <completed item>

#### Conflicts Detected
| Item | Saved | Current | Action Needed |
|------|-------|---------|---------------|
| <item> | <old> | <new> | <action> |

#### Agent History
| Agent | Last Task | Outcome |
|-------|-----------|---------|
| <type> | <task> | <result> |

---
**Context loaded.** Ready to continue work with full project history.
