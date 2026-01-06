# /release — Version bump and changelog

You are running the /release workflow.

## Inputs
Use the user's message as version:
- `patch` - Bug fixes (1.0.0 → 1.0.1)
- `minor` - New features (1.0.0 → 1.1.0)
- `major` - Breaking changes (1.0.0 → 2.0.0)
- `x.y.z` - Specific version

## Hard constraints
- Follow semantic versioning
- Update CHANGELOG.md with all changes
- Tag release in git
- Do NOT publish without confirmation

## Process

### 1. Determine version
Get current version from package.json/pyproject.toml/Cargo.toml

### 2. Generate changelog
Group commits since last tag by type:
- **Features**: `feat:` commits
- **Bug Fixes**: `fix:` commits
- **Breaking Changes**: `BREAKING CHANGE`

### 3. Update version files
Update version in appropriate config files

### 4. Update CHANGELOG.md
```markdown
## [x.y.z] - YYYY-MM-DD

### Added
- Feature (#PR)

### Fixed
- Bug fix (#PR)
```

### 5. Create release commit and tag
```bash
git commit -m "chore(release): x.y.z"
git tag -a vx.y.z -m "Release x.y.z"
```

## Output format
### Release: v<version>

| Previous | New | Type |
|----------|-----|------|
| <old> | <new> | <type> |

#### Changelog
```markdown
<generated>
```

#### Commands
```bash
git push origin main --tags
gh release create v<version>
```
