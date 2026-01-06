---
description: Manage branching, commits, and merge strategy
allowed-tools: Bash, Read
model: sonnet
argument-hint: <action: status|branch|merge|rebase|sync>
---

# /git-workflow — Git workflow management

You are running the /git-workflow workflow.

## Inputs
- $ARGUMENTS: Action to perform
  - `status` - Full repo status with branch info
  - `branch <name>` - Create feature branch
  - `merge <branch>` - Merge branch with strategy
  - `rebase` - Rebase current branch on main
  - `sync` - Sync fork with upstream
  - `cleanup` - Delete merged branches

## Hard constraints
- Never force push to main/master
- Always fetch before branch operations
- Use merge commits for feature branches (preserve history)
- Use rebase for keeping feature branches updated

## Actions

### status
```bash
git fetch --all
git status
git log --oneline -5
git branch -vv
```

### branch <name>
1. Fetch latest: `git fetch origin`
2. Checkout base: `git checkout main && git pull`
3. Create branch: `git checkout -b <type>/<name>`
4. Push with tracking: `git push -u origin <type>/<name>`

### merge <branch>
1. Checkout target: `git checkout main && git pull`
2. Merge with message: `git merge --no-ff <branch> -m "Merge <branch>"`
3. Push: `git push origin main`

### rebase
1. Fetch: `git fetch origin`
2. Rebase: `git rebase origin/main`
3. If conflicts: list them and pause for resolution
4. After resolution: `git rebase --continue`

### sync (for forks)
1. Fetch upstream: `git fetch upstream`
2. Checkout main: `git checkout main`
3. Merge upstream: `git merge upstream/main`
4. Push to origin: `git push origin main`

### cleanup
1. Fetch and prune: `git fetch -p`
2. List merged: `git branch --merged main | grep -v main`
3. Delete each: `git branch -d <branch>`
4. Prune remote: `git remote prune origin`

## Output format
```
Action: <action>
Branch: <current-branch>
Status: <result>
Next steps: <recommendations>
```
