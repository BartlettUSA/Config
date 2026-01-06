# /commit — Create conventional commit with semantic message

You are running the /commit workflow.

## Inputs
Use the user's message for optional specific files to stage (default: all staged changes).

## Hard constraints
- Follow Conventional Commits specification (feat, fix, docs, style, refactor, test, chore)
- Use appropriate emoji prefix based on commit type
- Keep subject line under 72 characters
- Do NOT amend existing commits unless explicitly requested

## Emoji mapping
| Type | Emoji | Use case |
|------|-------|----------|
| feat | ✨ | New feature |
| fix | 🐛 | Bug fix |
| docs | 📚 | Documentation |
| style | 💄 | Formatting, no code change |
| refactor | ♻️ | Code restructuring |
| test | ✅ | Adding tests |
| chore | 🔧 | Maintenance |
| perf | ⚡ | Performance |
| security | 🔒 | Security fix |
| breaking | 💥 | Breaking change |

## Process
1. Run `git status` to see staged and unstaged changes
2. Run `git diff --cached` to analyze staged changes
3. Determine the primary change type from the diff
4. Generate commit message: `<emoji> <type>(<scope>): <description>`
5. Execute `git commit -m "<message>"`
6. Show the resulting commit with `git log -1 --oneline`

## Output format
```
Staged: <file count> files
Type: <commit type>
Message: <full commit message>
Result: <success/failure>
```
