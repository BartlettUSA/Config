# /deps-audit — Dependency security and license compliance

You are running the /deps-audit workflow.

## Inputs
Use the user's message for optional focus:
- `--security` - Vulnerability scan only
- `--license` - License compliance only
- `--outdated` - Outdated packages only

## Hard constraints
- Check all detected package managers
- Flag GPL/AGPL licenses in proprietary projects
- Prioritize by exploitability and severity
- Include transitive dependencies

## Supported ecosystems
| Ecosystem | Files | Commands |
|-----------|-------|----------|
| Node.js | package.json | `npm audit`, `npm outdated` |
| Python | requirements.txt | `pip-audit`, `pip list --outdated` |
| Go | go.mod | `go list -m -u all` |
| Rust | Cargo.toml | `cargo audit` |

## Process
1. Detect ecosystems from config files
2. Run security audit for each
3. Check license compliance
4. Identify outdated packages
5. Flag supply chain risks (typosquatting, maintainer changes)

## Output format
### Dependency Audit Report

#### Security Vulnerabilities
| Package | Severity | CVE | Fix Version |
|---------|----------|-----|-------------|

#### License Compliance
| Package | License | Risk |
|---------|---------|------|

#### Outdated Packages
| Package | Current | Latest | Type |
|---------|---------|--------|------|

#### Remediation
```bash
<fix commands>
```
