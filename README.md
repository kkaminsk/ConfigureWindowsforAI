# Configure Windows 11 as an AI-Powered Administrator Workstation

This guide walks you through setting up a Windows 11 machine with **Claude Code** and **OpenSpec** to create an AI-powered development environment where you design features before the AI writes a single line of code.

## Overview

| Tool | Purpose |
|------|---------|
| **Claude Code** | Anthropic's agentic CLI for AI-assisted development |
| **OpenSpec** | Spec-driven framework that enforces planning before coding |

---

## Prerequisites

Before you start, ensure you have:

- **Account**: An active Claude Pro/Max subscription or Claude Console API credits
- **Account** (optional): An active GitHub Copilot subscription is nice to have
- **OS**: Windows 11

---

## Part 1: Installation

### Step 1: Install Prerequisites via winget

Open PowerShell and run:

```powershell
winget install Microsoft.VisualStudioCode
winget install Microsoft.PowerShell
winget install OpenJS.NodeJS
```

Restart your terminal after installation to ensure the new tools are available in your PATH.

### Step 2: Install Claude Code

```powershell
winget install Anthropic.ClaudeCode
```

### Step 3: Install OpenSpec

OpenSpec is a Node package, so install it via npm:

```powershell
npm install -g @fission-ai/openspec@latest
```

Verify the installation:

```powershell
openspec --version
```

---

## Part 2: Project Setup

### Step 4: Initialize Your Project

Navigate to your project folder and initialize OpenSpec:

```powershell
cd my-project-folder
openspec init
```

When prompted:
- Select **Claude Code** as your AI assistant
- OpenSpec will configure slash commands (like `/openspec`) automatically

### Step 5: Authenticate Claude

Launch Claude and complete the login process:

```powershell
claude
```

---

## Part 3: Spec-Driven Development Workflow

Now that you're set up, your workflow changes from "chatting" to **spec-driven engineering**. Here's a complete walkthrough.

### Step 6: Create an Application Specification

Start by creating a specification. You can write it by hand or ask Claude to create one:

```
Make me a powershell script that does a Hello World prompt and then exits. Document the specification in a file called `spec.md`.
```

### Step 7: Clarify the Specification

Ask Claude to analyze your specification and identify areas that need clarification:

```
Read the spec.md and ask questions to clarify requirements. Put these questions in a file called `questions.md`.
```

### Step 8: Refine Based on Questions

Use the generated questions to improve your specification:

```
Read the questions.md and use them to clarify the specification in spec.md.
```

### Step 9: Update Project Context

Sync your specification with the OpenSpec project context:

```
Read the spec.md and update the project.md file with the specification.
```

---

## Part 4: Using OpenSpec Proposals

Once your specification is ready, use OpenSpec's proposal workflow to plan implementation.

### Step 10: Create the Proposals

Instead of asking Claude to "write code," use the slash command to create a structured proposal:

```
/openspec:proposal read the spec.md and create a series of tasks to implement the specification. Number the tasks sequentially in order of implementation.
```

Claude will generate:
- `proposal.md` - The what and why of the change
- `tasks.md` - Implementation checklist

### Step 11: Review the Proposal

Check the generated spec files in the `openspec/changes/` directory. Ensure:
- Tasks are in logical order
- Requirements are complete
- No ambiguity remains

### Step 12: Initialize Claude Code

Before applying proposals, initialize Claude Code to work with your project. The `/init` command analyzes your codebase and generates a `CLAUDE.md` file that serves as Claude's persistent memory across sessions.

```powershell
claude
```

Then inside Claude:

```
/init
```

**What `/init` does:**

- **Scans your project** to detect build systems, test frameworks, and code patterns
- **Creates a `CLAUDE.md` file** at your project root with project-specific instructions
- **Establishes context** so Claude understands your project's conventions

**The generated `CLAUDE.md` contains:**

- Build and test commands Claude can't infer on its own
- Code style rules specific to your project
- Repository etiquette (branch naming, PR conventions)
- Architectural decisions and common gotchas

Review and refine the generated file, then commit it to git so your team benefits from shared context.

### Step 13: Apply the Proposal

Tell Claude to execute it:

```
/openspec:apply the next proposal
```

---

## Quick Reference

| Command | Purpose |
|---------|---------|
| `claude` | Start Claude Code CLI |
| `/init` | Generate CLAUDE.md with project context |
| `openspec init` | Initialize OpenSpec in a project |
| `openspec --version` | Check OpenSpec version |
| `/openspec:proposal <description>` | Create a new proposal |
| `/openspec:apply` | Apply an approved proposal |
| `openspec validate <change-id> --strict` | Validate a proposal |

---

## File Structure

After setup, your project will have:

```
my-project/
├── CLAUDE.md               # Claude Code project memory (created by /init)
├── openspec/
│   ├── project.md          # Project context and conventions
│   ├── AGENTS.md           # AI assistant instructions
│   ├── specs/              # Current specifications
│   └── changes/            # Proposals and archived changes
├── spec.md                 # Your application specification
└── questions.md            # Clarification questions
```

---

## Next Steps

- Review `openspec/project.md` and customize it for your project
- Read `openspec/AGENTS.md` to understand how AI assistants interact with specs
- Create your first real specification and proposal

---

## Troubleshooting

**Claude command not found**: Restart your terminal after installing via winget.

**npm command not found**: Ensure Node.js is installed and restart your terminal.

**OpenSpec init fails**: Make sure you're running the command inside a git repository.

---

## Appendix A: Reduce Prompting with settings.local.json

By default, Claude Code prompts for permission before running shell commands. To streamline your workflow, you can install a settings file that pre-approves common operations.

### Installation

Copy the example settings file to your Claude configuration directory:

```powershell
# Create the .claude directory if it doesn't exist
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude" -Force

# Copy the settings file
Copy-Item "ExampleClaudeConfig\settings.local.json" "$env:USERPROFILE\.claude\settings.local.json"
```

### What This Enables

The provided `settings.local.json` contains:

```json
{
  "permissions": {
    "allow": [
      "Bash(*)"
    ],
    "deny": [],
    "ask": []
  }
}
```

This configuration:
- **Allows all Bash commands** without prompting
- Eliminates confirmation dialogs for shell operations
- Speeds up workflows where you trust Claude's command execution

### Security Considerations

⚠️ **Only use this setting on development machines where you trust Claude's operations.** This grants Claude permission to run any shell command without asking. For production or sensitive environments, consider using more restrictive permissions.

### Customization

You can modify the `allow` array to be more specific:

```json
{
  "permissions": {
    "allow": [
      "Bash(git *)",
      "Bash(npm *)",
      "Bash(openspec *)"
    ],
    "deny": [],
    "ask": []
  }
}
```

This restricts auto-approval to only git, npm, and openspec commands.
