---
description: Prime Claude with comprehensive project understanding
allowed-tools: Bash, Read, Grep, Glob
model: sonnet
argument-hint: [optional: specific area to focus on]
---

# /context-prime — Prime project context

You are running the /context-prime workflow.

## Inputs
- $ARGUMENTS: Optional focus area (e.g., "authentication", "API", "frontend")

## Hard constraints
- Read key files, don't just list them
- Understand architecture before answering questions
- Identify patterns and conventions
- Note any tech debt or inconsistencies

## Context gathering sequence

### 1. Project identity
```bash
# Root files
cat README.md 2>/dev/null | head -100
cat CONTRIBUTING.md 2>/dev/null | head -50
cat .claude/CLAUDE.md 2>/dev/null
```

### 2. Technology stack
| File | Indicates |
|------|-----------|
| package.json | Node.js, dependencies |
| requirements.txt / pyproject.toml | Python |
| go.mod | Go |
| Cargo.toml | Rust |
| Dockerfile | Containerization |
| docker-compose.yml | Service architecture |

### 3. Project structure
```bash
# Directory layout
find . -type f -name "*.ts" -o -name "*.py" -o -name "*.go" | head -50
ls -la src/ app/ lib/ pkg/ 2>/dev/null
```

### 4. Architecture patterns
Look for:
- API routes/endpoints
- Database models/schemas
- Authentication/authorization
- State management
- Configuration system

### 5. Code conventions
Analyze:
- Naming patterns (camelCase, snake_case)
- File organization
- Import structure
- Error handling patterns
- Logging approach
- Test structure

### 6. Development workflow
```bash
# Scripts and tooling
cat package.json | jq '.scripts' 2>/dev/null
cat Makefile 2>/dev/null | head -30
cat .github/workflows/*.yml 2>/dev/null | head -50
```

## Focus area deep-dive
If $ARGUMENTS specifies a focus:
1. Find files related to that area
2. Read implementations
3. Trace dependencies
4. Understand data flow
5. Note integration points

## Output format
### Project Context: <project-name>

#### Overview
<2-3 sentence project summary>

#### Tech Stack
| Category | Technology |
|----------|------------|
| Language | <lang> |
| Framework | <framework> |
| Database | <db> |
| Testing | <test framework> |
| CI/CD | <platform> |

#### Architecture
```
<high-level component diagram or description>
```

#### Key Patterns
- **Routing**: <pattern>
- **State**: <pattern>
- **Auth**: <pattern>
- **Data access**: <pattern>

#### Code Conventions
- Naming: <convention>
- Structure: <pattern>
- Error handling: <approach>

#### Entry Points
| Purpose | File |
|---------|------|
| Main | <path> |
| API | <path> |
| Config | <path> |

#### Notable Files
<list of important files to be aware of>

#### Focus Area: <area> (if specified)
<detailed analysis of focus area>

---
**Context loaded.** Ready for questions about this codebase.
