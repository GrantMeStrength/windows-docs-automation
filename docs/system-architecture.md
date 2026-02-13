# Windows Documentation Automation - System Architecture

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        User Interface (Web App)                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │ Intake Form  │  │   Preview    │  │ PR Dashboard │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API Gateway (Azure Functions)               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │ /api/intake  │  │/api/generate │  │ /api/publish │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Orchestration Layer                           │
│                                                                   │
│  ┌──────────────────────────────────────────────────────┐       │
│  │          WindowsDocsGenerator Agent                   │       │
│  │                                                        │       │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐│       │
│  │  │ Planner │→ │Generator│→ │Validator│→ │Publisher││       │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘│       │
│  │                                                        │       │
│  └──────────────────────────────────────────────────────┘       │
└─────────────────────────────────────────────────────────────────┘
                              │
                ┌─────────────┼─────────────┐
                ▼             ▼             ▼
      ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
      │  Azure      │  │  Knowledge  │  │  External   │
      │  OpenAI     │  │    Base     │  │   APIs      │
      │  Service    │  │  (Schemas)  │  │             │
      └─────────────┘  └─────────────┘  └─────────────┘
                                              │
                          ┌───────────────────┼───────────────────┐
                          ▼                   ▼                   ▼
                    ┌──────────┐      ┌──────────┐      ┌──────────┐
                    │  GitHub  │      │  Azure   │      │Compiler  │
                    │   API    │      │DevOps API│      │ Service  │
                    └──────────┘      └──────────┘      └──────────┘
```

## Component Details

### 1. Web Application (Frontend)

**Technology:** React + Next.js + TypeScript

**Pages:**
- `/` - Landing page with features overview
- `/create` - Documentation creation wizard
- `/status/:jobId` - Generation progress tracking
- `/preview/:jobId` - Content preview before PR
- `/dashboard` - User's documentation projects
- `/admin` - System metrics and monitoring

**Key Features:**
- Real-time form validation
- Progress indicators
- Live preview with syntax highlighting
- Diff view for generated content
- Responsive design (desktop/mobile)

**State Management:**
- React Context for global state
- React Query for API data
- Local storage for form persistence

---

### 2. API Gateway (Backend)

**Technology:** Azure Functions (Node.js/TypeScript)

**Endpoints:**

```typescript
// Intake
POST /api/intake
  Body: IntakeFormData
  Returns: { sessionId: string }

// Planning
POST /api/plan
  Body: { sessionId: string }
  Returns: { plan: DocumentationPlan, estimate: Estimate }

// Generation
POST /api/generate
  Body: { sessionId: string, approvedPlan: DocumentationPlan }
  Returns: { jobId: string }

GET /api/status/:jobId
  Returns: { status: Status, progress: number, currentPhase: string }

// Validation
GET /api/validation/:jobId
  Returns: { validationReport: ValidationReport, qualityScore: number }

// Preview
GET /api/preview/:jobId
  Returns: { files: GeneratedFile[], previewUrl: string }

// Publication
POST /api/publish/:jobId
  Body: { approveOverride: boolean }
  Returns: { prUrl: string, prNumber: number }

// Utility
GET /api/repos
  Returns: { repos: RepositoryInfo[] }

GET /api/templates/:contentType
  Returns: { template: Template }
```

**Authentication:**
- Microsoft Entra ID (Azure AD)
- OAuth 2.0 flow
- JWT tokens for API access

**Authorization:**
- Role-based access control (RBAC)
- Roles: `contributor`, `reviewer`, `admin`
- Scope validation per endpoint

---

### 3. WindowsDocsGenerator Agent

**Technology:** Azure OpenAI + Custom Logic

#### 3.1 Planner Module

**Responsibilities:**
- Parse source materials (spec docs, header files)
- Extract API definitions
- Identify key concepts
- Generate documentation outline
- Estimate scope and effort

**Implementation:**
```typescript
class Planner {
  async createPlan(
    userInputs: IntakeFormData,
    sourceMaterials: SourceMaterial[]
  ): Promise<DocumentationPlan> {
    // Load content planning template
    const template = await this.loadTemplate('content_planning');
    
    // Parse source materials
    const extracted = await this.extractAPIs(sourceMaterials);
    
    // Generate plan using GPT-4
    const plan = await this.generateWithAI({
      template,
      userInputs,
      extractedInfo: extracted,
      context: this.knowledgeBase.standards
    });
    
    // Validate plan completeness
    await this.validatePlan(plan);
    
    return plan;
  }
}
```

#### 3.2 Generator Module

**Responsibilities:**
- Generate conceptual documentation
- Create API reference pages
- Write code samples
- Apply editorial standards
- Use examples as patterns

**Implementation:**
```typescript
class Generator {
  async generateConceptualDoc(
    docSpec: DocSpecification
  ): Promise<GeneratedDocument> {
    // Find similar examples from gallery
    const examples = await this.findSimilarExamples(docSpec.type);
    
    // Load editorial standards
    const standards = await this.loadStandards('editorial');
    
    // Generate content
    const content = await this.generateWithAI({
      spec: docSpec,
      examples,
      standards,
      instructions: this.buildPrompt(docSpec)
    });
    
    // Apply metadata
    content.metadata = this.generateMetadata(docSpec);
    
    return content;
  }
  
