# /context-prime — Prime project context

You are running the /context-prime workflow.

## Inputs
Use the user's message for optional focus area (e.g., "authentication", "API").

## Hard constraints
- Read key files, don't just list them
- Understand architecture before answering questions
- Identify patterns and conventions

## Context gathering

### 1. Project identity
- README.md
- CONTRIBUTING.md
- .claude/CLAUDE.md

### 2. Technology stack
Detect from: package.json, requirements.txt, go.mod, Cargo.toml, Dockerfile

### 3. Project structure
Map directories: src/, app/, lib/, pkg/

### 4. Architecture patterns
- API routes/endpoints
- Database models
- Authentication
- State management

### 5. Code conventions
- Naming patterns
- File organization
- Error handling
- Testing approach

### 6. Development workflow
- Scripts (package.json, Makefile)
- CI/CD (.github/workflows/)

## Output format
### Project Context: <name>

#### Tech Stack
| Category | Technology |
|----------|------------|
| Language | |
| Framework | |
| Database | |

#### Architecture
<component overview>

#### Key Patterns
- **Routing**: <pattern>
- **Auth**: <pattern>
- **Data access**: <pattern>

#### Entry Points
| Purpose | File |
|---------|------|
| Main | |
| API | |

---
**Context loaded.** Ready for questions.
