# Getting Started with Windows Documentation Generator

A tool that helps feature teams and technical writers create Windows developer documentation using GitHub Copilot.

---

## What It Does

**Copilot generates:**
- Structured first drafts from specs or header files
- API reference documentation
- Tutorials and code samples
- Standards-compliant formatting

**Writers then:**
- Review and refine for accuracy
- Add context and advanced scenarios
- Improve clarity and polish content

---

## How to Use It

### Step 1: Open GitHub Copilot

**In VS Code:**
- Press `Ctrl+Shift+I` (Windows) or `Cmd+Shift+I` (Mac)
- Opens Copilot Chat panel

**In GitHub CLI:**
- Use `gh copilot suggest` command

### Step 2: Copy This Prompt

```
I need to generate Windows developer documentation. Please act as the 
Windows Documentation Generator agent and follow this workflow:

1. Ask me for the 5 required pieces of information
2. Create a documentation plan
3. Generate all necessary files
4. Validate against quality schemas
5. Create a pull request

Use the standards from: https://github.com/GrantMeStrength/windows-docs-automation

Let's start!
```

### Step 3: Answer 5 Questions

Copilot will ask you:

1. **Feature name** - What are you documenting?
2. **Content type** - New Feature, API Reference, Tutorial, etc.
3. **Target audience** - Beginner, Intermediate, or Advanced
4. **Release version** - e.g., "Windows App SDK 2.0"
5. **Source** - Spec document URL OR header file path

**For API documentation:**
6. **Existing stub files?** - Do you have stubbed-out API topics?
   - If yes: Provide directory path, Copilot will fill them in
   - If no: Copilot will create new files

### Step 4: Review the Plan

Copilot shows you what it will create or fill:
- List of files (new or existing stubs)
- What content will be added
- Structure and sections

Approve it or ask for changes.

### Step 5: Generate Documentation

Copilot creates all files:
- ✅ Conceptual overview
- ✅ API reference
- ✅ Tutorial with code samples
- ✅ Troubleshooting guide
- ✅ Validation report with quality scores

### Step 6: Review and Refine

Technical writers:
- Review generated content for accuracy
- Add context and real-world scenarios
- Enhance examples
- Improve clarity and flow
- Final editorial polish

### Step 7: Create Pull Request

Copilot creates a PR with:
- All documentation files
- Validation report
- Quality scores

---

## Example Conversation

**You:** [Paste the prompt above]

**Copilot:** I'll help you create comprehensive Windows documentation. Let me gather some quick information.

**Feature name:** What are you documenting?

**You:** Window Snapping API

**Copilot:** Great! **Content type:** What kind of content is this?

**You:** New Feature

**Copilot:** Perfect. **Target audience:** Who is this documentation for?

**You:** Intermediate

**Copilot:** Got it. **Release version:** What version will this be part of?

**You:** Windows App SDK 2.0

**Copilot:** Excellent! **Source material:** Do you have a spec document URL or header file path?

**You:** https://github.com/microsoft/WindowsAppSDK/pull/1234

**Copilot:** [Generates plan, creates files, validates, creates PR]

Done! ✅

---

## What Gets Created

Typical documentation set:
- `overview.md` - Conceptual introduction
- `api-reference.md` - Complete API documentation
- `tutorial.md` - Step-by-step guide
- `code-samples/` - C# and C++ examples
- `troubleshooting.md` - Common issues and solutions
- Pull request with validation report

---

## Quality Validation

Every document is validated against:
- ✅ Editorial standards (metadata, clarity, terminology)
- ✅ API completeness (all methods documented)
- ✅ Code quality (samples compile)
- ✅ Links and references

**Typical quality score:** 90-95% (Excellent)

---

## Tips

- **Have your spec or header file ready** - Makes generation faster and more accurate
- **Review the plan** - Make sure structure fits your needs before generation
- **Iterate** - Ask Copilot to regenerate specific sections if needed
- **Validate** - Check quality scores before creating PR
- **Refine** - Writers add the context and polish that makes docs great

---

## Need Help?

**Quick reference:** https://github.com/GrantMeStrength/windows-docs-automation/blob/main/QUICK_REFERENCE.md

**Full guide:** https://github.com/GrantMeStrength/windows-docs-automation/blob/main/COPILOT_WORKFLOW.md

**Example sessions:** https://github.com/GrantMeStrength/windows-docs-automation/blob/main/EXAMPLE_SESSION.md

**Repository:** https://github.com/GrantMeStrength/windows-docs-automation

---

## Questions?

Contact your documentation team or visit the repository.

---

**Ready to try?** Just copy the prompt above and paste it into Copilot!
