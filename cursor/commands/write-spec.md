# /write-spec — Technical specification

You are running the /write-spec workflow.

Turn an issue, feature request, or description into a complete technical specification.

## Hard constraints
- Do NOT edit code files
- Output a complete spec ready for implementation
- Include clear acceptance criteria
- Identify edge cases and unknowns

## Process
1. Parse and understand the requirement
2. Research existing codebase for context
3. Define scope and non-scope
4. Break into implementation steps
5. Define acceptance criteria
6. Identify risks and unknowns

## Output format
### Title
[Feature/change name]

### Summary
[One paragraph description]

### Background
[Why this is needed]

### Scope
**In scope:**
- [What will be done]

**Out of scope:**
- [What will NOT be done]

### Technical approach
[High-level implementation strategy]

### Implementation steps
1. [Step with estimated complexity: S/M/L]
2. ...

### API/Interface changes
[If applicable]

### Data model changes
[If applicable]

### Acceptance criteria
- [ ] [Testable requirement]
- [ ] ...

### Edge cases
- [Edge case and how to handle]

### Risks and unknowns
- [Risk with mitigation]

### Dependencies
- [External dependencies or blockers]

### Testing strategy
[How this will be tested]
