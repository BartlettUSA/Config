---
description: OWASP vulnerability assessment and security audit
allowed-tools: Bash, Read, Grep, Glob, Task
model: sonnet
argument-hint: [optional: specific path or --full]
---

# /security-scan — Security vulnerability assessment

You are running the /security-scan workflow.

## Inputs
- $ARGUMENTS: Optional path to scan or `--full` for complete audit

## Hard constraints
- Never expose secrets or credentials in output
- Prioritize findings by severity (Critical > High > Medium > Low)
- Provide actionable remediation for each finding
- Check OWASP Top 10 vulnerabilities

## Scan categories

### 1. Dependency vulnerabilities
```bash
# Node.js
npm audit --json 2>/dev/null || yarn audit --json 2>/dev/null

# Python
pip-audit 2>/dev/null || safety check 2>/dev/null

# Go
go list -json -m all | nancy sleuth 2>/dev/null
```

### 2. Secret detection
Search for patterns:
- API keys: `[A-Za-z0-9_]{20,}`
- AWS keys: `AKIA[0-9A-Z]{16}`
- Private keys: `-----BEGIN.*PRIVATE KEY-----`
- Passwords in code: `password\s*=\s*["'][^"']+["']`
- Tokens: `(token|secret|api_key)\s*[:=]\s*["'][^"']+["']`

### 3. Code vulnerabilities (OWASP Top 10)
| Category | Pattern to detect |
|----------|------------------|
| SQL Injection | Raw SQL with string concatenation |
| XSS | `innerHTML`, `dangerouslySetInnerHTML`, unescaped output |
| Command Injection | `exec()`, `system()`, `shell_exec()` with user input |
| Path Traversal | File operations with user-controlled paths |
| Insecure Deserialization | `pickle.loads()`, `eval()`, `unserialize()` |
| Hardcoded Secrets | Credentials in source code |
| Missing Auth | Endpoints without authentication checks |

### 4. Configuration issues
- Debug mode enabled in production
- CORS allowing all origins (`*`)
- Missing security headers (CSP, HSTS, X-Frame-Options)
- Default credentials
- Exposed .env or config files

## Process
1. Detect project type (package.json, requirements.txt, go.mod, etc.)
2. Run dependency audit for detected ecosystems
3. Scan for hardcoded secrets
4. Check for OWASP Top 10 patterns
5. Review configuration files
6. Generate prioritized report

## Output format
### Security Scan Report

**Scan scope**: <path or "full project">
**Project type**: <detected type>

#### Critical Findings
| File | Line | Issue | Remediation |
|------|------|-------|-------------|

#### High Findings
| File | Line | Issue | Remediation |
|------|------|-------|-------------|

#### Medium Findings
| File | Line | Issue | Remediation |
|------|------|-------|-------------|

#### Dependency Vulnerabilities
| Package | Severity | CVE | Fix Version |
|---------|----------|-----|-------------|

#### Summary
- Critical: <count>
- High: <count>
- Medium: <count>
- Low: <count>

#### Recommended Actions
1. <prioritized action>
2. <prioritized action>
