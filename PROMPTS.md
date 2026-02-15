# Quick Start Prompts

Copy and paste these prompts to quickly start the documentation workflow with GitHub Copilot.

## 🚀 Full Workflow Prompt

```
I need to generate Windows developer documentation. Please act as the Windows Documentation Generator agent and follow this workflow:

1. Ask me for the 5 required pieces of information (feature name, content type, audience, version, source)
2. Analyze my input and create a documentation plan
3. Generate all necessary files following Windows authoring standards
4. Validate against the quality schemas in this repository
5. Create a pull request with the documentation

Use the schemas and standards from: https://github.com/GrantMeStrength/windows-docs-automation

Let's start!
```

## 📝 Specific Content Type Prompts

### New Feature Documentation

```
Generate documentation for a new Windows feature using the Windows Documentation Generator workflow.

Feature: [YOUR FEATURE NAME]
Type: New Feature
Audience: [Beginner/Intermediate/Advanced]
Version: [Windows App SDK X.X]
Spec: [URL or file path]

Create: overview, API reference, tutorial, code samples, and troubleshooting guide.
Follow: schemas/editorial-standards-schema.json and schemas/api-doc-standards-schema.json
Validate before creating PR.
```

### API Reference Only

```
Generate API reference documentation for [CLASS/NAMESPACE NAME].

Header file: [path to .h file]
Namespace: [namespace]
Target: Windows App SDK [version]

Follow the API documentation standards in schemas/api-doc-standards-schema.json
Include: Triple-slash comments, parameter descriptions, return values, exceptions, code examples
Validate for 95%+ completeness before showing me.
```

### Tutorial

```
Create a step-by-step tutorial for [TASK/FEATURE].

Difficulty: [Beginner/Intermediate/Advanced]
Time to complete: [XX minutes]
Prerequisites: [list]
Goal: [what user will accomplish]

Include: Prerequisites, step-by-step instructions, complete code samples, expected output, troubleshooting, next steps
Follow tutorial examples from Windows Authoring Guide
```

### Troubleshooting Guide

```
Generate a troubleshooting guide for [FEATURE/SCENARIO].

Common issues:
- [Issue 1]
- [Issue 2]
- [Issue 3]

For each issue include: error message, likely causes, step-by-step solution, prevention tips
Format: Clear headers, numbered steps, code blocks for commands/fixes
```

### Migration Guide

```
Create a migration guide from [OLD VERSION] to [NEW VERSION] for [FEATURE/API].

Breaking changes:
- [Change 1]
- [Change 2]

Include: Overview of changes, step-by-step migration instructions, before/after code samples, testing guidance
```

## 🔄 Iterative Prompts

### After Initial Generation

```
The documentation looks good! Can you:
1. Add more code examples to the tutorial section
2. Expand the troubleshooting guide with [specific error]
3. Include a "Common Pitfalls" section in the overview

Then re-validate and show updated quality score.
```

### Request Specific Improvements

```
The API reference completeness is only 85%. Please:
- Add missing parameter descriptions
- Include return value documentation for all methods
- Add code examples for the top 3 most-used APIs
- Add cross-references to related APIs

Target: 95%+ completeness
```

### Validate Before Committing

```
Before creating the PR, please validate all documentation against:
1. Editorial standards (schemas/editorial-standards-schema.json)
2. API completeness (schemas/api-doc-standards-schema.json)
3. Code sample compilation
4. Link validity

Show me the validation report with specific scores.
```

## 🎯 Context-Enhanced Prompts

### Using @workspace

```
@workspace Generate Windows documentation for [FEATURE] using the automation workflow from this repository.

Reference:
- Standards: schemas/
- Examples: Link to Windows Authoring Guide
- Config: config/agent-config.json

Start by asking me for the required information.
```

### With Specific Files

```
@file:schemas/api-doc-standards-schema.json
@file:schemas/editorial-standards-schema.json

Generate API documentation for [CLASS NAME] that validates 100% against these schemas.

Header file: [path]
```

## 🛠️ Advanced Prompts

### Custom Workflow

```
I need to document [FEATURE] but with a custom structure:

1. Executive summary (200 words max)
2. Technical deep-dive
3. API reference (full)
4. Advanced scenarios
5. Performance considerations
6. Security best practices

Source: [URL]
Audience: Advanced developers
Validate against standard schemas but adapt structure as needed.
```

### Bulk Generation

```
Generate documentation for multiple related APIs:

1. [API 1]
2. [API 2]
3. [API 3]

Source: [header file or spec URL]

For each API:
- Individual API reference page
- Code sample
- Common usage scenario

Plus:
- Single overview page linking all APIs
- Combined troubleshooting guide
- Comparison table

Validate all files before showing me.
```

### Update Existing Docs

```
I have existing documentation that needs updates for [NEW VERSION].

Files to update:
- [file1.md]
- [file2.md]

Changes:
- [Change description]

Please:
1. Analyze existing content
2. Identify what needs updating
3. Generate updated versions
4. Show diff of changes
5. Validate updated docs
6. Create PR with changes

Preserve existing good content, only update what's necessary.
```

## 💬 Conversational Starters

### Simple Start

```
Help me document a new Windows API
```

Then answer the questions Copilot asks.

### With Context

```
I'm documenting the Window Snapping API for intermediate developers. It's part of Windows App SDK 2.0. Can you help me create comprehensive docs?
```

### Quick Generation

```
Generate docs from this spec: [URL]
Content type: New Feature
Audience: Intermediate
Version: Windows App SDK 2.0
```

## 📊 Validation-First Approach

```
Before I create any documentation, please:

1. Fetch and analyze: [spec URL or header file]
2. Show me what you would generate (file list, structure)
3. Explain what standards you'll follow
4. Set quality targets (scores for each validation)
5. Estimate time and complexity

Wait for my approval before generating anything.
```

## 🎓 Learning Prompts

### Show Me How

```
Show me an example of excellent Windows API documentation by:
1. Analyzing examples-gallery.md
2. Generating a sample API doc for a simple class
3. Explaining what makes it high-quality
4. Showing the validation scores

Then I'll give you my actual API to document.
```

### Explain Standards

```
Explain the Windows documentation standards you follow:
1. What's in editorial-standards-schema.json?
2. What's in api-doc-standards-schema.json?
3. Show examples of each standard
4. What quality scores should I target?
```

## 🆘 Troubleshooting Prompts

### Low Quality Score

```
My documentation quality score is only [XX]%. Please:
1. Show me specific issues
2. Explain each problem
3. Show before/after examples
4. Re-generate with fixes
5. Validate again
```

### Missing Information

```
I don't have a spec URL or header file. I can provide:
- Feature description
- Key scenarios
- API surface (list of classes/methods)
- Example usage

Can you generate docs from this information?
```

### Need Different Format

```
The generated docs don't match my needs. I need:
- [Different structure]
- [Different sections]
- [Different style]

Can you regenerate following this custom structure while still validating against the quality schemas?
```

---

## 💡 Tips

1. **Be specific** - The more context you provide, the better the output
2. **Iterate** - Start with generation, then refine based on validation
3. **Reference files** - Use @file: to give Copilot direct access to schemas
4. **Validate first** - Always validate before creating PR
5. **Use examples** - Ask Copilot to reference examples-gallery.md for patterns

---

## 🎯 One-Liner Prompts

For quick starts:

```
Generate Windows docs from: [URL]
```

```
Document this API: [header file path]
```

```
Create tutorial for: [feature name]
```

```
Update docs for version: [new version]
```

---

**Copy any prompt above and paste into Copilot to get started!** 🚀
