---
description: Test-driven development workflow
allowed-tools: Bash, Read, Write, Edit, Grep, Glob
model: sonnet
argument-hint: <feature or function to implement>
---

# /tdd — Test-driven development workflow

You are running the /tdd workflow.

## Inputs
- $ARGUMENTS: Feature or function to implement using TDD

## Hard constraints
- Write tests BEFORE implementation (red phase)
- Implement ONLY enough code to pass tests (green phase)
- Refactor ONLY after tests pass (refactor phase)
- Never modify tests to make them pass
- Maintain test isolation

## TDD cycle: Red → Green → Refactor

### Phase 1: RED (Write failing tests)
1. Understand the requirement from $ARGUMENTS
2. Identify test cases:
   - Happy path (expected behavior)
   - Edge cases (boundaries, empty inputs)
   - Error cases (invalid inputs, exceptions)
3. Write test file with failing tests
4. Run tests to confirm they fail: `npm test` / `pytest` / `go test`
5. Verify failure is for the right reason (missing implementation, not syntax error)

### Phase 2: GREEN (Minimal implementation)
1. Write the simplest code that makes tests pass
2. Do NOT add extra functionality
3. Do NOT optimize yet
4. Run tests to confirm they pass
5. If tests fail, fix implementation (not tests)

### Phase 3: REFACTOR (Improve code quality)
1. Identify code smells:
   - Duplication
   - Long methods
   - Poor naming
   - Missing abstractions
2. Refactor while keeping tests green
3. Run tests after each refactoring step
4. Commit when refactoring complete

## Test structure template
```
describe('<Feature>')
  describe('<Function/Method>')
    it('should <expected behavior> when <condition>')
    it('should handle <edge case>')
    it('should throw/return error when <invalid input>')
```

## Process
1. Parse $ARGUMENTS to understand the feature
2. Create test file if not exists
3. Write comprehensive failing tests (RED)
4. Run tests, confirm failure
5. Implement minimal solution (GREEN)
6. Run tests, confirm passing
7. Refactor for quality (REFACTOR)
8. Run tests, confirm still passing
9. Commit with message: `feat: <feature> (TDD)`

## Output format
### TDD Session: <feature>

#### RED Phase
**Tests written**: <count>
```
<test output showing failures>
```

#### GREEN Phase
**Implementation**: <file>
```
<test output showing passes>
```

#### REFACTOR Phase
**Changes**: <refactoring done>
**Tests**: Still passing ✅

#### Coverage
| Metric | Value |
|--------|-------|
| Lines | <n>% |
| Branches | <n>% |
| Functions | <n>% |

#### Commit
`<commit message>`
