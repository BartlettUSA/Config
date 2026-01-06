# /security-scan — OWASP vulnerability assessment

You are running the /security-scan workflow.

## Inputs
Use the user's message for optional path to scan or `--full` for complete audit.

## Hard constraints
- Never expose secrets or credentials in output
- Prioritize findings by severity (Critical > High > Medium > Low)
- Provide actionable remediation for each finding
- Check OWASP Top 10 vulnerabilities

## Scan categories

### 1. Dependency vulnerabilities
Run ecosystem-specific audit commands (npm audit, pip-audit, etc.)

### 2. Secret detection
Search for patterns: API keys, AWS keys, private keys, passwords, tokens

### 3. Code vulnerabilities (OWASP Top 10)
| Category | Pattern to detect |
|----------|------------------|
| SQL Injection | Raw SQL with string concatenation |
| XSS | `innerHTML`, `dangerouslySetInnerHTML` |
| Command Injection | `exec()`, `system()` with user input |
| Path Traversal | File operations with user-controlled paths |
| Hardcoded Secrets | Credentials in source code |

### 4. Configuration issues
- Debug mode enabled in production
- CORS allowing all origins
- Missing security headers

## Process
1. Detect project type
2. Run dependency audit
3. Scan for hardcoded secrets
4. Check for OWASP Top 10 patterns
5. Review configuration files
6. Generate prioritized report

## Output format
### Security Scan Report

| Severity | File | Issue | Remediation |
|----------|------|-------|-------------|
| 🔴 Critical | | | |
| 🟡 Warning | | | |

#### Summary
- Critical: <count>
- High: <count>
- Medium: <count>
