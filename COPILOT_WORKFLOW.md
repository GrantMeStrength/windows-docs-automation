# Windows Documentation Generator - Copilot Workflow

This guide shows you how to use GitHub Copilot / Agency to generate comprehensive Windows documentation using the machine-readable standards and templates in this repository.

## 🎯 Overview

This workflow helps feature teams and technical writers collaborate on Windows documentation. Copilot generates structured first drafts, handles repetitive tasks, and validates against standards - freeing writers to focus on what they do best: refining content, ensuring accuracy, and adding polish.

**Copilot handles:**
- Initial structure and scaffolding
- Basic API documentation from header files
- Code sample generation
- Standards compliance validation
- Formatting and metadata

**Writers focus on:**
- Reviewing and refining generated content
- Adding context and real-world scenarios
- Ensuring technical accuracy
- Improving clarity and flow
- Advanced examples and edge cases
- Final editorial quality

**Integration:** Works directly in VS Code, CLI, or any Copilot interface

---

## 🚀 Quick Start

### Option 1: Using Copilot CLI

```bash
# Navigate to your docs repository
cd /path/to/windows-dev-docs-pr

# Start the documentation workflow with Copilot
gh copilot suggest "Generate Windows documentation using the automation workflow from windows-docs-automation repo"
```

### Option 2: Using VS Code with Copilot Chat

1. Open VS Code in your docs repository
2. Open Copilot Chat (Ctrl+Shift+I / Cmd+Shift+I)
3. Use this prompt:

```
I need to create Windows developer documentation. Please use the workflow from the windows-docs-automation repository to:

1. Ask me the minimal required information
2. Generate a documentation plan
3. Create all necessary files following Windows standards
4. Validate against quality schemas
5. Create a pull request

Use the schemas at: https://github.com/GrantMeStrength/windows-docs-automation
```

---

## 📋 The Copilot-Based Workflow

### Phase 1: Intake (2 minutes)

Copilot will ask you for:
- Feature name
- Content type (New Feature, API Reference, Tutorial, etc.)
- Target audience (Beginner, Intermediate, Advanced)
- Release version
- One of: Spec document URL OR Header file path

**Example conversation:**
```
Copilot: What's the feature name?
You: Window Snapping API

Copilot: What type of content? (New Feature, API Reference, Tutorial, etc.)
You: New Feature

Copilot: Target audience? (Beginner, Intermediate, Advanced)
You: Intermediate

Copilot: Release version?
You: Windows App SDK 2.0

Copilot: Spec document URL or header file path?
You: https://github.com/microsoft/WindowsAppSDK/pull/1234
```

### Phase 2: Planning (~30 seconds)

Copilot will:
1. Fetch and analyze your spec/header file
2. Review Windows authoring guide standards
3. Generate a documentation plan showing:
   - Files to be created
   - Code samples needed
   - Topics to cover
   - Estimated structure

**You review and approve the plan**

### Phase 3: Generation (~5 minutes)

