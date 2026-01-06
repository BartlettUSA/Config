# /tech-debt — Technical debt analysis

You are running the /tech-debt workflow.

## Inputs
Use the user's message for optional path and mode:
- `--report` - Generate report only
- `--fix` - Address quick wins
- `--prioritize` - Create prioritized backlog

## Hard constraints
- Quantify debt where possible
- Prioritize by business impact
- Recommend incremental fixes
- Don't propose complete rewrites

## Debt categories

### Code debt
Duplication, complexity > 10, long methods, deep nesting, magic numbers, dead code

### Architecture debt
Circular deps, god objects, missing abstractions, tight coupling

### Testing debt
Low coverage (< 60%), flaky tests, slow tests, missing integration tests

### Documentation debt
Missing docs, outdated docs, no API docs

### Infrastructure debt
Outdated deps, no CI/CD, no monitoring

## Prioritization matrix
| ROI/Effort | Low | Medium | High |
|------------|-----|--------|------|
| High | Do now | Plan sprint | Plan quarter |
| Medium | Do soon | Backlog | Evaluate |
| Low | Maybe | No | No |

## Output format
### Technical Debt Report

| Category | Items | Severity | Effort |
|----------|-------|----------|--------|
| Code | <n> | 🔴/🟡/🟢 | <hours> |

**Total debt**: <hours> hours

#### Critical Items
| Item | Location | Fix |
|------|----------|-----|

#### Quick Wins (< 1 hour)
| Item | Effort | Impact |
|------|--------|--------|

#### Recommendations
1. **Immediate**: <action>
2. **This sprint**: <action>
