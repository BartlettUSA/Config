---
description: Generate comprehensive test suite (unit, integration, e2e)
allowed-tools: Bash, Read, Write, Edit, Grep, Glob
model: sonnet
argument-hint: <file or module to test> [--type=unit|integration|e2e|all]
---

# /test-harness — Generate comprehensive test suite

You are running the /test-harness workflow.

## Inputs
- $ARGUMENTS: File/module to test plus optional type
  - `--type=unit` - Unit tests only
  - `--type=integration` - Integration tests only
  - `--type=e2e` - End-to-end tests only
  - `--type=all` - All test types (default)

## Hard constraints
- Match project's existing test framework and style
- Include positive, negative, and edge cases
- Use realistic test data
- Maintain test isolation
- Follow AAA pattern (Arrange, Act, Assert)

## Test frameworks by ecosystem
| Ecosystem | Unit | Integration | E2E |
|-----------|------|-------------|-----|
| Node.js | Jest, Vitest | Supertest | Playwright, Cypress |
| Python | pytest | pytest | pytest + Selenium |
| Go | testing | testing | testing |
| Rust | cargo test | cargo test | - |

## Test categories

### Unit tests
- Test single functions/methods in isolation
- Mock all dependencies
- Fast execution (< 100ms per test)
- High volume (many small tests)

```javascript
describe('functionName', () => {
  it('should return expected output for valid input', () => {
    // Arrange
    const input = 'valid';
    // Act
    const result = functionName(input);
    // Assert
    expect(result).toBe('expected');
  });
});
```

### Integration tests
- Test component interactions
- Use real dependencies where practical
- Test database operations, API calls
- Medium execution time

```javascript
describe('API /users', () => {
  it('should create user and return 201', async () => {
    const response = await request(app)
      .post('/users')
      .send({ name: 'Test User' });
    expect(response.status).toBe(201);
  });
});
```

### End-to-end tests
- Test complete user workflows
- Use browser automation
- Test real UI interactions
- Longer execution time

```javascript
test('user can complete checkout', async ({ page }) => {
  await page.goto('/products');
  await page.click('[data-testid="add-to-cart"]');
  await page.click('[data-testid="checkout"]');
  await expect(page.locator('.confirmation')).toBeVisible();
});
```

## Process
1. Read target file/module
2. Analyze exports, functions, classes
3. Detect existing test framework
4. Generate test file structure
5. Write tests for each function:
   - Happy path
   - Edge cases (null, empty, max values)
   - Error cases (invalid input, exceptions)
6. Add test data fixtures
7. Run tests to verify they execute

## Test data patterns
```javascript
// Factory pattern
const createUser = (overrides = {}) => ({
  id: 1,
  name: 'Test User',
  email: 'test@example.com',
  ...overrides,
});

// Fixtures
const fixtures = {
  validUser: createUser(),
  invalidUser: createUser({ email: 'invalid' }),
  adminUser: createUser({ role: 'admin' }),
};
```

## Output format
### Test Harness: <target>

**Framework**: <detected>
**Test types**: <unit/integration/e2e>

#### Files created
| File | Type | Tests |
|------|------|-------|
| <path> | unit | <n> |

#### Test summary
| Category | Count | Coverage |
|----------|-------|----------|
| Happy path | <n> | - |
| Edge cases | <n> | - |
| Error cases | <n> | - |

#### Run command
```bash
<command to run tests>
```

#### Sample output
```
<test run output>
```