Copilot will create:
- ✅ Conceptual overview document
- ✅ Getting started guide
- ✅ API reference documentation
- ✅ Code samples (C#, C++, etc.)
- ✅ Troubleshooting guide
- ✅ Migration guide (if needed)
- ✅ Updated TOC files

### Phase 4: Validation (~30 seconds)

Copilot will validate against:
- Editorial standards schema
- API documentation standards schema
- Link checker
- Metadata requirements
- Code compilation (simulated)

**You'll get a quality score and fix any issues**

### Phase 5: Publication (~1 minute)

Copilot will:
1. Create a feature branch
2. Commit all files
3. Push to GitHub
4. Create a pull request with:
   - Description
   - Validation report
   - Preview links

**At this point, technical writers take over to:**
- Review the generated content for accuracy
- Refine explanations and add context
- Enhance examples with real-world scenarios
- Improve clarity and flow
- Add edge cases and advanced topics
- Final editorial polish

---

## 👥 Collaboration with Writers

### Recommended Workflow

**1. Feature Team Uses Copilot**
- Generates initial draft from spec/header files
- Creates structured documentation set
- Runs validation to catch basic issues
- Creates PR for writer review

**2. Writer Reviews and Refines**
- Checks technical accuracy
- Improves explanations and clarity
- Adds advanced scenarios
- Enhances code examples
- Addresses edge cases
- Polishes style and voice

**3. Iterative Improvement**
- Writer can ask Copilot to regenerate specific sections
- Can request additional examples or scenarios
- Can validate changes against schemas
- Maintains consistent structure while improving content

### What This Enables

**For Feature Teams:**
- Provide writers with structured first drafts instead of specs
- Reduce back-and-forth on basic structure
- Get documentation started earlier in the development cycle

**For Writers:**
- Receive well-organized content to refine, not blank pages
- Focus time on quality, accuracy, and advanced content
- Spend less time on formatting and structure
- More time for editorial excellence

---

## 🔧 Advanced Usage

### Using the Schemas Directly

The machine-readable schemas can be referenced by Copilot:

```javascript
// Copilot can read and validate against these:
{
  "editorial-standards": "schemas/editorial-standards-schema.json",
  "api-standards": "schemas/api-doc-standards-schema.json",
  "intake-form": "schemas/intake-form-schema.json"
}
```

### Custom Prompts

**For API Documentation:**
```
Generate API reference documentation for [ClassName] following the 
standards in windows-docs-automation/schemas/api-doc-standards-schema.json.

Header file: [path]
Namespace: [namespace]
Target framework: Windows App SDK 2.0
```

**For Tutorials:**
```
Create a tutorial for [feature] following Windows authoring guide standards.
Use examples from windows-docs-automation/schemas/examples-gallery.md.

Feature: [name]
Difficulty: [Beginner/Intermediate/Advanced]
Estimated time: [duration]
```

**For Troubleshooting:**
```
Generate a troubleshooting guide for [feature] based on common issues.
Follow the template in windows-docs-automation/templates/.

Feature: [name]
Common errors: [list]
```

---

## 📚 Context Files for Copilot

When using Copilot, reference these files for better results:

### Standards and Guidelines
- `schemas/editorial-standards-schema.json` - Quality requirements
- `schemas/api-doc-standards-schema.json` - API documentation rules

### Templates
- `templates/pr-description.md` - PR description format

### Configuration
- `config/agent-config.json` - Workflow configuration

### Examples
Reference the Windows Authoring Guide for examples:
- Editorial standards: `.../writing-guidance/editorial-standards.md`
- API standards: `.../writing-guidance/api-doc-standards.md`
- Examples gallery: `.../writing-guidance/examples-gallery.md`

---

## 💡 Pro Tips

### 1. Use Copilot Workspace
For complex documentation, use Copilot Workspace to:
- See all file changes at once
- Review before committing
- Edit multiple files simultaneously

### 2. Leverage @workspace Context
```
@workspace Generate Windows docs for the SnapLayout API using the 
automation workflow from windows-docs-automation
```

### 3. Iterative Refinement
```
The API reference looks good, but can you add more code examples 
following the patterns in examples-gallery.md?
```

### 4. Validation First
```
Before creating the PR, validate all docs against the editorial 
standards schema and show me the quality score.
```

---

## 🎓 Example: Complete Session

```
You: I need to document the new Window Snapping API

Copilot: I'll help you create comprehensive documentation. Let me gather 
some information first.

What's the spec document URL or header file path?

You: https://github.com/microsoft/WindowsAppSDK/pull/1234

Copilot: Great! I'll analyze the spec. What's the target audience?
(Beginner/Intermediate/Advanced)

You: Intermediate

Copilot: Perfect. I'll create:
- Conceptual overview (window-snapping-overview.md)
- API reference (window-snapping-api.md)  
- Tutorial (snap-windows-tutorial.md)
- Code samples (C#, C++)
- Troubleshooting guide

Does this plan look good?

You: Yes, generate it

Copilot: [Generates all files...]

Files created:
✅ window-snapping-overview.md (3.2 KB)
✅ window-snapping-api.md (8.5 KB)
✅ snap-windows-tutorial.md (4.1 KB)
✅ code-samples/snap-window.cs (1.2 KB)
✅ code-samples/snap-window.cpp (1.5 KB)
✅ troubleshooting/window-snapping.md (2.3 KB)

Validation results:
✅ Editorial standards: 92%
✅ API completeness: 95%
✅ Code compiles: ✅
✅ Links valid: ✅

Quality score: 93% (Excellent)

Ready to create PR?

You: Yes

Copilot: [Creates branch, commits, pushes, creates PR...]

PR created: https://github.com/.../pull/5678
Branch: feature/window-snapping-docs
Files: 6 changed, +1,234 insertions

Done! ✅
```

---

## 🔗 Integration with Your Workflow

### VS Code Settings

Add to `.vscode/settings.json`:
```json
{
  "github.copilot.chat.codeGeneration.useInstructionFiles": true,
  "github.copilot.chat.contextReferences": [
    "windows-docs-automation/schemas/",
    "windows-authoring-guide/writing-guidance/"
  ]
}
```

### Copilot Instructions File

Create `.github/copilot-instructions.md`:
```markdown
When generating Windows developer documentation:

1. Follow standards in windows-docs-automation/schemas/
2. Use examples from windows-authoring-guide
3. Always include code samples
4. Validate before creating PR
5. Target Windows App SDK developers
```

---

## 🚦 Quality Gates

Copilot will check:

✅ **Metadata** - title, description, ms.topic, ms.date, etc.  
✅ **Technical Accuracy** - API signatures, parameters, return types  
✅ **Clarity** - Reading level, sentence structure, terminology  
✅ **Completeness** - All sections present, examples included  
✅ **Code Quality** - Samples compile, follow best practices  
✅ **Links** - All URLs valid, relative links correct  
✅ **Accessibility** - Alt text, heading hierarchy, contrast  

**Minimum passing score:** 80%

---

## 📊 Comparison

| Aspect | Web App | Copilot Workflow |
|--------|---------|------------------|
| **Access** | Browser required | VS Code / CLI |
| **Cost** | Azure OpenAI ($5/doc) | Free (Copilot license) |
| **Integration** | Separate tool | Native to workflow |
| **Speed** | ~8 minutes | ~8 minutes |
| **Quality** | Same schemas | Same schemas |
| **Customization** | Limited | Full control |
| **Offline** | No | Yes (with local LLM) |

---

## 🆘 Troubleshooting

**Copilot doesn't have context:**
```
@workspace Load context from windows-docs-automation repository
```

**Quality score too low:**
```
Review the validation report and fix issues. Then re-validate:
Validate docs against editorial-standards-schema.json
```

**Need different structure:**
```
Regenerate using the template from examples-gallery.md for [content type]
```

---

## 🎯 Next Steps

1. **Try it now** - Use the Quick Start commands above
2. **Customize** - Add your own prompts and templates
3. **Share** - Create reusable Copilot instructions for your team
4. **Iterate** - Refine based on validation feedback

**Questions?** See the full system architecture in `docs/system-architecture.md`

---

## 📖 Resources

- **Machine-readable schemas:** `schemas/`
- **Agent configuration:** `config/agent-config.json`
- **System architecture:** `docs/system-architecture.md`
- **Windows Authoring Guide:** See references in schemas

---

**Ready to generate documentation in 8 minutes?** Just start a conversation with Copilot! 🚀
