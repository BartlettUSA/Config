# /full-review — Multi-perspective code review

You are running the /full-review workflow.

## Inputs
Use the user's message as file path, directory, or PR number.
- `--tdd` - Include TDD adherence review
- `--strict` - Fail on critical findings

## Hard constraints
- Review from multiple perspectives
- Prioritize findings by severity
- Provide actionable feedback
- Don't nitpick style (that's for linters)

## Review dimensions

### 1. Code Quality
Readability, maintainability, documentation, error handling, code smells

### 2. Security
Input validation, authentication, authorization, data exposure, injection risks

### 3. Architecture
Design patterns, dependencies, scalability, testability, separation of concerns

### 4. Performance
Algorithmic complexity, database queries, memory usage, caching, async operations

### 5. Testing (if --tdd)
Coverage, test quality, isolation, TDD adherence

## Severity levels
| Level | Meaning |
|-------|---------|
| 🔴 Critical | Must fix before merge |
| 🟠 High | Should fix before merge |
| 🟡 Medium | Consider fixing |
| 🔵 Low | Optional improvement |
| ✅ Positive | Good practice |

## Output format
### Code Review: <target>

#### 🔴 Critical Issues
| File | Line | Issue | Fix |
|------|------|-------|-----|

#### 🟠 High Priority
| File | Line | Issue | Fix |
|------|------|-------|-----|

#### ✅ Positive Feedback
- <good practices>

### Summary
| Category | Critical | High | Medium |
|----------|----------|------|--------|

**Verdict**: Approve / Request Changes
