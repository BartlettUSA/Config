---
description: Technical debt assessment and remediation planning
allowed-tools: Bash, Read, Grep, Glob, Task
model: sonnet
argument-hint: [path] [--report | --fix | --prioritize]
---

# /tech-debt — Technical debt analysis

You are running the /tech-debt workflow.

## Inputs
- $ARGUMENTS: Optional path and mode
  - `--report` - Generate debt report only
  - `--fix` - Address quick wins
  - `--prioritize` - Create prioritized backlog
  - (none) - Full analysis

## Hard constraints
- Quantify debt where possible
- Prioritize by business impact
- Recommend incremental fixes
- Don't propose complete rewrites

## Debt categories

### 1. Code debt
| Indicator | Detection | Impact |
|-----------|-----------|--------|
| Duplication | Similar code blocks | Maintenance cost |
| Complexity | Cyclomatic > 10 | Bug risk |
| Long methods | > 50 lines | Readability |
| Deep nesting | > 4 levels | Maintainability |
| Magic numbers | Hardcoded values | Flexibility |
| Dead code | Unused functions | Confusion |

### 2. Architecture debt
| Indicator | Detection | Impact |
|-----------|-----------|--------|
| Circular deps | Import cycles | Coupling |
| God objects | Classes > 500 lines | Modification risk |
| Missing abstractions | Repeated patterns | Inflexibility |
| Tight coupling | Direct dependencies | Testing difficulty |

### 3. Testing debt
| Indicator | Detection | Impact |
|-----------|-----------|--------|
| Low coverage | < 60% lines | Regression risk |
| Flaky tests | Random failures | CI reliability |
| Slow tests | > 5 min suite | Developer velocity |
| Missing types | No integration tests | Integration bugs |

### 4. Documentation debt
| Indicator | Detection | Impact |
|-----------|-----------|--------|
| Missing docs | No README, comments | Onboarding time |
| Outdated docs | Doesn't match code | Confusion |
| No API docs | Missing OpenAPI | Integration difficulty |

### 5. Infrastructure debt
| Indicator | Detection | Impact |
|-----------|-----------|--------|
| Outdated deps | Major versions behind | Security risk |
| No CI/CD | Manual deployments | Release velocity |
| No monitoring | Missing alerts | Incident response |

## Analysis process
1. Scan codebase for indicators
2. Calculate complexity metrics
3. Identify patterns and clusters
4. Estimate remediation effort
5. Calculate ROI for fixes
6. Prioritize by impact/effort

## Prioritization matrix
| ROI | Effort: Low | Effort: Medium | Effort: High |
|-----|-------------|----------------|--------------|
| High | Do now | Plan sprint | Plan quarter |
| Medium | Do soon | Backlog | Evaluate |
| Low | Maybe | Probably not | Don't |

## Output format
### Technical Debt Report: <scope>

#### Summary
| Category | Items | Severity | Estimated Effort |
|----------|-------|----------|------------------|
| Code | <n> | 🔴/🟡/🟢 | <hours> |
| Architecture | <n> | 🔴/🟡/🟢 | <hours> |
| Testing | <n> | 🔴/🟡/🟢 | <hours> |
| Documentation | <n> | 🔴/🟡/🟢 | <hours> |
| Infrastructure | <n> | 🔴/🟡/🟢 | <hours> |

**Total estimated debt**: <hours> hours
**Monthly maintenance tax**: <estimate>

---

#### Critical Items (fix now)
| Item | Location | Impact | Fix |
|------|----------|--------|-----|
| <item> | <file:line> | <impact> | <recommendation> |

#### Quick Wins (< 1 hour each)
| Item | Location | Effort | Impact |
|------|----------|--------|--------|

#### Planned Improvements (1-5 hours)
| Item | Location | Effort | Impact |
|------|----------|--------|--------|

#### Strategic Initiatives (> 5 hours)
| Item | Scope | Effort | Business Case |
|------|-------|--------|---------------|

---

#### Metrics
| Metric | Current | Target | Gap |
|--------|---------|--------|-----|
| Test coverage | <n>% | 80% | <n>% |
| Cyclomatic complexity avg | <n> | < 10 | <n> |
| Dependency age | <months> | < 6mo | <months> |

#### Recommendations
1. **Immediate**: <action>
2. **This sprint**: <action>
3. **This quarter**: <action>
