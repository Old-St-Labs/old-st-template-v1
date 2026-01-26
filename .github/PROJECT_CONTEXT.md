# PROJECT_CONTEXT.md

## 1. PROJECT OVERVIEW
*   **Project Name:** Project Draper
*   **Purpose:** Automate the conversion of media plans and variant maps into specific creative deliverables lists and Monday.com job entries.
*   **Description:** A web-based internal tool that ingests Excel files (.xlsx) containing "Media Specs" and "Variant Maps." It applies configurable JSON-based business rules to validate data, generate deliverables with automated filename generation, and export results to Excel and Monday.com CSV format.
*   **Repository URL:** *[TODO: Insert GitHub URL]* (Managed by Old St Labs)
*   **Key Source Documents:**
    *   "Complete Media Plan Deliverables Generation Rules"
    *   "Project Draper - Initial Arch Design"

## 2. TECH STACK

### Frontend
*   **Framework:** [TODO: React / Vue / Next.js / Other?]
*   **Language:** [TODO: TypeScript / JavaScript?]
*   **Version:** [TODO: e.g., React 18, Vue 3]
*   **Styling:** [TODO: Tailwind / CSS Modules / Styled Components / Material-UI?]
*   **UI Components:** [TODO: shadcn/ui / Ant Design / Material-UI / Custom?]
*   **State Management:** [TODO: Redux / Zustand / React Query / Context API?]
*   **Form Handling:** [TODO: React Hook Form / Formik / Custom?]
*   **File Upload:** [TODO: Library or native implementation?]

### Backend
*   **Runtime:** AWS Lambda
*   **Language:** [TODO: Node.js (TypeScript/JavaScript) / Python / Other?]
*   **Version:** [TODO: e.g., Node.js 18, Python 3.11]
*   **API Gateway:** AWS API Gateway (REST or HTTP API?)
*   **Framework:** [TODO: Express / Serverless Framework / AWS CDK / SAM?]

### Database
*   **Primary Database:** Amazon DynamoDB
*   **Schema Design:** Single-table design with domain-based partition keys

### File Storage
*   **Service:** AWS S3
*   **Purpose:** Store uploaded Excel files (.xlsx)
*   **Bucket Structure:** [TODO: Bucket naming convention?]

### Authentication
*   **Provider:** AWS Cognito
*   **Methods:** 
    *   Email/Password login
    *   Google SSO (MVP)
    *   [TODO: Future - Full Google Workspace integration]
*   **Token Type:** [TODO: JWT / OAuth 2.0 tokens?]

### APIs & Integrations
*   **Monday.com:** CSV export integration
*   **Excel Processing:** [TODO: Library used - ExcelJS / SheetJS / XLSX / Python openpyxl?]
*   **Google Sheets API:** [TODO: If applicable for future features]

### Infrastructure & DevOps
*   **Cloud Provider:** AWS
*   **Infrastructure as Code:** [TODO: Serverless Framework / AWS CDK / SAM / Terraform?]
*   **CI/CD:** [TODO: GitHub Actions / AWS CodePipeline / Other?]
*   **Secrets Management:** AWS Secrets Manager
*   **Monitoring:** [TODO: CloudWatch / Sentry / DataDog?]
*   **Logging:** [TODO: CloudWatch Logs / Custom solution?]

## 3. USER ROLES
*Based on authentication flows and architectural design.*

### **Admin (Super Admin)**
*   **Access:** Full system access.
*   **Capabilities:**
    *   Upload/Edit JSON configuration rules (Validation, Processing, Job Creation) via copy-paste interface.
    *   Export system Activity Logs (CSV).
    *   Manage user access (MVP: likely handled via hardcoded list or simple flag in DB).

### **General User**
*   **Access:** Standard operational access.
*   **Capabilities:**
    *   Create/Select Campaigns.
    *   Upload Media Plans (Excel).
    *   Run generation processes.
    *   View and edit the "Deliverables List" table (UI).
    *   Export final Deliverables (Excel) and Monday.com Jobs (CSV).
*   **Restriction:** Cannot edit underlying business rules (JSON).

### **Authentication Flow**
*   **MVP:** Email/Password login or Google SSO via AWS Cognito.
*   **Future:** Full Google Workspace integration.

## 4. KEY DATA MODELS/ENTITIES
*Derived from DynamoDB Schema and Business Rules.*

### **Campaign / Project**
*   **PK:** `PROJECT#<projectId>`
*   **Fields:** 
    *   Client Name
    *   Campaign Name
    *   Project Code
    *   Season
    *   Delivery Date
    *   Live Date
    *   Status (Draft, Processing, Completed)
