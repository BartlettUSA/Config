---
description: Full red-green-refactor TDD orchestration
allowed-tools: Bash, Read, Write, Edit, Grep, Glob, Task
model: sonnet
argument-hint: <feature> [--strict] [--coverage=80]
---

# /tdd-cycle — Full TDD orchestration

You are running the /tdd-cycle workflow.

## Inputs
- $ARGUMENTS: Feature to implement plus optional flags
  - `--strict` - Fail if TDD discipline breaks
  - `--coverage=N` - Require N% coverage (default: 80)
  - `--incremental` - One test at a time
  - `--suite` - Write all tests first

## Hard constraints
- Tests MUST be written before implementation
- Each phase must complete before next begins
- Coverage thresholds must be met
- Refactoring cannot change behavior (tests must stay green)

## Coverage thresholds
| Metric | Minimum | Target |
|--------|---------|--------|
| Line coverage | 80% | 90% |
| Branch coverage | 75% | 85% |
| Function coverage | 90% | 100% |

## TDD phases

### Phase 1: Specification
1. Analyze feature requirements
2. Design test architecture:
   - Unit tests for individual functions
   - Integration tests for component interactions
   - Edge case tests for boundaries
3. Create test file structure
4. Document expected behaviors

### Phase 2: RED (Failing tests)
```
Mode: --incremental (default) or --suite

Incremental: Write one test, run, confirm fail, repeat
Suite: Write all tests, run, confirm all fail
```

Validation:
- All tests must fail
- Failures must be "not implemented" not "syntax error"
- Error messages must be meaningful

### Phase 3: GREEN (Minimal implementation)
1. Implement just enough to pass first test
2. Run tests after each change
3. Continue until all tests pass
4. Do NOT optimize or add features

Validation:
- All tests must pass
- No test modifications allowed
- Implementation must be minimal

### Phase 4: REFACTOR (Code quality)
Refactoring triggers:
| Metric | Threshold | Action |
|--------|-----------|--------|
| Cyclomatic complexity | > 10 | Simplify logic |
| Method length | > 20 lines | Extract methods |
| Duplication | > 3 occurrences | Create abstraction |
| Nesting depth | > 3 levels | Flatten structure |

Validation:
- Tests must stay green
- No behavior changes
- Code quality improved

### Phase 5: Integration
1. Run full test suite
2. Check coverage meets thresholds
3. Run linting and type checks
4. Verify no regressions

### Phase 6: Completion
1. Generate coverage report
2. Commit with TDD tag
3. Document any deviations

## Anti-patterns to avoid
- ❌ Writing implementation before tests
- ❌ Modifying tests to pass
- ❌ Skipping refactor phase
- ❌ Adding untested features
- ❌ Testing implementation details

## Output format
### TDD Cycle Report: <feature>

#### Specification
- Test cases planned: <count>
- Coverage target: <N>%

#### RED Phase ✅
- Tests written: <count>
- All failing: Yes

#### GREEN Phase ✅
- Implementation: <files>
- All passing: Yes

#### REFACTOR Phase ✅
- Improvements: <list>
- Tests still passing: Yes

#### Coverage
| Metric | Result | Target | Status |
|--------|--------|--------|--------|
| Lines | <n>% | 80% | ✅/❌ |
| Branches | <n>% | 75% | ✅/❌ |
| Functions | <n>% | 90% | ✅/❌ |

#### TDD Adherence Score: <n>/100
