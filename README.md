# Windows Documentation Automation System

## Two Automation Tools

### 🆕 **Documentation Update Tool** (Quick Edits)
Make quick edits to existing conceptual documentation. Just provide a URL and describe the change!

👉 **[Quick Start →](workflows/DOC-UPDATE-README.md)** | **[Detailed Workflow →](workflows/doc-update-workflow.md)** | **[Prompts →](PROMPTS.md#-documentation-update-tool)**

**Example:**
```
URL: https://learn.microsoft.com/windows/apps/design/input/pen-and-stylus-interactions
Edit: Update second paragraph to say ink feature is now supported on all Windows 11 devices

Use the Documentation Update Tool workflow.
```

### ⭐ **Documentation Generator** (New Content)
Generate complete documentation sets from scratch. Perfect for new features!

👉 **[Quick Reference →](QUICK_REFERENCE.md)** | **[Full Guide →](COPILOT_WORKFLOW.md)** | **[Copy Prompts →](PROMPTS.md)** | **[See Example →](EXAMPLE_SESSION.md)**

---

## Two Ways to Use This System

### ⭐ **Recommended: Copilot Workflow** (Free with your Copilot license)
Use GitHub Copilot directly in VS Code or CLI. No web app needed, no MCP server registration required!

### 🌐 **Alternative: Web Demo**
🚀 **[Try the Live Demo →](https://grantmestrength.github.io/windows-docs-automation/)**

---

## Overview

This system helps feature teams and technical writers create comprehensive Windows developer documentation. It automates the initial draft, structure, and validation, allowing writers to focus on refining content, adding advanced scenarios, and ensuring quality.

**What it does:**
- Generates structured first drafts from specs or header files
- Validates against Windows documentation standards
- Creates complete documentation sets (overview, API reference, tutorials, samples)
- Handles repetitive formatting and structural work

**What writers still do:**
- Review and refine generated content
- Add nuanced explanations and edge cases
- Ensure technical accuracy and completeness
- Enhance examples with real-world scenarios
- Final editorial polish and style improvements

**Integration:** Works directly in your editor via GitHub Copilot

## Architecture

### Components

1. **Web Application** (hosted)
   - User intake form
   - Real-time preview
   - Progress tracking
   - PR management interface

2. **AI Agent** (WindowsDocsGenerator)
   - Content planning
   - Documentation generation
   - Quality validation
   - PR automation

3. **Validation Engine**
   - Schema-based validation
   - Code compilation checks
   - Link verification
   - Quality scoring

4. **Knowledge Base**
   - Editorial standards
   - API documentation guidelines
   - Examples gallery
   - Process documentation

## Directory Structure

```
windows-docs-automation/
├── .github/
│   └── copilot-instructions.md         # Copilot agent definition
├── workflows/                           # ⭐ Agent workflows
│   ├── DOC-UPDATE-README.md            # Documentation Update Tool guide
│   └── doc-update-workflow.md          # Detailed workflow instructions
├── schemas/                             # Machine-readable standards
│   ├── editorial-standards-schema.json
│   ├── api-doc-standards-schema.json
│   ├── intake-form-schema.json
│   └── doc-update-schema.json          # Update tool validation
├── config/                              # Agent configuration
│   ├── agent-config.json
│   └── doc-update-config.json          # Update tool settings
├── templates/                           # Document templates
│   └── pr-description.md
├── docs/                                # System documentation
│   ├── system-architecture.md
│   └── implementation-summary.md
├── webapp/                              # Web demo (optional)
│   └── index.html
├── COPILOT_WORKFLOW.md                  # ⭐ Copilot usage guide
├── PROMPTS.md                           # ⭐ Ready-to-use prompts
└── README.md
```

## Quick Start with Copilot

### 1. Copy a prompt from [PROMPTS.md](PROMPTS.md)

```
I need to generate Windows developer documentation. Please act as the Windows Documentation Generator agent and follow this workflow:

1. Ask me for the 5 required pieces of information
2. Create a documentation plan
3. Generate all necessary files
4. Validate against quality schemas
5. Create a pull request

Use the standards from: https://github.com/GrantMeStrength/windows-docs-automation
```

### 2. Paste into Copilot (VS Code or CLI)

In VS Code: Open Copilot Chat (Ctrl+Shift+I / Cmd+Shift+I)  
In CLI: `gh copilot suggest "..."`

### 3. Answer Copilot's Questions

It will ask for: Feature name, content type, audience, version, and source URL

### 4. Review & Approve

Copilot shows you the plan → you approve → it generates everything

### 5. Done!

PR created with validated, high-quality documentation in ~8 minutes

**[Full Workflow Guide →](COPILOT_WORKFLOW.md)**

---

## Comparison: Copilot vs Web App

| Feature | Copilot Workflow | Web App Demo |
|---------|------------------|--------------|
| **Cost** | Free (your Copilot license) | Would need Azure OpenAI ($5/doc) |
| **Access** | VS Code, CLI, anywhere | Browser only |
| **Integration** | Native to your workflow | Separate tool |
| **Customization** | Full control via prompts | Limited UI options |
| **Offline** | Works with local models | Requires internet |
| **Speed** | ~8 minutes | ~8 minutes |
| **Quality** | Same schemas & standards | Same schemas & standards |
| **Ease of use** | Conversational | Form-based |

**Recommendation:** Use Copilot workflow for production. Web app is for demos.

---

## How It Works

### 1. User Input (5 minutes)

Feature owner fills out minimal web form:
- Feature name
- Spec document URL or header file path
- Target audience
- Release version
- Contact info

### 2. Automated Planning (30 seconds)

Agent analyzes source materials and creates plan:
- Parses spec document or header file
- Identifies APIs, classes, methods
- Determines documentation scope
- Estimates pages and samples needed
- Presents plan for approval

### 3. Content Generation (2-5 minutes)

Agent generates all documentation:
- Conceptual overview pages
- How-to guides
- API reference documentation
- Code samples (multiple languages)
- Applies editorial standards
- Uses examples gallery as patterns

### 4. Quality Validation (30 seconds)

Automated validation against standards:
- Metadata completeness
- Code sample compilation
- Link verification
- Editorial standards compliance
- API documentation completeness
- Generates quality score

### 5. Pull Request Creation (15 seconds)

Agent creates PR automatically:
- Clones correct repository
- Creates feature branch
- Commits generated files
- Creates PR with validation report
- Tags docs team for review

**Total time: ~8 minutes from start to PR**

## Machine-Readable Schemas

### Editorial Standards Schema

Defines validation rules for content quality:
- Metadata requirements
- Technical accuracy checks
- Clarity and structure rules
- Code quality standards
- Voice and style guidelines
- Accessibility requirements

**Usage:**
```json
{
  "metadata": {
    "title": "...",
    "description": "...",
    "validation": "automated"
  },
  "content": {
    "technical_accuracy": {
      "api_names_verified": true,
      "code_samples_compile": true
    }
  }
}
```

### API Documentation Standards Schema

Validates API reference documentation:
- Summary requirements
- Parameter documentation
- Return value documentation
- Exception documentation
- Code example requirements
- Cross-reference requirements

**Usage:**
```json
{
  "api_member": {
    "type": "method",
    "name": "CreateWindow",
    "summary": {
      "text": "Creates a new application window...",
      "starts_with_verb": true
    },
    "parameters": [...]
  }
}
```

### Intake Form Schema

Defines minimal user input required:
- Feature identification
- Content type selection
- Audience specification
- Source material references
- Owner information

**Generates web form automatically from schema**

## Integration with Existing Documentation

The system leverages existing Windows Authoring Guide content:

```
Knowledge Base Sources:
├── editorial-standards.md        → editorial-standards-schema.json
├── api-doc-standards.md          → api-doc-standards-schema.json
├── examples-gallery.md           → Pattern matching database
├── content-planning-template.md  → Planning workflow
├── repo-locations.md             → Repository routing
└── troubleshooting.md            → Error handling rules
```

## Quality Assurance

### Automated Checks

1. **Metadata Validation**
   - All required fields present
   - Correct format (dates, aliases)
   - Appropriate content type

2. **Technical Accuracy**
   - API names verified against SDK
   - Code samples compile
   - Version requirements correct

3. **Content Quality**
   - Proper heading hierarchy
   - Scannable structure
   - Clear language
   - Complete examples

4. **Code Quality**
   - Language tags present
   - Compilable samples
   - Error handling shown
   - Comments included

### Quality Scoring

```
Excellent (90-100%):  Ready to publish with minor review
Good (80-89%):        Needs light editorial review
Acceptable (70-79%):  Needs standard review
Needs Work (<70%):    Requires significant revision
```

## Example User Flow

### Step 1: User submits form

```json
{
  "feature_name": "Window Snapping API",
  "content_type": "new_feature",
  "target_audience": "intermediate",
  "release_info": {
    "version": "Windows App SDK 2.0",
    "release_date": "2026-04-15"
  },
  "source_materials": {
    "spec_doc_url": "https://github.com/microsoft/WindowsAppSDK/blob/main/specs/window-snapping.md"
  }
}
```

### Step 2: Agent presents plan

```
📋 Documentation Plan for Window Snapping API

Content to Create:
✅ 1 Overview page (800 words)
✅ 1 How-to guide (1200 words)  
✅ API reference for 6 classes, 15 methods
✅ 3 code samples (C#, C++)

Estimated effort: 8 hours (manual) → 8 minutes (automated)

Approve plan? [Yes] [Modify] [Cancel]
```

### Step 3: Agent generates content

```
⚙️  Generating documentation...

✅ Created: docs/window-snapping-overview.md
✅ Created: docs/how-to-snap-windows.md
✅ Created: api/WindowSnappingManager.md
✅ Created: api/SnapLayout.md
✅ Created: samples/basic-snapping.cs
✅ Created: samples/advanced-snapping.cs

Running validation...
```

### Step 4: Validation report

```
📊 Quality Report

Overall Score: 87% (Good)

✅ Metadata: 100% complete
✅ Code Samples: All compile successfully
✅ Links: All valid
✅ API Docs: 95% complete
⚠️  3 suggestions for improvement:
  - Add accessibility notes to overview
  - Include keyboard navigation in how-to
  - Add troubleshooting section

Create PR? [Yes] [Review] [Cancel]
```

### Step 5: PR created

```
✅ Pull Request Created!

PR #12345: 📝 new_feature: Window Snapping API
https://github.com/MicrosoftDocs/windows-dev-docs-pr/pull/12345

Files changed: 7
Additions: +1,234 lines

Reviewers: @windows-docs
Labels: auto-generated, needs-review

Estimated review time: 2-3 business days

Preview: https://review.learn.microsoft.com/...?pr=12345
```

## Deployment

### Web Application Stack

**Recommended:**
- Frontend: React/Next.js
- Backend: Node.js/Azure Functions
- AI: Azure OpenAI Service (GPT-4)
- Storage: Azure Blob Storage (for generated files)
- Auth: Microsoft Entra ID (Azure AD)
- Hosting: Azure Static Web Apps + Functions

### Required APIs & Services

1. **Azure OpenAI Service**
   - GPT-4 for content generation
   - Embeddings for similarity matching
   - Function calling for structured output

2. **GitHub API**
   - Repository cloning
   - Branch creation
   - PR creation
   - File operations

3. **Azure DevOps API**
   - For repos hosted in Azure DevOps

4. **Compilation Service**
   - Docker containers with SDKs
   - Compile C#, C++, JavaScript samples
   - Return compilation errors

5. **Link Validation Service**
   - Check internal links
   - Verify external links
   - Validate xref UIDs

## Configuration

### Agent Settings

Edit `config/agent-config.json`:

```json
{
  "quality_gates": {
    "validation_phase": {
      "minimum_score": 80,  // Adjust threshold
      "required_checks": [
        "metadata_complete",
        "code_samples_compile"
      ]
    }
  }
}
```

### Repository Mapping

Agent uses `repo-locations.md` to determine target repository:
- Windows App SDK → windows-dev-docs-pr
- PowerToys → windows-dev-docs-pr
- Win32 → win32-pr
- UWP → windows-uwp-pr

## API Endpoints (Proposed)

```
POST /api/intake
  - Submit intake form
  - Returns: session_id

GET /api/plan/{session_id}
  - Get generated plan
  - Returns: documentation plan

POST /api/generate/{session_id}
  - Start generation
  - Returns: job_id

GET /api/status/{job_id}
  - Check generation status
  - Returns: progress, files generated

GET /api/validation/{job_id}
  - Get validation report
  - Returns: quality score, issues

POST /api/publish/{job_id}
  - Create pull request
  - Returns: PR URL
```

## Security & Privacy

- **Authentication**: Microsoft Entra ID required
- **Authorization**: Only Microsoft employees can create docs
- **Data Privacy**: No customer data in prompts
- **Audit Logging**: All generations logged
- **Rate Limiting**: Prevent abuse

## Metrics & Monitoring

Track:
- Documents generated per week
- Average quality score
- Time saved (vs manual authoring)
- PR approval rate
- User satisfaction

## Future Enhancements

1. **Video Generation**
   - Auto-generate tutorial videos
   - Narration from documentation text

2. **Localization**
   - Auto-translate to supported languages
   - Cultural adaptation

3. **Continuous Updates**
   - Monitor API changes
   - Auto-update documentation

4. **Interactive Samples**
   - Generate CodePen/JSFiddle embeds
   - Live code playgrounds

## Support

- **Documentation**: See `docs/` directory
- **Issues**: GitHub Issues (this repo)
- **Contact**: Windows Docs Team <jkendirs@microsoft.com>

## License

Microsoft Internal Use Only

## Changelog

### Version 1.0.0 (2026-02-13)
- Initial system design
- Schema definitions
- Agent configuration
- Integration with Windows Authoring Guide
