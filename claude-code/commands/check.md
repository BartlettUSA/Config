---
description: Comprehensive code quality and standards check
allowed-tools: Bash, Read, Grep, Glob
model: sonnet
argument-hint: [optional: specific path or --fix]
---

# /check — Comprehensive code quality check

You are running the /check workflow.

## Inputs
- $ARGUMENTS: Optional path or `--fix` to auto-fix issues

## Hard constraints
- Run all applicable checks for detected project type
- Report issues by severity
- Provide fix commands where available
- Do NOT auto-fix without `--fix` flag

## Check categories

### 1. Linting
| Ecosystem | Tool | Command |
|-----------|------|---------|
| JavaScript/TS | ESLint | `npx eslint . --ext .js,.jsx,.ts,.tsx` |
| Python | Ruff/Flake8 | `ruff check .` or `flake8` |
| Go | golangci-lint | `golangci-lint run` |
| Rust | Clippy | `cargo clippy` |

### 2. Formatting
| Ecosystem | Tool | Check Command |
|-----------|------|---------------|
| JavaScript/TS | Prettier | `npx prettier --check .` |
| Python | Black | `black --check .` |
| Go | gofmt | `gofmt -l .` |
| Rust | rustfmt | `cargo fmt --check` |

### 3. Type checking
| Ecosystem | Tool | Command |
|-----------|------|---------|
| TypeScript | tsc | `npx tsc --noEmit` |
| Python | mypy/pyright | `mypy .` or `pyright` |

### 4. Tests
```bash
# Detect and run test suite
npm test 2>/dev/null || pytest 2>/dev/null || go test ./... 2>/dev/null || cargo test 2>/dev/null
```

### 5. Build verification
```bash
# Verify build succeeds
npm run build 2>/dev/null || python -m py_compile *.py 2>/dev/null || go build ./... 2>/dev/null || cargo build 2>/dev/null
```

## Process
1. Detect project type from config files
2. Run linting checks
3. Run formatting checks
4. Run type checks (if applicable)
5. Run test suite
6. Verify build
7. Aggregate results

## Output format
### Code Quality Report

**Project type**: <detected>
**Scope**: <path or "full project">

#### Linting
| Status | Issues | Tool |
|--------|--------|------|
| ✅/❌ | <count> | <tool> |

<details of issues if any>

#### Formatting
| Status | Files | Tool |
|--------|-------|------|
| ✅/❌ | <count> | <tool> |

#### Type Checking
| Status | Errors | Tool |
|--------|--------|------|
| ✅/❌ | <count> | <tool> |

#### Tests
| Status | Passed | Failed | Skipped |
|--------|--------|--------|---------|
| ✅/❌ | <n> | <n> | <n> |

#### Build
| Status | Duration |
|--------|----------|
| ✅/❌ | <time> |

#### Summary
- Total issues: <count>
- Blocking: <count>
- Warnings: <count>

#### Fix Commands
```bash
# Run these to fix issues
<auto-fix commands>
```