*   **Business Rule:** One Campaign = One Media Plan file (MVP).
*   **Relationships:** Has many Deliverables.

### **Media Spec (Input)**
*   **Source:** Excel Tab "MEDIA SPECS".
*   **Key Fields:** 
    *   Markets (e.g., "UK, FR")
    *   Languages
    *   Channel Type
    *   Duration
    *   Aspect Ratio
    *   Resolution
*   **Business Rule:** Rows containing "strikethrough", "delete", or "cancelled" must be skipped during processing.

### **Variant Map (Input)**
*   **Source:** Excel Tab "VARIANT MAP".
*   **Key Fields:** 
    *   Channel (Row header)
    *   Market (Column header)
    *   Creative Name
    *   Available Durations
*   **Business Rule:** Dynamic column mapping required (e.g., "Variants US/CA"). Column headers vary by client.

### **Deliverable (Output)**
*   **PK:** `DELIV#<projectId>#<deliverableId>`
*   **SK:** [TODO: Sort key pattern?]
*   **Fields:** 
    *   `Market` (e.g., UK)
    *   `Language` (e.g., en-GB)
    *   `Channel` (e.g., Paid Social)
    *   `Platform` (e.g., TikTok)
    *   `Creative_Name`
    *   `Duration` (e.g., 15s)
    *   `Aspect_Ratio` (e.g., 9:16)
    *   `Resolution`
    *   `File_Format` (e.g., mov)
    *   `Filename` (Generated via naming convention)
    *   `Status` (Pending, Generated, Exported)
*   **Key Business Logic:** 
    *   **US Exclusion:** US Market (en-US) is *always* excluded from deliverables.
    *   **Meta 9:16 Split:** If Platform is Meta AND Ratio is 9:16, generate *two* deliverables:
        *   `IG_FB_Story`
        *   `IG_FB_Reel`

### **Rule Set (Configuration)**
*   **Format:** JSON
*   **Storage:** [TODO: S3 / DynamoDB / Both?]
*   **Scope:** Per Client (initially)
*   **Types:** 
    *   Validation Rules (data quality checks)
    *   Deliverables Generation Rules (business logic)
    *   Job List Rules (Monday.com formatting)
*   **Versioning:** [TODO: How are rule changes tracked/versioned?]

### **Activity Log**
*   **Purpose:** Audit trail of user actions
*   **Fields:** [TODO: User, Action, Timestamp, Project ID, Details?]
*   **Export:** CSV format for Admin users

## 5. STANDARD PATTERNS

### Frontend Patterns
*   **Component Structure:** [TODO: e.g., `src/components/{feature}/{ComponentName}.tsx`?]
*   **Page Structure:** [TODO: e.g., `src/pages/{route-name}/index.tsx`?]
*   **API Calls:** [TODO: Axios / Fetch / React Query hooks?]
*   **File Organization:** [TODO: Folder structure pattern?]
    ```
    [TODO: Example structure]
    src/
      components/
      pages/
      hooks/
      utils/
      services/
    ```

### Backend / Lambda Patterns
*   **Function Organization:** [TODO: One function per endpoint? Monolithic? Microservices?]
*   **Code Structure:** [TODO: Controller → Service → Repository pattern?]
*   **File Naming:** [TODO: Convention for Lambda functions?]
*   **Folder Structure:** [TODO: Example]
    ```
    [TODO: Example structure]
    lambdas/
      upload-media-plan/
      process-deliverables/
      export-jobs/
    ```

### API Conventions
*   **Base URL:** [TODO: e.g., `/api/v1/` or custom domain?]
*   **Endpoint Pattern:** [TODO: RESTful? Resource-based?]
*   **Request Format:**
    *   Content-Type: [TODO: application/json for most? multipart/form-data for uploads?]
    *   Authentication: `Authorization: Bearer <token>` (Cognito JWT)
*   **Response Format (Success):**
    ```json
    {
      "success": true,
      "data": { ... }
    }
    ```
*   **Response Format (Error):**
    ```json
    {
      "error": "ERROR_CODE",
      "message": "Human-readable error message",
      "details": [ ... ]  // Optional: field-level errors
    }
    ```
*   **Common Error Codes:** [TODO: Document standard codes]
    *   `VALIDATION_ERROR` - 400
    *   `UNAUTHORIZED` - 401
    *   `FORBIDDEN` - 403
    *   `NOT_FOUND` - 404
    *   `SERVER_ERROR` - 500