  async generateAPIReference(
    apiMember: APIDefinition
  ): Promise<GeneratedDocument> {
    // Load API doc standards
    const standards = await this.loadStandards('api');
    
    // Generate triple-slash comments
    const content = await this.generateWithAI({
      apiMember,
      standards,
      template: this.apiTemplates[apiMember.type]
    });
    
    return content;
  }
  
  async generateCodeSample(
    scenario: Scenario,
    language: string
  ): Promise<CodeSample> {
    const sample = await this.generateWithAI({
      scenario,
      language,
      requirements: this.codeStandards,
      includeComments: true,
      includeErrorHandling: true
    });
    
    // Validate compilation
    await this.validateCompilation(sample, language);
    
    return sample;
  }
}
```

#### 3.3 Validator Module

**Responsibilities:**
- Validate against editorial standards schema
- Check API documentation completeness
- Compile code samples
- Verify links
- Calculate quality score

**Implementation:**
```typescript
class Validator {
  async validate(
    generatedFiles: GeneratedFile[]
  ): Promise<ValidationReport> {
    const report: ValidationReport = {
      overall: 0,
      checks: []
    };
    
    for (const file of generatedFiles) {
      // Validate metadata
      const metadataCheck = await this.validateMetadata(
        file,
        this.schemas.metadata
      );
      report.checks.push(metadataCheck);
      
      // Validate content structure
      const structureCheck = await this.validateStructure(
        file,
        this.schemas.editorial
      );
      report.checks.push(structureCheck);
      
      // Validate code samples
      if (file.type === 'code') {
        const compileCheck = await this.compileCode(file);
        report.checks.push(compileCheck);
      }
      
      // Validate links
      const linkCheck = await this.validateLinks(file);
      report.checks.push(linkCheck);
    }
    
    // Calculate overall score
    report.overall = this.calculateScore(report.checks);
    report.qualityLevel = this.determineQualityLevel(report.overall);
    
    return report;
  }
  
  private async compileCode(
    file: CodeSample
  ): Promise<ValidationCheck> {
    const result = await this.compilerService.compile({
      code: file.content,
      language: file.language,
      sdk: file.targetSDK
    });
    
    return {
      name: 'code_compilation',
      passed: result.success,
      errors: result.errors,
      warnings: result.warnings
    };
  }
}
```

#### 3.4 Publisher Module

**Responsibilities:**
- Clone target repository
- Create feature branch
- Commit generated files
- Create pull request
- Tag reviewers

**Implementation:**
```typescript
class Publisher {
  async publish(
    jobId: string,
    validationReport: ValidationReport
  ): Promise<PublicationResult> {
    // Get generated files
    const files = await this.storage.getGeneratedFiles(jobId);
    const metadata = await this.storage.getMetadata(jobId);
    
    // Determine target repo
    const repo = await this.determineRepository(metadata.contentType);
    
    // Clone repository
    await this.git.clone(repo.url);
    
    // Create branch
    const branchName = this.generateBranchName(metadata);
    await this.git.createBranch(branchName);
    
    // Commit files
    for (const file of files) {
      await this.git.add(file.path, file.content);
    }
    
    const commitMsg = this.generateCommitMessage(metadata);
    await this.git.commit(commitMsg);
    
    // Push branch
    await this.git.push(branchName);
    
    // Create PR
    const prDescription = await this.generatePRDescription({
      metadata,
      validationReport,
      files
    });
    
    const pr = await this.github.createPullRequest({
      title: this.generatePRTitle(metadata),
      body: prDescription,
      base: 'main',
      head: branchName,
      reviewers: ['@windows-docs'],
      labels: ['auto-generated', 'needs-review']
    });
    
    return {
      prUrl: pr.html_url,
      prNumber: pr.number,
      branchName
    };
  }
}
```

---

### 4. Knowledge Base

**Storage:** Azure Blob Storage + Search Index

**Structure:**
```
knowledge-base/
├── standards/
│   ├── editorial-standards.md
│   ├── api-doc-standards.md
│   └── schemas/
│       ├── editorial-standards-schema.json
│       └── api-doc-standards-schema.json
├── examples/
│   ├── examples-gallery.md
│   └── indexed-examples/
│       ├── conceptual-excellent.md
│       ├── api-reference-excellent.md
│       └── tutorial-excellent.md
├── templates/
│   ├── content-planning-template.md
│   ├── conceptual-doc-template.md
│   └── api-reference-template.md
└── process/
    ├── getting-started-checklist.md
    ├── troubleshooting.md
    └── repo-locations.md
