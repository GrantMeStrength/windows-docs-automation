# Quick Reference Card

## 🚀 Generate Docs in 3 Steps

### 1. Open Copilot
- VS Code: `Ctrl+Shift+I` (Windows) or `Cmd+Shift+I` (Mac)
- CLI: `gh copilot suggest "..."`

### 2. Paste This Prompt
```
Generate Windows docs using the automation workflow from 
windows-docs-automation repo. Start by asking me for requirements.
```

### 3. Answer 5 Questions
1. Feature name
2. Content type
3. Target audience  
4. Release version
5. Source (URL or file path)

**Result:** Complete validated documentation set

---

## 📚 Available Prompts

### Full Workflow
```
I need to generate Windows developer documentation. Please act as the 
Windows Documentation Generator agent...
```
[Full prompt in PROMPTS.md](PROMPTS.md#full-workflow-prompt)

### New Feature
```
Generate documentation for a new Windows feature...
Feature: [NAME]
Type: New Feature
Audience: [Beginner/Intermediate/Advanced]
```
[More in PROMPTS.md](PROMPTS.md#new-feature-documentation)

### API Reference Only
```
Generate API reference documentation for [CLASS NAME]
Header file: [path]
```
[More in PROMPTS.md](PROMPTS.md#api-reference-only)

### Tutorial
```
Create a step-by-step tutorial for [TASK]
Difficulty: [level]
```
[More in PROMPTS.md](PROMPTS.md#tutorial)

---

## ✅ Quality Scores

| Score | Grade | Meaning |
|-------|-------|---------|
| 90-100% | Excellent | Ready to publish |
| 80-89% | Good | Light review needed |
| 70-79% | Acceptable | Standard review |
| <70% | Needs work | Significant revision |

**Copilot typically generates:** 93-95% (Excellent)

---

## 📋 What Gets Created

Typical output for a new feature:
- ✅ Conceptual overview (~3 KB)
- ✅ API reference (~8 KB)
- ✅ Tutorial (~4 KB)
- ✅ Code samples (C#, C++)
- ✅ How-to guides
- ✅ Troubleshooting
- ✅ TOC updates
- ✅ Pull request with validation report

**Total:** 10+ files, ~25 KB content

---

## 🎯 Common Commands

### Request Validation
```
Validate all docs against quality schemas and show me the scores
```

### Fix Quality Issues
```
The score is only 82%. Show me specific issues and fix them.
```

### Add More Examples
```
Add 3 more code examples to the tutorial section
```

### Create PR
```
Create a pull request with all the generated documentation
```

---

## 🔧 Troubleshooting

**Problem:** Copilot doesn't have context  
**Solution:**
```
@workspace Load context from windows-docs-automation repository
```

**Problem:** Low quality score  
**Solution:**
```
Show validation report with specific issues, then fix and regenerate
```

**Problem:** Wrong structure  
**Solution:**
```
Regenerate using the template from examples-gallery.md
```

---

## 🎓 Learning Path

1. **Read:** [COPILOT_WORKFLOW.md](COPILOT_WORKFLOW.md)
2. **Try:** Copy a prompt from [PROMPTS.md](PROMPTS.md)
3. **See:** Example in [EXAMPLE_SESSION.md](EXAMPLE_SESSION.md)
4. **Generate:** Your first documentation set
5. **Master:** Custom prompts and workflows

---

## 🔗 Quick Links

| Resource | Purpose |
|----------|---------|
| [COPILOT_WORKFLOW.md](COPILOT_WORKFLOW.md) | Complete guide |
| [PROMPTS.md](PROMPTS.md) | Copy/paste prompts |
| [EXAMPLE_SESSION.md](EXAMPLE_SESSION.md) | See it in action |
| [SUMMARY.md](SUMMARY.md) | Full overview |
| [README.md](README.md) | Project home |

---

## 💡 Pro Tips

1. **Use @workspace** for better context
2. **Validate before committing** - ask for quality scores
3. **Iterate** - improve based on validation feedback
4. **Reference files** - `@file:schemas/api-doc-standards-schema.json`
5. **Save good prompts** - customize for your team

---

## 🆘 Need Help?

- **Questions?** See [COPILOT_WORKFLOW.md](COPILOT_WORKFLOW.md#troubleshooting)
- **Examples?** See [EXAMPLE_SESSION.md](EXAMPLE_SESSION.md)
- **More prompts?** See [PROMPTS.md](PROMPTS.md)
- **Issues?** Create an issue on GitHub

---

**Remember:** You're just one prompt away from complete, validated Windows documentation! 🚀

---

*Keep this card handy - bookmark this page or print it for quick reference.*
