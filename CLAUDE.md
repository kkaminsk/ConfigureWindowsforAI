# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Documentation-only repository providing guides for configuring **Windows 11 as an AI-powered Administrator Workstation** using Claude Code and OpenSpec. No application code—only markdown documentation and templates.

## Tech Stack

- PowerShell 7 (not Windows PowerShell 5.1)
- Node.js 20.19.0+
- OpenSpec (`@fission-ai/openspec`)
- Markdown documentation

## Key Constraints

- **Windows 11 specific**: All commands and documentation target Windows 11
- **Documentation only**: This repo contains guides and templates, no application code
- **Enterprise focus**: Consider corporate firewall/proxy requirements in documentation

## OpenSpec Workflow

This project uses OpenSpec for spec-driven development. When making documentation changes:

1. **Check existing specs**: `openspec list --specs` and `openspec list`
2. **Create proposals**: For significant changes, create `proposal.md` and `tasks.md` in `openspec/changes/<change-id>/`
3. **Validate**: `openspec validate <change-id> --strict`
4. **Archive after completion**: `openspec archive <change-id> --yes`

See `openspec/AGENTS.md` for full workflow details.

## File Structure

```
openspec/
├── project.md          # Project conventions and context
├── AGENTS.md           # AI assistant instructions for OpenSpec
├── specs/              # Current specifications
└── changes/            # Proposals and archived changes
```

## Style Conventions

- **File naming**: kebab-case for directories and markdown files
- **Commands**: Include shell type (PowerShell) before code blocks
- **Headings**: Use sparingly for visual hierarchy in guides
