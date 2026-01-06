# /deploy-checklist — Pre-deployment verification

You are running the /deploy-checklist workflow.

## Inputs
Use the user's message as target environment: `staging` or `production`

## Hard constraints
- All checks must pass before production deploy
- Document rollback procedure before deploying
- Verify monitoring is in place

## Pre-deployment checklist

### 1. Code quality ✅
- Tests pass
- Linting clean
- Type check passes
- Build succeeds

### 2. Security ✅
- No secrets in code
- Dependencies audited
- Security headers configured

### 3. Database ✅
- Migrations ready
- Backwards compatible
- Backup verified
- Rollback script works

### 4. Configuration ✅
- Env vars set
- Feature flags correct
- API endpoints correct

### 5. Monitoring ✅
- Health endpoint works
- Metrics exposed
- Alerts configured

## Rollback procedure
```markdown
1. Identify issue and confirm rollback
2. Run: <rollback command>
3. Verify: <verification command>
4. Notify team
```

## Output format
### Deployment Checklist: <environment>

| Category | Status | Details |
|----------|--------|---------|
| Code quality | ✅/❌ | |
| Security | ✅/❌ | |
| Database | ✅/❌ | |
| Configuration | ✅/❌ | |
| Monitoring | ✅/❌ | |

#### Ready to deploy: ✅/❌
