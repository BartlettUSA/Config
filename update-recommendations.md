# Config Installer Template Update Recommendations

Generated: 2026-01-06  
**Context**: Recommendations for aligning `P:\dev\repos\Config\installer\templates\` with working runtime configs.

**Important**: These templates are **reference designs** for portable deployment. The active deployment mechanism is `P:\dev\repos\Dotfiles` via Chezmoi.

---

## Priority 1: Critical Schema Fixes

### 1.1 Claude Code Settings Schema
**File**: `installer/templates/claude/settings.json`

**Issue**: Template uses outdated schema  
**Current**: `permissions.allow/deny`  
**Required**: `permissions.allowedTools/deniedTools`

**Action**: Update template to match Claude Code current schema (as seen in runtime).

---

### 1.2 Zed Settings Schema  
**File**: `installer/templates/zed/settings.json`

**Issue**: Template uses wrong key and structure  
**Current**: `mcpServers` with flat `command/args`  
**Required**: `context_servers` with nested `command.path/command.args`

**Action**: Update to Zed-specific schema.

---

## Priority 2: Add Missing Templates

### 2.1 Cursor CLI Config
**Action**: Create `installer/templates/cursor/cli-config.json`  
**Source**: Copy from `C:\Users\lance\.cursor\cli-config.json` (871 bytes)  
**Purpose**: Hard-deny list for destructive shell commands

### 2.2 Gemini Instructions
**Action**: Create `installer/templates/gemini/instructions.md`  
**Source**: Copy from `C:\Users\lance\.gemini\instructions.md` (637 bytes)  
**Purpose**: Agent instruction markdown

---

## Priority 3: MCP Server Coverage

Runtime configs include servers missing from templates:

**Add to all platform templates**:
- `auth0` (OAuth flows)
- `figma` (Infisical-wrapped)
- `ms-learn-docs` (Microsoft docs)
- `hugging-face` (ML models)
- `skills` (local server — use `{{SKILLS_SERVER_PATH}}` placeholder)
- `obsidian` (vault access)
- `firecrawl` (Infisical-wrapped)

**Infisical Wrapper Pattern**:
```json
{
  "figma": {
    "command": "infisical",
    "args": [
      "run",
      "--projectId={{INFISICAL_PROJECT_ID}}",
      "--env={{INFISICAL_ENV}}",
      "--path=/",
      "--silent",
      "--log-level=error",
      "--",
      "npx",
      "-y",
      "figma-mcp"
    ]
  }
}
```

---

## Priority 4: Platform-Specific Variations

### Claude Desktop Hooks
Add to `installer/templates/claude-desktop/claude_desktop_config.json`:

```json
{
  "hooks": {
    "PostToolUse": [{
      "matcher": "Edit|Write",
      "hooks": [{
        "type": "command",
        "command": "{{LINT_COMMAND}}"
      }]
    }]
  }
}
```

### LM Studio HTTP Schema
Update `installer/templates/lmstudio/mcp.json` to use `url` property for HTTP endpoints (not `command/args`).

---

## Not Recommended

**Do not update**:
- Runtime configs in `C:\Users\lance` (working and protected)
- Dotfiles Chezmoi templates (managed separately, 42 commits)

**These recommendations apply only to Config/installer templates** for portable deployment reference.

