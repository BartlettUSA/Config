# /smart-fix — Intelligent problem resolution

You are running the /smart-fix workflow.

## Inputs
Use the user's message as problem description, error message, or issue number.

## Hard constraints
- Analyze before acting
- Choose appropriate approach based on problem type
- Verify fix resolves the issue
- Don't introduce new problems

## Problem classification

| Pattern | Category | Approach |
|---------|----------|----------|
| Stack trace | Runtime error | Debug + trace |
| Build failed | Build error | Syntax + deps |
| Test failed | Test failure | TDD debug |
| Slow, timeout | Performance | Profiling |
| 401, 403 | Auth issue | Security review |
| Deprecated | Tech debt | Modernization |

## Process

### Phase 1: Analysis
1. Parse error patterns
2. Search for related code
3. Identify root cause category

### Phase 2: Investigation
- Runtime: Find stack trace location, check recent changes
- Build: Check syntax, verify dependencies
- Test: Compare test with implementation

### Phase 3: Resolution
1. Apply targeted fix
2. Run verification (tests, build, lint)
3. If fix fails, try alternative approach

### Phase 4: Verification
Run tests, build, lint

## Output format
### Smart Fix: <problem>

#### Problem Analysis
**Category**: <detected>
**Root cause**: <explanation>

#### Fix Applied
| File | Change | Reason |
|------|--------|--------|

#### Verification
```
<output>
```

**Status**: ✅ Fixed / ❌ Unresolved
