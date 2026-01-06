---
description: Production issue resolution and postmortem
allowed-tools: Bash, Read, Write, Edit, Grep, Glob, Task, WebFetch
model: sonnet
argument-hint: <incident description or alert>
---

# /incident-response — Production incident resolution

You are running the /incident-response workflow.

## Inputs
- $ARGUMENTS: Incident description, error, or monitoring alert

## Hard constraints
- Speed is critical in early phases
- All changes must be safe and reversible
- Document everything for postmortem
- Don't make the situation worse

## Incident phases

### Phase 1: Immediate Response (0-5 min)
**Goal**: Assess severity and impact

1. **Categorize severity**
   | Level | Impact | Response |
   |-------|--------|----------|
   | P1 | Service down | All hands |
   | P2 | Major degradation | On-call + backup |
   | P3 | Minor impact | On-call |
   | P4 | No user impact | Normal priority |

2. **Gather initial data**
   - What's the symptom?
   - When did it start?
   - What changed recently?
   - Who's affected?

3. **Notify stakeholders**
   ```
   Incident: <summary>
   Severity: P<n>
   Impact: <description>
   Status: Investigating
   ```

### Phase 2: Diagnosis (5-15 min)
**Goal**: Identify root cause

1. **Check recent deployments**
   ```bash
   git log --oneline -10
   # Check CI/CD for recent deploys
   ```

2. **Review logs and metrics**
   - Error logs
   - Performance metrics
   - Resource utilization
   - Request patterns

3. **Identify scope**
   - Which services affected?
   - Which regions/users?
   - Is it spreading?

### Phase 3: Mitigation (15-30 min)
**Goal**: Restore service

| Strategy | When to use |
|----------|-------------|
| Rollback | Bad deploy identified |
| Feature flag | New feature causing issue |
| Scale up | Resource exhaustion |
| Failover | Infrastructure failure |
| Hotfix | Known quick fix |

```bash
# Example rollback
git revert <commit> --no-edit
# or deploy previous version
```

### Phase 4: Stabilization (30+ min)
**Goal**: Ensure stability

1. Verify fix is holding
2. Monitor for regressions
3. Clear any backlog/queue
4. Confirm all systems nominal

### Phase 5: Postmortem
**Goal**: Prevent recurrence

Document:
- Timeline of events
- Root cause analysis
- What went well
- What could improve
- Action items

## Output format
### Incident Response: <incident>

#### Status: 🔴 Active / 🟡 Mitigating / 🟢 Resolved

#### Severity: P<n>
**Impact**: <user/business impact>
**Duration**: <start> - <end/ongoing>

---

#### Timeline
| Time | Event |
|------|-------|
| HH:MM | <event> |

#### Root Cause
<explanation of what caused the incident>

#### Mitigation Applied
| Action | Result |
|--------|--------|
| <action> | <outcome> |

#### Current Status
- Services: <status>
- Affected users: <count/description>
- Monitoring: <what to watch>

#### Verification
```
<commands to verify resolution>
```

---

### Postmortem (after resolution)

#### What happened
<summary>

#### Root cause
<technical details>

#### What went well
- <positive>

#### What could improve
- <improvement>

#### Action items
| Action | Owner | Due |
|--------|-------|-----|
| <action> | <person> | <date> |
