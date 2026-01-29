# Project Context

## Purpose

This repository provides comprehensive documentation and guidance for configuring **Windows 11 as an AI-powered Administrator Workstation**. The goal is to help enterprise IT administrators and developers set up a productive environment using:

- **Claude Code** - Anthropic's agentic CLI for AI-assisted development and automation
- **OpenSpec** - A spec-driven development framework that enforces planning before implementation

This is a documentation-only repository; no application code will be added.

## Tech Stack

- **PowerShell 7** - Primary terminal and scripting environment
- **Node.js 20.19.0+** - Runtime for OpenSpec
- **Claude Code CLI** - AI assistant interface
- **OpenSpec** - Spec-driven development framework (`@fission-ai/openspec`)
- **Git** - Version control
- **Markdown** - Documentation format

## Project Conventions

### Code Style

- **File naming**: Lowercase with hyphens (kebab-case) for directories and markdown files
- **Documentation**: Use clear, step-by-step instructions with code blocks for commands
- **Command examples**: Include the shell type (PowerShell, Bash) before code blocks
- **Headings**: Use emoji icons sparingly for visual hierarchy in guides

### Architecture Patterns

This project follows the **OpenSpec proposal workflow**:

1. **Proposal Stage** - Create `proposal.md` and `tasks.md` before any implementation
2. **Review Stage** - Get approval before proceeding
3. **Implementation Stage** - Execute tasks following the approved plan
4. **Archive Stage** - Move completed changes to `changes/archive/`

### Testing Strategy

- **Validation**: Use `openspec validate [change-id] --strict` to verify proposals
- **Manual verification**: Test all documented commands on a clean Windows 11 environment
- **Checklist completion**: Ensure all `tasks.md` items are checked before marking complete

### Git Workflow

- **Main branch**: `main` is the primary branch
- **Feature branches**: Create branches for new documentation sections or major updates
- **Commit messages**: Use clear, descriptive messages explaining what changed and why
- **Pull requests**: Required for significant changes; include summary of updates

## Domain Context

**Enterprise IT Administration**: This documentation targets IT professionals who:

- Manage Windows 11 workstations in corporate environments
- Need to configure developer tools while adhering to enterprise policies
- Want to leverage AI assistants for administrative tasks and development
- Require structured, auditable workflows (spec-driven approach)

**Key concepts AI assistants should understand**:

- Windows 11 administrative tasks and PowerShell scripting
- Enterprise software deployment considerations
- Security best practices for AI tool usage in corporate environments
- The OpenSpec workflow: propose first, implement after approval

## Important Constraints

- **Windows 11 only** - All documentation and commands are specific to Windows 11
- **PowerShell 7 required** - Commands assume PowerShell 7, not Windows PowerShell 5.1
- **Enterprise considerations** - Assume potential corporate firewall and proxy requirements
- **Claude subscription required** - Users need Claude Pro/Max or API credits
- **Documentation scope** - This repo contains no application code, only guides and templates

## External Dependencies

- **Claude API** - Requires active Claude Pro/Max subscription or Console API credits
- **npm registry** - For installing OpenSpec (`@fission-ai/openspec`)
- **claude.ai** - Source for Claude Code installer (`https://claude.ai/install.ps1`)
- **GitHub** - For version control and potential collaboration
