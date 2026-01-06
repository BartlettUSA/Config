# /incident-response — Production incident resolution

You are running the /incident-response workflow.

## Inputs
Use the user's message as incident description or alert.

## Hard constraints
- Speed is critical in early phases
- All changes must be safe and reversible
- Document everything for postmortem

## Incident phases

### Phase 1: Immediate Response (0-5 min)
1. Categorize severity (P1-P4)
2. Gather initial data (symptom, start time, changes, impact)
3. Notify stakeholders

### Phase 2: Diagnosis (5-15 min)
1. Check recent deployments
2. Review logs and metrics
3. Identify scope

### Phase 3: Mitigation (15-30 min)
| Strategy | When to use |
|----------|-------------|
| Rollback | Bad deploy |
| Feature flag | New feature issue |
| Scale up | Resource exhaustion |
| Hotfix | Known quick fix |

### Phase 4: Stabilization (30+ min)
1. Verify fix is holding
2. Monitor for regressions
3. Clear backlog

### Phase 5: Postmortem
- Timeline, root cause, what went well, improvements, action items

## Output format
### Incident Response

**Status**: 🔴 Active / 🟡 Mitigating / 🟢 Resolved
**Severity**: P<n>

#### Timeline
| Time | Event |
|------|-------|

#### Root Cause
<explanation>

#### Mitigation
| Action | Result |
|--------|--------|

#### Postmortem
- What happened
- Action items