```

**Embedding & Search:**
- Convert all docs to embeddings (Azure OpenAI)
- Store in Azure Cognitive Search
- Similarity search for pattern matching
- Vector search for example retrieval

---

### 5. External Services

#### 5.1 Azure OpenAI Service

**Models:**
- GPT-4 (content generation)
- GPT-4 Turbo (faster planning)
- text-embedding-ada-002 (embeddings)

**Configuration:**
```json
{
  "deployment": "gpt-4-32k",
  "temperature": 0.3,
  "max_tokens": 8000,
  "top_p": 0.95,
  "frequency_penalty": 0.2,
  "presence_penalty": 0.1
}
```

#### 5.2 GitHub API

**Operations:**
- Clone repositories
- Create branches
- Commit files
- Create pull requests
- Manage reviewers/labels

**Authentication:** GitHub App (installation token)

#### 5.3 Compilation Service

**Technology:** Docker containers with SDKs

**Supported Languages:**
- C# (.NET 8 SDK)
- C++ (MSVC, Clang)
- JavaScript (Node.js)
- TypeScript (tsc)

**API:**
```
POST /compile
Body: {
  code: string,
  language: string,
  sdk: string
}
Returns: {
  success: boolean,
  errors: CompilerError[],
  warnings: CompilerWarning[]
}
```

---

## Data Flow

### Happy Path: Feature Owner Creates Documentation

```
1. User fills intake form
   ↓
2. Form validated client-side
   ↓
3. POST /api/intake
   ↓
4. Session created, source materials fetched
   ↓
5. POST /api/plan
   ↓
6. Agent analyzes sources, generates plan
   ↓
7. User reviews and approves plan
   ↓
8. POST /api/generate
   ↓
9. Agent generates all content:
   - Conceptual docs (using examples gallery patterns)
   - API reference (using API standards)
   - Code samples (compiled and validated)
   ↓
10. Automatic validation:
    - Metadata complete: ✅
    - Code compiles: ✅
    - Links valid: ✅
    - Quality score: 87%
   ↓
11. User reviews preview
   ↓
12. POST /api/publish
   ↓
13. Agent creates PR:
    - Clones windows-dev-docs-pr
    - Creates branch: owner/feature-name
    - Commits 7 files
    - Creates PR with validation report
    - Tags @windows-docs
   ↓
14. Docs team reviews PR
   ↓
15. PR merged, content goes live
```

### Total Time: ~8 minutes

---

## Security Architecture

### Authentication Flow

```
1. User visits web app
   ↓
2. Redirected to Microsoft login
   ↓
3. Azure AD authentication
   ↓
4. Token issued (JWT)
   ↓
5. Token included in all API calls
   ↓
6. API Gateway validates token
   ↓
7. Check user roles/permissions
   ↓
