# How to Use the Documentation Update Tool

## Prerequisites & Authentication

### ✅ What You Need:
- **GitHub Copilot subscription** (CLI, VS Code, or any Copilot interface)
- **GitHub CLI (`gh`) authenticated** with access to Microsoft repos
- Access to this repository: `https://github.com/GrantMeStrength/windows-docs-automation`

### 🔐 How Authentication Works

**The tool uses YOUR credentials** - When you run this tool from your terminal or VS Code:

1. **Copilot runs as YOU** - It uses your GitHub authentication
2. **Your access = Tool's access** - If you can access `MicrosoftDocs/windows-dev-docs-pr`, the tool can too
3. **No special permissions needed** - Just your normal GitHub/Microsoft access

**Why This Matters:**
- ✅ **Works seamlessly** if you have repo access
- ✅ **Respects security** - Only edits repos you can already access
- ✅ **No token sharing** - Uses your existing authentication
- ❌ **Won't work** if you don't have access to the target repository

### 🎫 How to Get Repository Access

If you need access to Microsoft documentation repositories:

#### For Microsoft Employees:

1. **Join the MicrosoftDocs organization** on GitHub
   - Visit: https://repos.opensource.microsoft.com/
   - Sign in with your Microsoft account
   - Link your GitHub account

2. **Request access to specific repos**
   - Go to: https://repos.opensource.microsoft.com/MicrosoftDocs/teams
   - Find the team for your doc set (e.g., "windows-dev-docs")
   - Request to join the team

3. **Authenticate GitHub CLI**
   ```bash
   gh auth login
   ```
   - Choose "GitHub.com"
   - Choose "HTTPS" protocol
   - Authenticate with a browser
   - Select scopes: `repo`, `read:org`, `workflow`

4. **Verify access**
   ```bash
   gh repo list MicrosoftDocs | grep windows-dev-docs-pr
   ```
   You should see: `MicrosoftDocs/windows-dev-docs-pr  private`

#### For External Contributors:

- You'll work with **public repositories** (without `-pr` suffix)
- Example: `MicrosoftDocs/windows-dev-docs` (public)
- The tool will **automatically use public repos** if you don't have private access
- Your PRs will go through standard external contributor review process

### 🔄 Automatic Fallback Behavior

The tool is smart about repository access:

1. **First tries private repo** (e.g., `windows-dev-docs-pr`)
2. **If access denied** → Automatically tries public repo (e.g., `windows-dev-docs`)
3. **Notifies you** which repo it's using
4. **Continues smoothly** with whichever repo is accessible

**Example:**
```
🔍 Checking MicrosoftDocs/windows-dev-docs-pr... Access denied
🔄 Falling back to MicrosoftDocs/windows-dev-docs... ✅ Access granted
📝 Using public repository. Your PR will need standard review process.
```

### ❌ What You DON'T Need:
- MCP Learn server registration
- Azure OpenAI API keys
- Special app permissions
- Additional software beyond GitHub CLI

---

## Quick Start (3 Steps)

### Step 1: Open GitHub Copilot

**In VS Code:**
- Press `Ctrl+Shift+I` (Windows) or `Cmd+Shift+I` (Mac)
- Or click the Copilot icon in the activity bar

**In GitHub Copilot CLI:**
```bash
gh copilot
```

### Step 2: Copy and Paste This Prompt

```
I need to make a quick edit to existing Windows documentation.

URL: https://learn.microsoft.com/windows/apps/design/input/pen-and-stylus-interactions
Edit: Update the second paragraph to say that the ink feature is now supported on all Windows 11 devices.

Please use the Documentation Update Tool workflow from:
https://github.com/GrantMeStrength/windows-docs-automation
```

**Important:** Include the repository URL so Copilot knows where to find the workflow instructions.

### Step 3: Follow Along

Copilot will:
1. Find the correct repository and file
2. Check if it's conceptual content (not API reference)
3. Make the edit with AI
4. Show you a diff
5. Ask for your approval
6. Create a PR and notify the docs team

---

## Link to the Tool

Share this link with your team:

