# Example Session: Generating Docs with Copilot

This shows a realistic conversation between a user and GitHub Copilot using the Windows Documentation Generator workflow.

---

## Session 1: New Feature Documentation

**User:** I need to generate Windows developer documentation. Please act as the Windows Documentation Generator agent and follow this workflow:

1. Ask me for the 5 required pieces of information
2. Create a documentation plan
3. Generate all necessary files
4. Validate against quality schemas
5. Create a pull request

Use the standards from: https://github.com/GrantMeStrength/windows-docs-automation

---

**Copilot:** I'll help you create comprehensive Windows documentation. Let me gather some quick information.

**Feature name:** What are you documenting?

---

**User:** Window Snapping API

---

**Copilot:** Great! **Content type:** What kind of content is this? (New Feature, API Reference, Tutorial, Migration Guide, Troubleshooting, or something else?)

---

**User:** New Feature

---

**Copilot:** Perfect. **Target audience:** Who is this documentation for? (Beginner, Intermediate, or Advanced developers?)

---

**User:** Intermediate

---

**Copilot:** Got it. **Release version:** What version of Windows App SDK or Windows will this be part of?

---

**User:** Windows App SDK 2.0

---

**Copilot:** Excellent! **Source material:** Do you have a spec document URL or header file path I can analyze?

---

**User:** https://github.com/microsoft/WindowsAppSDK/pull/4321

---

**Copilot:** Perfect! Let me analyze that spec and create a documentation plan.

*[Analyzing spec document...]*

Based on the spec, I'll create the following documentation:

### Documentation Plan

**1. Conceptual Overview** (`window-snapping-overview.md`)
   - What is window snapping?
   - Key scenarios (snap layouts, snap groups, custom snap zones)
   - Architecture overview
   - Prerequisites
   - Related features
   
**2. API Reference** (`api/window-snapping-api.md`)
   - `SnapController` class
     - `SnapToPosition()` method
     - `SnapLayout` property
     - `SnapStateChanged` event
   - `SnapConfiguration` class
     - Layout presets
     - Custom zones
   - `SnapZone` class
   - Enumerations and delegates
   
**3. Tutorial** (`tutorials/snap-windows-tutorial.md`)
   - Basic window snapping (30 min)
   - Custom snap layouts (45 min)
   - Advanced scenarios (snap groups)
   - Step-by-step with complete code
   
**4. Code Samples**
   - `BasicSnapping.cs` - Simple snap implementation
   - `CustomLayouts.cs` - Creating custom snap zones
   - `BasicSnapping.cpp` - C++ equivalent
   - `CustomLayouts.cpp` - C++ custom zones
   
**5. How-To Guides**
   - How to enable window snapping
   - How to create custom layouts
   - How to handle snap events
   - How to restore snap state
   
**6. Troubleshooting** (`troubleshooting/window-snapping.md`)
   - Common errors
   - Performance issues
   - Platform compatibility
   
**7. Updates**
   - TOC.yml updates
   - Landing page updates

**Estimated:** 10 files, ~25 KB of content  
**Quality target:** 90%+ validation score

Does this plan look good? (Reply: yes / no / request changes)

---

**User:** Yes, looks great! Generate it.

---

**Copilot:** Generating all documentation files...

*[Progress indicators...]*

✅ Created: `window-snapping-overview.md` (3.2 KB)  
✅ Created: `api/window-snapping-api.md` (8.7 KB)  
✅ Created: `tutorials/snap-windows-tutorial.md` (4.8 KB)  
✅ Created: `code-samples/BasicSnapping.cs` (1.3 KB)  
✅ Created: `code-samples/CustomLayouts.cs` (2.1 KB)  
✅ Created: `code-samples/BasicSnapping.cpp` (1.5 KB)  
✅ Created: `code-samples/CustomLayouts.cpp` (2.4 KB)  
✅ Created: `how-to/enable-snapping.md` (1.1 KB)  
✅ Created: `how-to/custom-layouts.md` (1.8 KB)  
✅ Created: `troubleshooting/window-snapping.md` (2.6 KB)  

Running validation...

### Validation Results

**Editorial Standards:** 94% ✅ Excellent
- ✅ All metadata fields complete
- ✅ Clear, concise writing (avg 18 words/sentence)
- ✅ Active voice throughout
- ✅ Proper terminology (uses "WinUI" not "WinUI 3")
- ⚠️ One heading could be more descriptive (line 42 in overview)

**API Completeness:** 97% ✅ Excellent
- ✅ All public APIs documented
- ✅ All parameters described with types
- ✅ Return values documented
- ✅ Exceptions listed
- ✅ Code examples for each major API
- ✅ Remarks and cross-references present

**Code Quality:** 100% ✅
- ✅ All samples compile (syntax valid)
- ✅ Error handling included
- ✅ Best practices followed
- ✅ Comments explain intent

**Links & References:** 100% ✅
- ✅ All links valid
- ✅ Relative links for internal docs
- ✅ See-also sections complete

### Overall Quality Score: 95% (Excellent)

**Ready to publish!**

Would you like me to create the pull request? (yes/no)

---

**User:** Yes, create the PR

---

