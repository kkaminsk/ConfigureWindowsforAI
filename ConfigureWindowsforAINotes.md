Installing **Claude Code** (Anthropic’s agentic CLI) and **OpenSpec** (a spec-driven development framework) creates a powerful environment where you can design features before the AI writes a single line of code.

Here is a brief manual to get both up and running on your machine.

------

### 📋 Prerequisites

Before you start, ensure your environment meets these requirements:

- **Account**: An active Claude Pro/Max subscription or Claude Console API credits.
- **Account**: An active Copilot subscription is a nice to have.

- **VS Code**: Visual Studio Code should be installed.
- **Node.js**: Version **20.19.0** or higher is required for OpenSpec.
- **Terminal**: PowerShell 7.

#### Install Prerequisites via winget

Open PowerShell and run:

```powershell
winget install Microsoft.VisualStudioCode
winget install Microsoft.PowerShell
winget install OpenJS.NodeJS
```

*Restart your terminal after installation to ensure the new tools are available in your PATH.*

------

### 🚀 Step 1: Install Claude Code

Claude Code is the primary engine. Install it via winget for easy management and updates.

```powershell
winget install Anthropic.ClaudeCode
```

*After installation, run `claude` in your terminal to complete the login process.*

------

### 🛠️ Step 2: Install OpenSpec

OpenSpec is the framework that forces the AI to plan before it codes. Since it is a Node package, you install it via `npm`.

Run this command in PowerShell:

```powershell
npm install -g @fission-ai/openspec@latest
```

*Verify the installation by running `openspec --version`.*

------

### 🔗 Step 3: Connect & Initialize

This step bridges the two tools. You must run this **inside your project folder**.

1. **Navigate to your project folder:**

   ```powershell
   cd my-project-folder
   ```

2. **Initialize OpenSpec:**

   ```powershell
   openspec init
   ```

   - The tool will ask which AI assistant you use. Select **Claude Code**.
   - It will automatically configure slash commands (like `/openspec`) for you.

------

### 🏁 Authenticate Claude

Before you begin, make sure to launch Claude and log in.
   ```
   claude
   ```

------

### 🏁 Make an Application Specification

Make an application specification by hand or use Claude to create one.

   ```
   Make me a powershell script that does a Hello World prompt and then exits. Document the specification in a file called `spec.md`.
   ```

------

### 🏁 Clarify the Specification

Now take it a step further and create a more complex specification. Ask Claude to read the specification and ask questions to clarify requirements.

   ```
   Read the spec.md and ask questions to clarify requirements. Put these questions in a file called `questions.md`.
   ```

------

### 🏁 Now Use Some Seper Powers

Take the questions and use them to clarify the specification.

   ```
   Read the questions.md and use them to clarify the specification in spec.md.
   ```

------

### 🏁 Now Use Some Seper Powers

Update the project.md file with the specification.

   ```
   Read the spec.md and update the project.md file with the specification.
   ```

------

### 🏁 How to Use Openspec

Take the specification and use it to create the project.md.

1. **Start Claude:** Run `claude` in your terminal.

2. **Create a Proposal:** Instead of asking Claude to "write code," use the slash command:

   ```
   /openspec:proposal read the spec.md and create a series of tasks to implement the specification. Number the tasks sequentially in order of implementation.
   ```

   *Claude will generate a `proposal.md` and `tasks.md` instead of writing code immediately.*

3. **Review:** Check the generated spec files.

4. **Apply:** Once you agree with the plan, tell Claude to execute it:

   ```
   /openspec:apply the next proposal
   ```

------
