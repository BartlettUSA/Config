---
description: Dynamic problem-solving with automatic agent selection
allowed-tools: Bash, Read, Write, Edit, Grep, Glob, Task
model: sonnet
argument-hint: <issue description or error message>
---

# /smart-fix — Intelligent problem resolution

You are running the /smart-fix workflow.

## Inputs
- $ARGUMENTS: Problem description, error message, or issue number

## Hard constraints
- Analyze before acting
- Choose appropriate approach based on problem type
- Verify fix resolves the issue
- Don't introduce new problems

## Problem classification

### Category detection
| Pattern | Category | Approach |
|---------|----------|----------|
| Stack trace, exception | Runtime error | Debug + trace |
| Build failed, compile error | Build error | Syntax + deps |
| Test failed | Test failure | TDD debug |
| Slow, timeout, memory | Performance | Profiling |
| 401, 403, forbidden | Auth issue | Security review |
| Deprecated, outdated | Tech debt | Modernization |
| Type error, undefined | Type issue | Type analysis |

### Approach mapping
| Category | Primary focus | Tools |
|----------|---------------|-------|
| Runtime error | Stack trace analysis | Grep, Read |
| Build error | Dependency + syntax | Bash, Read |
| Test failure | Test + impl comparison | Read, Edit |
| Performance | Profiling + optimization | Bash, Task |
| Auth issue | Permission + config | Grep, Read |
| Tech debt | Refactoring | Edit, Task |

## Process

### Phase 1: Analysis
1. Parse $ARGUMENTS for error patterns
2. Search for related code
3. Identify root cause category
4. Determine fix approach

### Phase 2: Investigation
```
If runtime error:
  - Find stack trace location
  - Read surrounding code
  - Check recent changes

If build error:
  - Check syntax at error location
  - Verify dependencies
  - Check environment

If test failure:
  - Read failing test
  - Compare with implementation
  - Check test data
```

### Phase 3: Resolution
1. Apply targeted fix
2. Run verification (tests, build, lint)
3. If fix fails, try alternative approach
4. Document what was changed

### Phase 4: Verification
```bash
# Run appropriate verification
npm test 2>/dev/null || pytest 2>/dev/null || go test ./...
npm run build 2>/dev/null || make build 2>/dev/null
npm run lint 2>/dev/null || ruff check . 2>/dev/null
```

## Multi-domain issues
For complex issues spanning multiple areas:
1. Identify all affected domains
2. Address in dependency order
3. Verify each fix independently
4. Test integration between fixes

## Output format
### Smart Fix: <problem summary>

#### Problem Analysis
**Category**: <detected category>
**Root cause**: <explanation>
**Affected files**: <list>

#### Investigation
```
<relevant code or error details>
```

#### Fix Applied
| File | Change | Reason |
|------|--------|--------|
| <file> | <change> | <why> |

#### Verification
```
<test/build output>
```

#### Result
- **Status**: ✅ Fixed / ⚠️ Partial / ❌ Unresolved
- **Tests passing**: Yes/No
- **Build passing**: Yes/No

#### If Unresolved
**Attempted approaches**:
1. <approach 1> - <result>
2. <approach 2> - <result>

**Recommended next steps**:
- <manual action needed>
