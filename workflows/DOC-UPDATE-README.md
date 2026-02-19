# Documentation Update Tool

A GitHub Copilot workflow for making quick, surgical edits to existing Windows conceptual documentation on learn.microsoft.com.

## Overview

This tool enables PMs, feature owners, and docs team members to make minor updates to Windows documentation without manually navigating repositories, creating branches, or writing commit messages. Simply provide:

1. **A URL** to the documentation page
2. **A natural language edit description** (e.g., "update second paragraph to say ink feature is now supported")

The tool handles the rest: finding the repository, locating the file, making the edit with AI, creating a PR, and notifying the docs team.

## What It Supports

✅ **Supported Content Types:**
- Conceptual documentation
- Tutorials and how-to guides
- Overview and getting started pages
- Troubleshooting guides
- Migration guides

❌ **Not Supported (Different Publishing Pipeline):**
- API reference documentation
- Auto-generated API docs
- Content with API metadata (`uid:`, `api_name:`, etc.)

## Quick Start

### Using the Tool

Copy this prompt into GitHub Copilot:

```
I need to make a quick edit to existing Windows documentation.

URL: https://learn.microsoft.com/windows/apps/design/input/pen-and-stylus-interactions
Edit: Update the second paragraph to say that the ink feature is now supported on all Windows 11 devices.

Please use the Documentation Update Tool workflow.
```

### What Happens

1. **Repository Discovery** - Finds the correct GitHub repo (prefers private `-pr` repos)
2. **File Location** - Maps URL to markdown file path
3. **Content Validation** - Checks this is conceptual content (blocks API reference)
4. **AI-Powered Editing** - Makes precise changes based on your description
5. **Review** - Shows you a diff and asks for approval
6. **Git Operations** - Creates branch, commits, pushes
7. **Pull Request** - Creates PR with detailed description
8. **Notification** - Alerts docs team (jkendirs@microsoft.com)

## Files in This Tool

```
workflows/
  └── doc-update-workflow.md    # Detailed step-by-step agent instructions
config/
  └── doc-update-config.json    # Configuration settings
schemas/
  └── doc-update-schema.json    # Validation schema for inputs/outputs
PROMPTS.md                       # Example prompts (see "Documentation Update Tool" section)
```

## Example Use Cases

### Simple Update
```
URL: https://learn.microsoft.com/windows/apps/windows-app-sdk/downloads
Change: Add a note that version 1.5 is now in preview
```

### Specific Section Edit
```
URL: https://learn.microsoft.com/windows/uwp/get-started/create-a-hello-world-app
Edit: Update the prerequisites section to require Visual Studio 2022 instead of 2019
```

### Adding Content
```
URL: https://learn.microsoft.com/windows/apps/design/basics/navigation-basics
Edit: Add a troubleshooting tip at the end about navigation events not firing on first load
```

### Removing Outdated Info
```
URL: https://learn.microsoft.com/windows/apps/develop/data-access/sqlite-databases
Edit: Remove the warning about SQLite not being available on Xbox (it's now supported)
```

## How It Works

### Repository Discovery

The tool uses multiple strategies to find the correct repository:

1. Checks the [official repo mapping guide](https://review.learn.microsoft.com/en-us/windows-authoring-guide/writing-guidance/repo-locations)
2. Parses URL patterns (e.g., `/windows/apps/` → `MicrosoftDocs/windows-dev-docs-pr`)
3. Inspects page HTML source for GitHub references
4. Always prefers private repos ending in `-pr`

### AI-Powered Editing

The AI agent:
- Understands natural language edit instructions
- Locates the correct section in the markdown
- Makes minimal, surgical changes
- Preserves all existing formatting, links, and metadata
- Follows Microsoft style guidelines

### Validation & Safety

Before committing, the tool validates:
- ✅ Markdown syntax is valid
- ✅ YAML frontmatter unchanged (unless explicitly requested)
- ✅ No broken links introduced
- ✅ Content is conceptual (not API reference)
- ✅ Changes are within size limits
- ✅ User approves the edit

## Configuration

Edit `config/doc-update-config.json` to customize:

- **Email recipient** for notifications
- **Branch naming** patterns
- **PR title** format and labels
- **Repository mappings** for faster lookup
- **Validation rules** and limits

## Limitations

### Not for API Reference

API reference documentation uses a different publishing pipeline with auto-generation and strict validation. Use the separate API documentation workflow for those changes.

**Blocked content indicators:**
- `ms.topic: reference` or `ms.topic: api`
- Metadata fields: `uid:`, `api_name:`, `api_type:`, `namespace:`, `assembly:`
- Paths containing `/api/`

### Not for Large-Scale Changes

This tool is optimized for quick, surgical edits. For large-scale changes (restructuring, new sections, multiple files), use standard PR workflow or the documentation generator.

## Error Handling

The tool handles common issues gracefully:

| Issue | Resolution |
|-------|-----------|
| Repository not found | Asks user for repo name or shows likely matches |
| File not found | Searches repo and shows matching files |
| Access denied | Suggests using public repo or checking permissions |
| Reference content detected | Stops workflow, explains limitation |
| Edit location unclear | Shows found sections, asks user to clarify |
| User rejects changes | Allows re-editing or cancellation |

## Best Practices

1. **Be specific** in edit descriptions - mention exact sections or paragraph positions
2. **Review the diff** before approving - the AI shows you exactly what will change
3. **Keep edits small** - one logical change per PR for easier review
4. **Provide context** if the change relates to a specific release or feature
5. **Check the URL** - make sure you're editing the right page

## Workflow Details

For complete step-by-step instructions, see:
- **[doc-update-workflow.md](workflows/doc-update-workflow.md)** - Detailed agent workflow
- **[PROMPTS.md](PROMPTS.md)** - Example prompts and variations

## Support

- **Questions?** Contact jkendirs@microsoft.com
- **Issues?** File an issue in this repository
- **Suggestions?** PRs welcome!

## Version

Current version: 1.0.0

---

**Make quick documentation updates with confidence!** 🚀