**Copilot:** Creating pull request...

```
✅ Created branch: feature/window-snapping-docs
✅ Committed 10 files
✅ Pushed to origin
✅ Created pull request #5678
```

### Pull Request Created

**Title:** Add Window Snapping API documentation

**URL:** https://github.com/microsoft/windows-dev-docs-pr/pull/5678

**Summary:**
Comprehensive documentation for the new Window Snapping API in Windows App SDK 2.0.

**Files Added:**
- [x] window-snapping-overview.md (3.2 KB)
- [x] api/window-snapping-api.md (8.7 KB)
- [x] tutorials/snap-windows-tutorial.md (4.8 KB)
- [x] code-samples/BasicSnapping.cs (1.3 KB)
- [x] code-samples/CustomLayouts.cs (2.1 KB)
- [x] code-samples/BasicSnapping.cpp (1.5 KB)
- [x] code-samples/CustomLayouts.cpp (2.4 KB)
- [x] how-to/enable-snapping.md (1.1 KB)
- [x] how-to/custom-layouts.md (1.8 KB)
- [x] troubleshooting/window-snapping.md (2.6 KB)

**Quality Validation:**
- ✅ Editorial standards: 94% (Excellent)
- ✅ API completeness: 97% (Excellent)
- ✅ Code quality: 100% (All valid)
- ✅ Links: 100% (All valid)

**Overall Score:** 95% (Excellent - Ready to publish)

**Preview:** [View PR on GitHub](https://github.com/microsoft/windows-dev-docs-pr/pull/5678)

---

**Documentation complete!** 🎉

**Time elapsed:** 7 minutes 42 seconds  
**Time saved:** 7 hours 52 minutes (vs manual creation)

The PR is ready for review and can be merged once approved by the docs team.

---

## Session 2: Quick API Reference

**User:** Document this API: Microsoft.UI.Windowing.SnapController

---

**Copilot:** I'll create API reference documentation for `Microsoft.UI.Windowing.SnapController`.

What's the header file path or spec URL?

---

**User:** C:\code\WindowsAppSDK\src\Windowing\SnapController.h

---

**Copilot:** *[Analyzing header file...]*

Found:
- SnapController class
- 3 methods
- 2 properties
- 1 event
- Related types: SnapConfiguration, SnapZone

Generating API reference documentation...

✅ Created: `api/microsoft.ui.windowing.snapcontroller.md` (6.8 KB)

Includes:
- Class overview
- All method signatures with triple-slash comments
- Property descriptions
- Event documentation
- Code examples (C# and C++)
- Remarks and cross-references

Validation: 96% (Excellent)

Create PR? (yes/no)

---

**User:** Yes

---

**Copilot:** ✅ PR created: https://github.com/.../pull/5679

Done! Single-file API reference ready for review.

---

## Session 3: Improving Quality

**User:** The quality score is only 82%. What's wrong?

---

**Copilot:** Let me show you the specific issues:

### Validation Report (82% - Good, but needs improvement)

**Editorial Standards: 78%** ⚠️
Issues found:
1. Line 23: Sentence too long (34 words) - should be <25
   - "This API allows you to programmatically control..."
   - Suggest: Split into two sentences
   
2. Line 45: Passive voice detected
   - "The window is snapped by calling..."
   - Suggest: "Call SnapToPosition() to snap the window..."
   
3. Line 67: Incorrect terminology
   - Uses "WinUI 3" should be "WinUI"
   
4. Missing description metadata in YAML front matter

**API Completeness: 89%** ⚠️
Issues found:
1. `SnapToPosition()` method missing return value description
2. `SnapStateChanged` event missing parameter descriptions
3. No code example for `CustomSnapZone` property

**Code Quality: 100%** ✅
All good!

**Links: 100%** ✅
All good!

Would you like me to fix these issues and regenerate? (yes/no)

---

**User:** Yes, fix and regenerate

---

**Copilot:** *[Fixing issues...]*

✅ Fixed sentence length (split long sentences)  
✅ Changed to active voice throughout  
✅ Updated "WinUI 3" → "WinUI"  
✅ Added description metadata  
✅ Added return value documentation  
✅ Added event parameter descriptions  
✅ Added code example for CustomSnapZone  

Re-validating...

### Updated Validation Results

- ✅ Editorial standards: 94% (Excellent)
- ✅ API completeness: 97% (Excellent)
- ✅ Code quality: 100% (Perfect)
- ✅ Links: 100% (Perfect)

**Overall: 95% (Excellent - Ready to publish)**

Files updated. Ready to commit? (yes/no)

---

**User:** Yes

---

**Copilot:** ✅ Committed fixes  
✅ Quality score improved: 82% → 95%

Documentation is now excellent and ready to publish!

---

## Key Takeaways

1. **Conversational** - Natural back-and-forth dialogue
2. **Incremental** - Can iterate and improve based on validation
3. **Transparent** - Shows exactly what's being created
4. **Quality-focused** - Validates before committing
5. **Fast** - Complete docs in ~8 minutes
6. **Integrated** - Uses your existing Copilot access

**Just copy a prompt from PROMPTS.md and start chatting with Copilot!** 🚀
