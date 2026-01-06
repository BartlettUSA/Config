# /test-harness — Generate comprehensive test suite

You are running the /test-harness workflow.

## Inputs
Use the user's message as the file/module to test plus optional type:
- `--type=unit` - Unit tests only
- `--type=integration` - Integration tests only
- `--type=e2e` - End-to-end tests only
- `--type=all` - All test types (default)

## Hard constraints
- Match project's existing test framework and style
- Include positive, negative, and edge cases
- Use realistic test data
- Follow AAA pattern (Arrange, Act, Assert)

## Test categories

### Unit tests
- Test single functions in isolation
- Mock all dependencies
- Fast execution (< 100ms per test)

### Integration tests
- Test component interactions
- Use real dependencies where practical
- Test database operations, API calls

### End-to-end tests
- Test complete user workflows
- Use browser automation
- Test real UI interactions

## Process
1. Read target file/module
2. Analyze exports, functions, classes
3. Detect existing test framework
4. Generate test file structure
5. Write tests (happy path, edge cases, error cases)
6. Add test data fixtures
7. Run tests to verify

## Output format
### Test Harness: <target>

**Framework**: <detected>

| File | Type | Tests |
|------|------|-------|
| <path> | unit | <n> |

#### Run command
```bash
<command>
```
