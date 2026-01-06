# /tdd — Test-driven development workflow

You are running the /tdd workflow.

## Inputs
Use the user's message as the feature or function to implement using TDD.

## Hard constraints
- Write tests BEFORE implementation (red phase)
- Implement ONLY enough code to pass tests (green phase)
- Refactor ONLY after tests pass (refactor phase)
- Never modify tests to make them pass

## TDD cycle: Red → Green → Refactor

### Phase 1: RED
1. Understand the requirement
2. Write failing tests (happy path, edge cases, error cases)
3. Run tests to confirm they fail for the right reason

### Phase 2: GREEN
1. Write the simplest code that makes tests pass
2. Do NOT add extra functionality
3. Run tests to confirm they pass

### Phase 3: REFACTOR
1. Identify code smells (duplication, long methods, poor naming)
2. Refactor while keeping tests green
3. Run tests after each refactoring step

## Test structure
```
describe('<Feature>')
  it('should <behavior> when <condition>')
  it('should handle <edge case>')
  it('should throw when <invalid input>')
```

## Output format
### TDD Session: <feature>

#### RED Phase
```
<test output showing failures>
```

#### GREEN Phase
```
<test output showing passes>
```

#### REFACTOR Phase
**Changes**: <refactoring done>
**Tests**: Still passing ✅
