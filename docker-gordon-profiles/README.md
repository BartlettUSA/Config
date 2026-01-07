# Gordon MCP Profiles

Task-specific MCP configurations for Docker Desktop's Gordon AI assistant.

## Problem Solved

Gordon shows "You have too many tools in your request" when the MCP Gateway loads all 226+ tools from 15+ servers. This overwhelms the LLM context window.

## Solution

Use task-specific `gordon-mcp.yml` files that load only needed servers.

## Available Profiles

| Profile | File | Tools | Use Case |
|---------|------|-------|----------|
| **Minimal** | `gordon-mcp-minimal.yml` | ~5 | Basic queries, time, fetch |
| **Docker Ops** | `gordon-mcp-docker-ops.yml` | ~15 | Container/image management |
| **Research** | `gordon-mcp-research.yml` | ~25 | Web search, documentation |
| **GitHub** | `gordon-mcp-github.yml` | ~60 | Repository, PRs, issues |

## Usage

1. Copy the appropriate profile to your working directory:
   ```powershell
   Copy-Item "P:\dev\repos\Config\docker-gordon-profiles\gordon-mcp-docker-ops.yml" ".\gordon-mcp.yml"
   ```

2. Gordon will automatically use the `gordon-mcp.yml` in your current directory

3. Ask Gordon your question - it will only have access to the profiled tools

## Creating Custom Profiles

```yaml
# gordon-mcp.yml - Custom profile example
services:
  # Only include servers you need
  docker-hub:
    image: mcp/docker

  filesystem:
    image: mcp/filesystem
    command:
      - /workspace
    volumes:
      - ${PWD}:/workspace:ro
```

## Tool Count Reference

| Server | Approx Tools |
|--------|--------------|
| docker | 13 |
| github | 56 |
| git | 11 |
| filesystem | 8 |
| fetch | 2 |
| duckduckgo | 1 |
| wikipedia | 10 |
| context7 | 2 |
| time | 1 |
| obsidian | 13 |
| chroma | 13 |
| playwright | 25 |
| desktop-commander | 30 |
| perplexity | 3 |
| memory | 8 |

## Recommended Limits

- **Safe:** < 50 tools
- **Caution:** 50-100 tools
- **Overload:** > 100 tools (will likely fail)

## Alternative: Docker Desktop GUI

You can also manage enabled servers via:
1. Docker Desktop → Settings → Extensions → MCP Toolkit
2. Disable servers you don't need
3. This affects all Gordon sessions globally

The `gordon-mcp.yml` approach is preferred for project-specific needs.
