# /check — Comprehensive code quality check

You are running the /check workflow.

## Inputs
Use the user's message for optional path or `--fix` to auto-fix issues.

## Hard constraints
- Run all applicable checks for detected project type
- Report issues by severity
- Provide fix commands where available
- Do NOT auto-fix without `--fix` flag

## Check categories

### 1. Linting
| Ecosystem | Tool |
|-----------|------|
| JavaScript/TS | ESLint |
| Python | Ruff/Flake8 |
| Go | golangci-lint |

### 2. Formatting
| Ecosystem | Tool |
|-----------|------|
| JavaScript/TS | Prettier |
| Python | Black |
| Go | gofmt |

### 3. Type checking
- TypeScript: `tsc --noEmit`
- Python: `mypy` or `pyright`

### 4. Tests
Run test suite for detected ecosystem

### 5. Build verification
Verify build succeeds

## Process
1. Detect project type
2. Run linting, formatting, type checks
3. Run test suite
4. Verify build
5. Aggregate results

## Output format
### Code Quality Report

| Check | Status | Issues |
|-------|--------|--------|
| Linting | ✅/❌ | <count> |
| Formatting | ✅/❌ | <count> |
| Types | ✅/❌ | <count> |
| Tests | ✅/❌ | <pass/fail> |
| Build | ✅/❌ | |

#### Fix Commands
```bash
<auto-fix commands>
```
