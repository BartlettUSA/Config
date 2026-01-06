---
description: Multi-perspective code review (security, architecture, performance)
allowed-tools: Bash, Read, Grep, Glob, Task
model: sonnet
argument-hint: <file or PR number> [--tdd]
---

# /full-review — Multi-perspective code review

You are running the /full-review workflow.

## Inputs
- $ARGUMENTS: File path, directory, or PR number
  - `--tdd` - Include TDD adherence review
  - `--strict` - Fail on any critical finding

## Hard constraints
- Review from multiple perspectives
- Prioritize findings by severity
- Provide actionable feedback
- Don't nitpick style (that's for linters)

## Review dimensions

### 1. Code Quality
| Aspect | Check |
|--------|-------|
| Readability | Clear naming, logical structure |
| Maintainability | Single responsibility, low coupling |
| Documentation | Comments where needed, not obvious |
| Error handling | Proper error propagation |
| Code smells | Duplication, long methods, deep nesting |

### 2. Security
| Aspect | Check |
|--------|-------|
| Input validation | All user input sanitized |
| Authentication | Proper auth checks |
| Authorization | Permission verification |
| Data exposure | No sensitive data in logs/errors |
| Injection risks | SQL, XSS, command injection |

### 3. Architecture
| Aspect | Check |
|--------|-------|
| Design patterns | Appropriate patterns used |
| Dependencies | Minimal, well-abstracted |
| Scalability | Can handle growth |
| Testability | Easy to unit test |
| Separation of concerns | Clear boundaries |

### 4. Performance
| Aspect | Check |
|--------|-------|
| Algorithmic complexity | O(n) analysis |
| Database queries | N+1 problems, missing indexes |
| Memory usage | Leaks, large allocations |
| Caching | Appropriate use of caching |
| Async operations | Non-blocking where needed |

### 5. Testing (if --tdd)
| Aspect | Check |
|--------|-------|
| Test coverage | Critical paths covered |
| Test quality | Testing behavior, not implementation |
| Test isolation | No shared state |
| TDD adherence | Tests written first |

## Severity levels
| Level | Meaning | Action |
|-------|---------|--------|
| 🔴 Critical | Security/data risk | Must fix before merge |
| 🟠 High | Bug or major issue | Should fix before merge |
| 🟡 Medium | Improvement needed | Consider fixing |
| 🔵 Low | Suggestion | Optional improvement |
| ✅ Positive | Good practice | Recognition |

## Process
1. Identify scope (file, directory, or PR diff)
2. Read code and understand context
3. Review from each perspective
4. Consolidate and prioritize findings
5. Generate actionable report

## Output format
### Code Review: <target>

**Scope**: <files reviewed>
**Reviewer perspectives**: Code, Security, Architecture, Performance

---

#### 🔴 Critical Issues
| File | Line | Issue | Recommendation |
|------|------|-------|----------------|
| <file> | <line> | <issue> | <fix> |

#### 🟠 High Priority
| File | Line | Issue | Recommendation |
|------|------|-------|----------------|

#### 🟡 Medium Priority
| File | Line | Issue | Recommendation |
|------|------|-------|----------------|

#### 🔵 Suggestions
| File | Line | Suggestion |
|------|------|------------|

#### ✅ Positive Feedback
- <recognition of good practices>

---

### Summary
| Category | Critical | High | Medium | Low |
|----------|----------|------|--------|-----|
| Code Quality | <n> | <n> | <n> | <n> |
| Security | <n> | <n> | <n> | <n> |
| Architecture | <n> | <n> | <n> | <n> |
| Performance | <n> | <n> | <n> | <n> |

**Verdict**: <Approve / Request Changes / Needs Discussion>
