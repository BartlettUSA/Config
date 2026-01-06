---
description: Version bump, changelog, and release management
allowed-tools: Bash, Read, Write, Edit, Grep
model: sonnet
argument-hint: <version: patch|minor|major|x.y.z>
---

# /release — Release management workflow

You are running the /release workflow.

## Inputs
- $ARGUMENTS: Version increment or specific version
  - `patch` - Bug fixes (1.0.0 → 1.0.1)
  - `minor` - New features (1.0.0 → 1.1.0)
  - `major` - Breaking changes (1.0.0 → 2.0.0)
  - `x.y.z` - Specific version number

## Hard constraints
- Follow semantic versioning (semver)
- Update CHANGELOG.md with all changes
- Tag release in git
- Do NOT publish without confirmation

## Semantic versioning rules
| Change type | Version bump | Example |
|-------------|--------------|---------|
| Breaking API change | Major | 1.x.x → 2.0.0 |
| New feature (backward compatible) | Minor | 1.0.x → 1.1.0 |
| Bug fix | Patch | 1.0.0 → 1.0.1 |
| Pre-release | Append suffix | 1.0.0-beta.1 |

## Process

### 1. Determine version
```bash
# Get current version
cat package.json | grep '"version"' || cat setup.py | grep 'version=' || cat Cargo.toml | grep '^version'

# Calculate new version based on $ARGUMENTS
```

### 2. Generate changelog
```bash
# Get commits since last tag
git log $(git describe --tags --abbrev=0)..HEAD --oneline
```

Group commits by type:
- **Features**: `feat:` commits
- **Bug Fixes**: `fix:` commits
- **Breaking Changes**: commits with `BREAKING CHANGE`
- **Other**: remaining commits

### 3. Update version files
| Ecosystem | File | Update |
|-----------|------|--------|
| Node.js | package.json | `"version": "x.y.z"` |
| Python | pyproject.toml | `version = "x.y.z"` |
| Rust | Cargo.toml | `version = "x.y.z"` |

### 4. Update CHANGELOG.md
```markdown
## [x.y.z] - YYYY-MM-DD

### Added
- New feature description (#PR)

### Changed
- Change description (#PR)

### Fixed
- Bug fix description (#PR)

### Breaking Changes
- Breaking change description (#PR)
```

### 5. Create release commit and tag
```bash
git add -A
git commit -m "chore(release): x.y.z"
git tag -a vx.y.z -m "Release x.y.z"
```

### 6. Push and create GitHub release
```bash
git push origin main --tags
gh release create vx.y.z --title "vx.y.z" --notes-file RELEASE_NOTES.md
```

## Output format
### Release: v<version>

#### Version Change
| Previous | New | Type |
|----------|-----|------|
| <old> | <new> | <patch/minor/major> |

#### Changelog
```markdown
<generated changelog>
```

#### Files Updated
- package.json (or equivalent)
- CHANGELOG.md

#### Git Commands
```bash
git add -A
git commit -m "chore(release): <version>"
git tag -a v<version> -m "Release <version>"
git push origin main --tags
```

#### GitHub Release
```bash
gh release create v<version> --title "v<version>" --notes-file CHANGELOG.md
```

**Ready to release?** Run the git commands above to complete.