8. Allow/Deny request
```

### Data Protection

- **In Transit:** HTTPS/TLS 1.3
- **At Rest:** Azure Storage encryption
- **Secrets:** Azure Key Vault
- **Access:** RBAC, Conditional Access policies
- **Audit:** All operations logged to Azure Monitor

### Privacy

- No customer data in prompts
- No proprietary code stored long-term
- Generated content sanitized
- Compliance with Microsoft data policies

---

## Scaling & Performance

### Scaling Strategy

**Frontend:**
- Azure Static Web Apps (auto-scale)
- CDN for static assets (Azure CDN)

**Backend:**
- Azure Functions (consumption plan)
- Auto-scale based on load

**AI Service:**
- Azure OpenAI (quota management)
- Request queuing for rate limiting

### Performance Targets

- Intake form submission: <500ms
- Plan generation: <30s
- Content generation: <5min
- Validation: <30s
- PR creation: <15s

### Caching

- Template cache (Redis)
- Schema cache (in-memory)
- Example embeddings (pre-computed)
- Repository info (1-hour TTL)

---

## Monitoring & Observability

### Metrics

**User Metrics:**
- Documents generated/day
- Average quality score
- PR approval rate
- User satisfaction (NPS)

**System Metrics:**
- API response times
- Error rates
- AI token usage
- Queue lengths

**Business Metrics:**
- Time saved (vs manual)
- Cost per document
- Adoption rate
- Feature requests

### Logging

- Structured logging (JSON)
- Azure Application Insights
- Log levels: DEBUG, INFO, WARN, ERROR
- Retention: 90 days

### Alerting

- API errors > 5% → Page on-call
- AI failures > 10% → Email team
- Validation score <50% → Review queue
- High queue depth → Scale alert

---

## Disaster Recovery

### Backup Strategy

- Generated content: Azure Blob (GRS)
- Configuration: Git repository
- Database: Azure SQL (geo-replicated)

### Recovery Procedures

**Service Outage:**
1. Switch to backup region
2. Redirect traffic via Traffic Manager
3. Restore from backups

**Data Loss:**
1. Restore from point-in-time backup
2. Regenerate missing content
3. Notify affected users

**RTO:** 1 hour  
**RPO:** 15 minutes

---

## Development Workflow

### Local Development

```bash
# Clone repo
git clone https://github.com/MicrosoftDocs/windows-docs-automation
cd windows-docs-automation

# Install dependencies
npm install

# Set up environment
cp .env.example .env
# Edit .env with your Azure credentials

# Run locally
npm run dev

# Frontend: http://localhost:3000
# API: http://localhost:7071
```

### Deployment

```bash
# Build
npm run build

# Test
npm test

# Deploy to staging
npm run deploy:staging

# Deploy to production
npm run deploy:production
```

### CI/CD Pipeline

```yaml
# Azure DevOps Pipeline
trigger:
  - main

stages:
  - stage: Build
    jobs:
      - job: BuildApp
        steps:
          - npm install
          - npm run build
          - npm test
  
  - stage: DeployStaging
    jobs:
      - job: Deploy
        steps:
          - Azure Static Web Apps Deploy
          - Azure Functions Deploy
  
  - stage: DeployProduction
    condition: succeeded()
    jobs:
      - job: Deploy
        steps:
          - Azure Static Web Apps Deploy
          - Azure Functions Deploy
```

---

## Cost Estimate

**Monthly (estimated 100 docs/month):**

| Service | Usage | Cost |
|---------|-------|------|
| Azure Static Web Apps | 100GB bandwidth | $9 |
| Azure Functions | 100,000 executions | $20 |
| Azure OpenAI | 10M tokens | $300 |
| Azure Storage | 100GB | $5 |
| Azure Cognitive Search | Basic tier | $75 |
| Compilation VMs | 200 hours | $50 |
| **Total** | | **~$459/month** |

**Cost per document:** ~$4.59

**Manual alternative cost:** 8 hours × $100/hr = **$800/document**

**Savings:** **~$795/document** (99.4% reduction)

---

## Next Steps

1. **Phase 1:** Deploy MVP (intake + planning)
2. **Phase 2:** Add content generation
3. **Phase 3:** Add validation + PR creation
4. **Phase 4:** Add monitoring + metrics
5. **Phase 5:** Add advanced features (video, localization)

---

## Appendix

### Technology Stack Summary

- **Frontend:** React, Next.js, TypeScript, Tailwind CSS
- **Backend:** Azure Functions, Node.js, TypeScript
- **AI:** Azure OpenAI (GPT-4, embeddings)
- **Storage:** Azure Blob Storage, Azure SQL
- **Auth:** Microsoft Entra ID
- **CI/CD:** Azure DevOps
- **Monitoring:** Application Insights, Azure Monitor
- **Hosting:** Azure Static Web Apps, Azure Functions

### Key Dependencies

```json
{
  "dependencies": {
    "react": "^18.2.0",
    "next": "^14.0.0",
    "@azure/openai": "^1.0.0",
    "@octokit/rest": "^20.0.0",
    "ajv": "^8.12.0",
    "marked": "^11.0.0"
  }
}
```
