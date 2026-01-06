---
description: Dependency security and license compliance check
allowed-tools: Bash, Read, Grep, Glob
model: sonnet
argument-hint: [optional: --security | --license | --outdated]
---

# /deps-audit — Dependency audit and compliance

You are running the /deps-audit workflow.

## Inputs
- $ARGUMENTS: Optional focus area
  - `--security` - Vulnerability scan only
  - `--license` - License compliance only
  - `--outdated` - Outdated packages only
  - (none) - Full audit

## Hard constraints
- Check all detected package managers
- Flag GPL/AGPL licenses in proprietary projects
- Prioritize by exploitability and severity
- Include transitive dependencies

## Supported ecosystems
| Ecosystem | Files | Commands |
|-----------|-------|----------|
| Node.js | package.json, package-lock.json | `npm audit`, `npm outdated` |
| Python | requirements.txt, pyproject.toml | `pip-audit`, `pip list --outdated` |
| Go | go.mod, go.sum | `go list -m -u all` |
| Rust | Cargo.toml, Cargo.lock | `cargo audit`, `cargo outdated` |
| Ruby | Gemfile, Gemfile.lock | `bundle audit`, `bundle outdated` |

## Process

### 1. Detect ecosystems
```bash
ls -la package.json requirements.txt pyproject.toml go.mod Cargo.toml Gemfile 2>/dev/null
```

### 2. Security audit
For each detected ecosystem, run vulnerability scan and parse output.

### 3. License check
Extract licenses and flag:
- **Copyleft**: GPL, AGPL, LGPL (may require source disclosure)
- **Unknown**: Packages without clear license
- **Commercial**: Requires paid license

### 4. Outdated analysis
Categorize by update type:
- **Major**: Breaking changes likely
- **Minor**: New features, backward compatible
- **Patch**: Bug fixes and security patches

### 5. Supply chain risks
- Check for typosquatting (similar package names)
- Flag packages with recent maintainer changes
- Identify packages with low download counts

## Output format
### Dependency Audit Report

**Ecosystems detected**: <list>
**Total dependencies**: <count>
**Direct / Transitive**: <count> / <count>

#### Security Vulnerabilities
| Package | Version | Severity | CVE | Fixed In | Exploitable |
|---------|---------|----------|-----|----------|-------------|

#### License Compliance
| Package | License | Risk | Action Required |
|---------|---------|------|-----------------|

#### Outdated Packages
| Package | Current | Latest | Type | Priority |
|---------|---------|--------|------|----------|

#### Supply Chain Risks
| Package | Risk Type | Details |
|---------|-----------|---------|

#### Remediation Script
```bash
# Auto-fix commands
<package manager commands>
```

#### Summary
- Vulnerabilities: <critical>/<high>/<medium>/<low>
- License issues: <count>
- Outdated: <major>/<minor>/<patch>