**Documentation Update Tool:**
```
https://github.com/GrantMeStrength/windows-docs-automation/blob/main/workflows/DOC-UPDATE-README.md
```

**Or use the short prompt:**
```
Use the Documentation Update Tool from github.com/GrantMeStrength/windows-docs-automation
```

---

## Example Scenarios

### 1. Simple Content Update

```
URL: https://learn.microsoft.com/windows/apps/windows-app-sdk/downloads
Edit: Add a note that version 1.5 is now in preview

Use the Documentation Update Tool workflow.
```

### 2. Fix Prerequisites

```
URL: https://learn.microsoft.com/windows/uwp/get-started/create-a-hello-world-app
Edit: Update the prerequisites section to require Visual Studio 2022 instead of 2019

Use the Documentation Update Tool from:
https://github.com/GrantMeStrength/windows-docs-automation
```

### 3. Add Troubleshooting Tip

```
URL: https://learn.microsoft.com/windows/apps/design/basics/navigation-basics
Edit: Add a troubleshooting tip at the end about navigation events not firing on first load

Use Doc Update Tool (github.com/GrantMeStrength/windows-docs-automation)
```

### 4. Remove Outdated Warning

```
URL: https://learn.microsoft.com/windows/apps/develop/data-access/sqlite-databases
Edit: Remove the warning about SQLite not being available on Xbox (it's now supported)

Use Documentation Update Tool workflow.
```

---

## How Copilot Finds the Workflow

When you include the repository URL, Copilot:

1. **Fetches the repository structure** using GitHub API
2. **Reads the workflow file**: `workflows/doc-update-workflow.md`
3. **Follows the instructions** step-by-step
4. **Uses the configuration**: `config/doc-update-config.json`
5. **Validates with schema**: `schemas/doc-update-schema.json`

All of this happens automatically - you don't need to do anything special!

---

## What About MCP Servers?

**You don't need MCP Learn server** for this tool. Here's why:

### What the Tool Uses:
- ✅ **GitHub MCP Server** - Built into Copilot CLI (list repos, files, create PRs)
- ✅ **Standard Tools** - bash, git, file operations
- ✅ **Web Fetch** - Gets repository mapping guide

### What the Tool Does NOT Use:
- ❌ Microsoft Learn MCP Server (not required)
- ❌ Azure OpenAI API keys
- ❌ Special authentication
- ❌ Custom installations

The GitHub MCP Server is included with GitHub Copilot CLI by default, so if you have Copilot, you're ready to go!

---

## Limitations to Remember

### ✅ Works With:
- Conceptual documentation
- Tutorials and how-to guides
- Overview and getting started pages
- Troubleshooting guides
- Migration guides

### ❌ Doesn't Work With:
- API reference documentation (different publishing pipeline)
- Auto-generated API docs
- Content with `ms.topic: reference`
- Files in `/api/` paths

If you try to edit API reference content, the tool will politely stop and explain the limitation.

---

## Getting Help

**If you encounter issues:**

1. **Check the URL** - Make sure it's from learn.microsoft.com
2. **Verify access** - Ensure you can access the repository
3. **Be specific** - Mention exact paragraph or section to edit
4. **Review the diff** - Copilot will show you the changes before committing

**Need assistance?**
- Email: jkendirs@microsoft.com
- GitHub Issues: https://github.com/GrantMeStrength/windows-docs-automation/issues

---

## Tips for Best Results

1. **Be specific about location**
   - Good: "Update the second paragraph"
   - Better: "Update the paragraph under 'Getting Started' section"

2. **Describe the change clearly**
   - Good: "Say ink is supported"
   - Better: "Say ink feature is now supported on all Windows 11 devices"

3. **One edit at a time**
   - Make focused, single-purpose changes for easier review

4. **Include context if needed**
   - "This change is for the Windows 11 24H2 release"
   - "Update to reflect the new API behavior in version 1.5"

---

## That's It!

No installation, no registration, just copy a prompt and go. The tool handles everything else! 🚀

**Next Steps:**
- [See more prompt examples →](../PROMPTS.md#-documentation-update-tool)
- [Read detailed workflow →](doc-update-workflow.md)
- [View configuration options →](../config/doc-update-config.json)
