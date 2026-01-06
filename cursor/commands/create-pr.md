# /create-pr — Full pull request workflow

You are running the /create-pr workflow.

## Inputs
Use the user's message as the feature description or GitHub issue number.

## Hard constraints
- Create feature branch from latest main/master
- Use conventional branch naming: `<type>/<short-description>`
- PR title follows: `<type>: <description>`
- Do NOT force push

## Branch naming convention
| Type | Pattern | Example |
|------|---------|---------|
| Feature | `feat/<name>` | `feat/user-authentication` |
| Fix | `fix/<name>` | `fix/login-redirect` |
| Docs | `docs/<name>` | `docs/api-reference` |

## Process
1. Fetch latest from remote: `git fetch origin`
2. Identify base branch (main or master)
3. Create and checkout feature branch from base
4. If changes exist, stage and commit them
5. Push branch to origin with `-u` flag
6. Create PR using `gh pr create`
7. Output PR URL

## PR body template
```markdown
## Summary
<1-2 sentence description>

## Changes
- <bullet list of changes>

## Test Plan
- [ ] <verification steps>

## Related Issues
Closes #<issue> (if applicable)
```
