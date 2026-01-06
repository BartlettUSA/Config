# /git-workflow — Manage branching, commits, and merge strategy

You are running the /git-workflow workflow.

## Inputs
Use the user's message as the action:
- `status` - Full repo status with branch info
- `branch <name>` - Create feature branch
- `merge <branch>` - Merge branch with strategy
- `rebase` - Rebase current branch on main
- `sync` - Sync fork with upstream
- `cleanup` - Delete merged branches

## Hard constraints
- Never force push to main/master
- Always fetch before branch operations
- Use merge commits for feature branches
- Use rebase for keeping feature branches updated

## Actions

### status
Show git status, recent commits, and branch info.

### branch <name>
1. Fetch latest: `git fetch origin`
2. Checkout base: `git checkout main && git pull`
3. Create branch: `git checkout -b <type>/<name>`
4. Push with tracking: `git push -u origin <type>/<name>`

### merge <branch>
1. Checkout target: `git checkout main && git pull`
2. Merge with message: `git merge --no-ff <branch>`
3. Push: `git push origin main`

### rebase
1. Fetch: `git fetch origin`
2. Rebase: `git rebase origin/main`
3. If conflicts: list them and pause

### sync (for forks)
1. Fetch upstream: `git fetch upstream`
2. Merge upstream: `git merge upstream/main`
3. Push to origin: `git push origin main`

### cleanup
1. Fetch and prune: `git fetch -p`
2. Delete merged branches: `git branch --merged main`
3. Prune remote: `git remote prune origin`
