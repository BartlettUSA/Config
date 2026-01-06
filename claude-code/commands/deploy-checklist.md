---
description: Pre-deployment verification and rollback planning
allowed-tools: Bash, Read, Grep, Glob
model: sonnet
argument-hint: <environment: staging|production> [--skip-tests]
---

# /deploy-checklist — Pre-deployment verification

You are running the /deploy-checklist workflow.

## Inputs
- $ARGUMENTS: Target environment
  - `staging` - Staging environment checks
  - `production` - Full production checklist
  - `--skip-tests` - Skip test execution (not recommended)

## Hard constraints
- All checks must pass before production deploy
- Document rollback procedure before deploying
- Verify monitoring is in place
- Never deploy on Fridays without approval

## Pre-deployment checklist

### 1. Code quality ✅
| Check | Command | Required |
|-------|---------|----------|
| Tests pass | `npm test` / `pytest` | Yes |
| Linting clean | `npm run lint` | Yes |
| Type check | `npm run typecheck` | Yes |
| Build succeeds | `npm run build` | Yes |

### 2. Security ✅
| Check | Verification |
|-------|--------------|
| No secrets in code | Grep for API keys, passwords |
| Dependencies audited | `npm audit` / `pip-audit` |
| Security headers | CSP, HSTS, X-Frame-Options |
| HTTPS enforced | Check redirect config |

### 3. Database ✅
| Check | Verification |
|-------|--------------|
| Migrations ready | All migrations committed |
| Backwards compatible | Old code can run with new schema |
| Backup verified | Recent backup exists |
| Rollback script | Migration down works |

### 4. Configuration ✅
| Check | Verification |
|-------|--------------|
| Env vars set | All required vars in target env |
| Feature flags | Correct state for environment |
| API endpoints | Pointing to correct services |
| Logging level | Appropriate for environment |

### 5. Monitoring ✅
| Check | Verification |
|-------|--------------|
| Health endpoint | `/health` returns 200 |
| Metrics exposed | Prometheus/StatsD configured |
| Alerts configured | PagerDuty/Slack integration |
| Dashboards ready | Grafana/Datadog dashboards |

### 6. Documentation ✅
| Check | Verification |
|-------|--------------|
| Changelog updated | Changes documented |
| Runbook current | Deployment steps accurate |
| API docs updated | OpenAPI spec current |

## Rollback procedure
```markdown
## Rollback Steps
1. Identify the issue and confirm rollback needed
2. Run: `<rollback command>`
3. Verify rollback: `<verification command>`
4. Notify team in #deployments
5. Create incident ticket if needed

## Previous version
- Tag: <previous-tag>
- Commit: <previous-commit>
- Deployed: <timestamp>
```

## Process
1. Detect environment from $ARGUMENTS
2. Run all applicable checks
3. Generate checklist report
4. If any critical check fails, STOP
5. Prepare rollback documentation
6. Generate deploy command

## Output format
### Deployment Checklist: <environment>

#### Pre-flight Checks
| Category | Status | Details |
|----------|--------|---------|
| Code quality | ✅/❌ | <summary> |
| Security | ✅/❌ | <summary> |
| Database | ✅/❌ | <summary> |
| Configuration | ✅/❌ | <summary> |
| Monitoring | ✅/❌ | <summary> |
| Documentation | ✅/❌ | <summary> |

#### Blocking Issues
<list if any>

#### Warnings
<list if any>

#### Rollback Plan
```bash
<rollback commands>
```

#### Deploy Command
```bash
<deploy command>
```

#### Ready to deploy: ✅/❌