### Error Handling
*   **Frontend:** [TODO: Toast notifications? Error boundaries? How are API errors displayed?]
*   **Backend:** [TODO: Global error middleware? Try-catch patterns? Logging?]
*   **Retry Logic:** [TODO: Automatic retry on failure? User-initiated retry?]

### Excel Processing Pattern
*   **Library:** [TODO: Which library is used?]
*   **Validation Steps:** [TODO: Tab existence check → Header validation → Data validation?]
*   **Error Reporting:** [TODO: Row-level errors? Summary errors?]

## 6. NON-FUNCTIONAL REQUIREMENTS

### Performance
*   **Processing Time:** Sub-5 minutes for typical media plans (target)
*   **Concurrency:** Low volume (~5-10 concurrent internal users)
*   **File Upload:** [TODO: Max upload time target?]
*   **API Response Time:** [TODO: Target response time for typical operations?]
*   **Database Queries:** [TODO: Target query performance?]

### Security
*   **Identity & Access:** AWS Cognito (Email/Password + Google SSO)
*   **API Authentication:** JWT tokens from Cognito
*   **Secrets Management:** API keys and service account credentials stored in AWS Secrets Manager
*   **Data Isolation:** Single DynamoDB table per domain (ProjectConfig, Deliverables, etc.)
*   **File Upload Security:** [TODO: Virus scanning? File type validation? Size limits?]
*   **Input Sanitization:** [TODO: How is user input validated/sanitized?]
*   **HTTPS:** [TODO: Enforced on all endpoints?]

### Accessibility
*   **Requirement Level:** [TODO: WCAG 2.1 AA? Lower priority for internal tool?]
*   **Keyboard Navigation:** [TODO: Required? To what extent?]
*   **Screen Reader Support:** [TODO: Required for internal tool?]
*   **Color Contrast:** [TODO: Minimum contrast ratio requirements?]

### Browser/Device Support
*   **Browsers:** [TODO: Chrome / Firefox / Safari / Edge? Latest 2 versions?]
*   **Browser Versions:** [TODO: Specific version requirements?]
*   **Mobile Support:** [TODO: Mobile responsive? Desktop-only internal tool?]
*   **Operating Systems:** [TODO: Windows / Mac / Linux support?]

### Monitoring & Logging
*   **Application Monitoring:** [TODO: CloudWatch / Sentry / DataDog?]
*   **Error Tracking:** [TODO: How are production errors tracked?]
*   **Performance Monitoring:** [TODO: Lambda execution metrics?]
*   **User Activity Logging:** Activity Logs stored in DynamoDB, exportable by Admins

### Scalability
*   **Current Scale:** 5-10 concurrent internal users
*   **Future Scale:** [TODO: Expected growth?]
*   **Auto-scaling:** [TODO: Lambda auto-scales, but any limits configured?]

## 7. PROJECT-SPECIFIC CONFIGURATIONS

### File Upload Constraints
*   **Format:** `.xlsx` only (Excel 2007+ format)
*   **Structure Requirements:** 
    *   Must contain two specific tabs: `VARIANT MAP` and `MEDIA SPECS`
    *   Tab names must match exactly (case-sensitive?)
*   **Max File Size:** [TODO: e.g., 10MB? 50MB?]
*   **Validation Steps:**
    1. Check file extension is `.xlsx`
    2. Verify tab existence
    3. Validate column headers
    4. [TODO: Additional validation steps?]

### Naming Convention (Automated Filename Generation)
*   **Pattern:** `{DeliveryDate}_{ProjectCode}_{Season}_{Language}_{Creative}_{Duration}_{AspectRatio}_{FileFormat}_{Platform}`
*   **Example:** `20250704_Blue_Summer_en-GB_Blue3_15s_9x16_mov_TikTok`
*   **Date Format:** YYYYMMDD
*   **Separator:** Underscore (`_`)
*   **Case:** [TODO: Title Case? Lowercase? As-entered?]

### Export Formats

#### Deliverables Export (Excel)
*   **Format:** `.xlsx`
*   **Tabs:**
    1. Original Variant Map (preserved from input)
    2. Original Media Specs (preserved from input)
    3. Generated Deliverables (system output)
*   **Deliverables Tab Columns:** [TODO: Specific column order/names?]

#### Monday.com Jobs Export (CSV)
*   **Format:** `.csv`
*   **Encoding:** [TODO: UTF-8? UTF-8 BOM?]
*   **Delimiter:** [TODO: Comma? Semicolon?]
*   **Column Mapping:** [TODO: Map Draper fields to Monday.com columns?]
*   **Row Format:** [TODO: One job per row? Header row included?]

