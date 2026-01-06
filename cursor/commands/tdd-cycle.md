# /tdd-cycle — Full red-green-refactor TDD orchestration

You are running the /tdd-cycle workflow.

## Inputs
Use the user's message as the feature plus optional flags:
- `--strict` - Fail if TDD discipline breaks
- `--coverage=N` - Require N% coverage (default: 80)

## Hard constraints
- Tests MUST be written before implementation
- Each phase must complete before next begins
- Coverage thresholds must be met

## Coverage thresholds
| Metric | Minimum |
|--------|---------|
| Line coverage | 80% |
| Branch coverage | 75% |
| Function coverage | 90% |

## Phases

### 1. Specification
- Analyze requirements
- Design test architecture
- Document expected behaviors

### 2. RED (Failing tests)
- Write comprehensive failing tests
- Verify failures are "not implemented" not "syntax error"

### 3. GREEN (Minimal implementation)
- Implement just enough to pass
- No test modifications allowed

### 4. REFACTOR (Code quality)
Triggers: complexity > 10, method > 20 lines, duplication

### 5. Integration
- Run full test suite
- Check coverage meets thresholds

## Anti-patterns to avoid
- ❌ Writing implementation before tests
- ❌ Modifying tests to pass
- ❌ Skipping refactor phase
- ❌ Adding untested features

## Output format
### TDD Cycle: <feature>

| Phase | Status | Notes |
|-------|--------|-------|
| RED | ✅ | <n> tests failing |
| GREEN | ✅ | All passing |
| REFACTOR | ✅ | <improvements> |

#### Coverage
| Metric | Result | Target |
|--------|--------|--------|
| Lines | <n>% | 80% |
| Branches | <n>% | 75% |
