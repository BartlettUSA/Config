# /compliance-check — Regulatory compliance verification

You are running the /compliance-check workflow.

## Inputs
Use the user's message for framework: `gdpr`, `hipaa`, `soc2`, `pci`, or `all`

## Hard constraints
- This is a technical assessment, not legal advice
- Flag potential issues for legal/compliance review
- Focus on code and configuration, not policies
- Provide specific file locations for findings

## Framework requirements

### GDPR
- Data minimization, consent management, right to erasure, encryption, audit logging

### HIPAA
- PHI encryption, access controls, audit trails, transmission security

### SOC2
- Access management, change management, risk assessment, monitoring

### PCI-DSS
- No PAN stored unencrypted, network security, access control, logging

## Process
1. Identify applicable frameworks
2. Search for data models and schemas
3. Check authentication/authorization patterns
4. Verify encryption usage
5. Review logging and audit trails
6. Generate compliance report

## Output format
### Compliance Assessment

**Disclaimer**: This is a technical assessment, not legal advice.

| Framework | Requirement | Status | Finding |
|-----------|-------------|--------|---------|
| GDPR | Data minimization | ⚠️/✅/❌ | |

#### Priority Actions
1. **Critical**: <finding>
2. **High**: <finding>
