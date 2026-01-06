---
description: Regulatory compliance verification (GDPR, HIPAA, SOC2, PCI-DSS)
allowed-tools: Read, Grep, Glob, Task
model: sonnet
argument-hint: <framework: gdpr|hipaa|soc2|pci|all>
---

# /compliance-check — Regulatory compliance verification

You are running the /compliance-check workflow.

## Inputs
- $ARGUMENTS: Compliance framework to check
  - `gdpr` - EU data protection
  - `hipaa` - Healthcare data (US)
  - `soc2` - Service organization controls
  - `pci` - Payment card industry
  - `all` - Check all frameworks

## Hard constraints
- This is a technical assessment, not legal advice
- Flag potential issues for legal/compliance review
- Focus on code and configuration, not policies
- Provide specific file locations for findings

## Framework requirements

### GDPR (General Data Protection Regulation)
| Requirement | What to check |
|-------------|---------------|
| Data minimization | Collect only necessary fields |
| Consent management | Explicit consent before data collection |
| Right to erasure | User data deletion capability |
| Data portability | Export user data feature |
| Encryption | Data encrypted at rest and transit |
| Audit logging | Track data access and modifications |

### HIPAA (Health Insurance Portability)
| Requirement | What to check |
|-------------|---------------|
| PHI encryption | All health data encrypted |
| Access controls | Role-based access to PHI |
| Audit trails | Comprehensive access logging |
| Transmission security | TLS for all PHI transfers |
| Automatic logoff | Session timeout implementation |

### SOC2 (Service Organization Control)
| Requirement | What to check |
|-------------|---------------|
| Access management | Authentication and authorization |
| Change management | Version control, code review |
| Risk assessment | Error handling, input validation |
| Monitoring | Logging, alerting, metrics |
| Incident response | Error handling, notification |

### PCI-DSS (Payment Card Industry)
| Requirement | What to check |
|-------------|---------------|
| Cardholder data | No PAN stored unencrypted |
| Network security | Firewall rules, segmentation |
| Access control | Least privilege, MFA |
| Encryption | Strong cryptography (AES-256) |
| Logging | Track all access to cardholder data |

## Process
1. Identify applicable frameworks from $ARGUMENTS
2. Search for data models and schemas
3. Check authentication/authorization patterns
4. Verify encryption usage
5. Review logging and audit trails
6. Check for sensitive data handling
7. Generate compliance report

## Output format
### Compliance Assessment Report

**Frameworks evaluated**: <list>
**Disclaimer**: This is a technical assessment, not legal advice.

#### GDPR Compliance
| Requirement | Status | Finding | Location | Remediation |
|-------------|--------|---------|----------|-------------|
| Data minimization | ⚠️/✅/❌ | | | |

#### [Additional frameworks...]

#### Summary by Framework
| Framework | Compliant | Warnings | Non-Compliant |
|-----------|-----------|----------|---------------|

#### Priority Actions
1. **Critical**: <finding requiring immediate attention>
2. **High**: <significant compliance gap>
3. **Medium**: <improvement recommended>

#### Recommended Reviews
- [ ] Legal review of consent flows
- [ ] Security team review of encryption
- [ ] Privacy impact assessment