### Business Rules Configuration
*   **Storage:** JSON format
*   **Access:** Admin users only (via copy-paste interface in UI)
*   **Structure:** [TODO: Schema/example of rule JSON?]
*   **Versioning:** [TODO: How are changes tracked? Rollback capability?]
*   **Validation:** [TODO: JSON schema validation before saving?]

### Ticket/Issue Numbering Convention

**Format:** `[PREFIX]-[NUMBER]`

**Components:**
- **PREFIX**: 2-10 character project code (configurable per project)
  - Examples: `DR`, `DRAPER`, `PRD`, `AUTH`
  - Typically 2-3 characters for brevity
  - Uppercase recommended for consistency
  - Defined at project inception

- **NUMBER**: Zero-padded sequential number
  - Format: `01`, `02`, `03`... `99`
  - For 100+ issues: `100`, `101`, `102`...
  - Sequential across entire project

**Examples:**
- `DR-01` - First ticket for "DR" project
- `DRAPER-42` - 42nd ticket for "DRAPER" project
- `AUTH-05` - 5th ticket for "AUTH" project

**Issue Title Format:**
```
[PREFIX]-[NUMBER] [Feature Name] - [Story Type]
```

**Examples:**
- `DR-01 Google SSO Authentication - Backend`
- `DR-02 View All Campaigns - Frontend`
- `DR-03 Review Deliverables Table - Full Stack`
- `DRAPER-15 Upload JSON Rules - Backend`

**Split Stories (Frontend/Backend separated):**
- Option A: Sequential numbering
  - `DR-29` Review Deliverables - Backend
  - `DR-30` Review Deliverables - Frontend
  
- Option B: Suffix notation (when explicit FE/BE linking needed)
  - `DR-29-BE` Review Deliverables - Backend
  - `DR-29-FE` Review Deliverables - Frontend

**Labels Convention:**
- Always include: `user-story`, `[epic-name]`, `priority-[level]`, `[story-type]`
- Examples: 
  - `["user-story", "authentication", "priority-high", "backend"]`
  - `["user-story", "deliverables", "priority-medium", "full-stack"]`

**Bug Format:** [TODO: BUG-[PREFIX]-## or same as features?]
**Tech Debt Format:** [TODO: TECH-[PREFIX]-## or same?]

**Configuration Location:**
- Ticket prefix is defined in `.github/ISSUE_TEMPLATE/user-story.yml`
- AI assistants request prefix during session setup
- Stored in PROJECT_CONTEXT.md for reference

## 8. RELATED DOCUMENTATION
*   **Architecture Diagram:** See "Initial Arch Design" - Mermaid Graph TD [TODO: Add link or embed]
*   **Business Rules Logic:** See "Complete Media Plan Deliverables Generation Rules" [TODO: Add link]
*   **UX/UI Flows:** See Figma file - Project Draper UX Workshop [TODO: Add Figma link]
*   **DynamoDB Schema:** See "Domains & Entities" table in Arch Design [TODO: Add link or embed]
*   **API Documentation:** [TODO: Swagger/OpenAPI spec? Postman collection?]
*   **Deployment Guide:** [TODO: Link to deployment documentation?]
*   **Development Setup:** [TODO: README with local dev setup?]
*   **Issue Templates:** `.github/ISSUE_TEMPLATE/user-story.yml` - GitHub issue template for user stories
*   **AI Issue Creator:** `.github/AI_ISSUE_CREATOR_PROMPT.md` - AI assistant prompt for automated issue creation

---

## How to Use This File

### For Business Analysts
When creating GitHub issues:
1. Reference relevant sections (Tech Stack, User Roles, Data Models) in your Copilot prompts
2. Copy specific patterns/conventions into issue Technical Context sections
3. Use naming conventions and export formats in acceptance criteria
4. Use the ticket numbering format: `[PREFIX]-[NUMBER]` (get PREFIX from project lead)

### For Developers
1. Fill in `[TODO: ...]` placeholders as implementation details are finalized
2. Update this file when architecture/patterns change
3. Use as single source of truth for project standards
4. Reference ticket prefix when creating manual issues

### For AI Assistants
1. Read this file before creating any issues
2. Extract tech stack, data models, patterns, and conventions
3. Use ticket numbering format specified in section 7
4. Auto-generate labels based on epic name, priority, and story type
5. Infer dependencies based on epic relationships

### Maintenance
*   **Owner:** [TODO: Who maintains this file?]
*   **Update Frequency:** [TODO: On major architecture changes? Sprint reviews?]
*   **Last Updated:** [TODO: Date]