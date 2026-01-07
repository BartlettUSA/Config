---
title: "AGENTS"
date: 2026-01-06
type: ref
slug: agents
status: active
tags: [ref, config, ide]
---
# Config Repository Agent Instructions

Cross-platform agent instructions for **Config** (IDE and tool configurations).

## Project Overview

This repository contains portable IDE and tool configurations for cross-machine consistency.

**Purpose:** Configuration management for development tools
**Structure:**
- `claude-code/` - Claude Code commands and settings
- `cursor/` - Cursor IDE commands and rules
- `continue/` - Continue extension configurations
- `vscode/` - VS Code settings and extensions
- `installer/` - Cross-platform install scripts
- `workspaces/` - VS Code workspace files

**Management:** Manual + Chezmoi hybrid (see README.md for details)

## Shared Utilities

Before creating new scripts, check the shared Utilities repository:
- **Location**: P:/dev/repos/Utilities (BartlettUSA/Utilities)
- **Index**: See Utilities/AGENTS.md for full list
- **Categories**: cleanup, deployment, validation, venv, github-api, health-check

Common utilities available:
- `mode-switch.sh` - Switch GitHub branch protection (dev/prod)
- `deploy.sh` - Deploy agent framework to repos
- `cleanup-dev.ps1` - Clean temp files and stale caches
- `health-check.sh` - Validate service endpoints
- `venv-setup.ps1/sh` - Python virtual environment management

**DO NOT recreate these. Import or reference them.**

## Boundaries

### Always
- Follow existing configuration patterns
- Test changes with dry-run modes when available
- Document configuration purposes and dependencies

### Ask First
- Adding new IDE platform configurations
- Modifying installer scripts
- Changing Chezmoi templates

### Never
- Commit secrets or API keys (use templates with env vars)
- Break cross-platform compatibility without discussion
- Modify production configs without backup
