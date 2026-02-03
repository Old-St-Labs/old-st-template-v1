# NotebookLM Project Context Extraction Prompt

> **Purpose:** Use this prompt in NotebookLM to extract comprehensive project context from your source documents for GitHub issue creation.

---

## 📋 Compact Prompt for NotebookLM (Character-Limit Friendly)

> **Use this shorter version if hitting paste limits**

```
Analyze all uploaded documents and create a PROJECT_CONTEXT.md with these 8 sections:

## 1. PROJECT OVERVIEW
- Project Name, Purpose (1-2 sentences), Description (2-4 sentences)
- Repository URL, Key Source Documents

## 2. TECH STACK
Extract and categorize: Frontend (framework, language, styling, UI library, state mgmt, forms), Backend (runtime, language, framework, API type, gateway), Database (type, schema design, ORM), File Storage (service, purpose), Auth (provider, methods, token type), APIs/Integrations, Infrastructure (cloud, IaC, CI/CD, monitoring)

## 3. USER ROLES
For each role: Name, Access Level, Capabilities, Restrictions, Auth Requirements

## 4. KEY DATA MODELS/ENTITIES
For each entity: Name, PK/SK, Key Fields (with types), Business Rules, Relationships, Status States

## 5. STANDARD PATTERNS
- Frontend: component structure, folder org, API patterns
- Backend: function org, code structure, error handling
- API: base URL, endpoints, request/response format (JSON examples), auth headers, error codes
- Naming: files, variables, DB tables, constants
- Error Handling: frontend display, backend logging, retry logic

## 6. NON-FUNCTIONAL REQUIREMENTS
Performance (targets, concurrent users), Security (auth, encryption, compliance), Accessibility (WCAG, keyboard nav), Browser/Device Support, Monitoring/Logging, Scalability

## 7. PROJECT-SPECIFIC CONFIGURATIONS
File Upload (formats, limits, validation), Automated Patterns (naming, templates, workflows), Export Formats (types, mappings), Business Rules (storage, access, versioning), Ticket Management (numbering, labeling), Domain-Specific Rules (validation, exclusions, edge cases)

## 8. RELATED DOCUMENTATION
List: architecture diagrams, BRDs, design files, API docs, deployment guides, runbooks

**EXTRACTION RULES:**
- Use `[TODO: specific question?]` for missing info
- Look for: "must", "should", "always", "never" for business rules
- Include specific examples, versions, configurations
- Prioritize actionable, concrete details over general descriptions

Output as markdown with clear headers, bullets, code blocks for examples, and [TODO] markers.
```

---

## 📋 Full Prompt for NotebookLM (If No Character Limit)

> **Use this detailed version if you can paste longer prompts**

```
Please analyze all uploaded source documents and create a comprehensive PROJECT CONTEXT document following this exact structure. Extract and organize information into these 8 sections:

---

## 1. PROJECT OVERVIEW

Extract and document:
- **Project Name:** Official project name
- **Purpose:** What problem does this solve? (1-2 sentences)
- **Description:** Detailed explanation of what the system does (2-4 sentences)
- **Repository URL:** GitHub repository location (if mentioned)
- **Key Source Documents:** List all relevant technical specifications, design documents, or business requirements documents

---

## 2. TECH STACK

Identify and categorize all technologies mentioned:

### Frontend
- Framework & Version (React, Vue, Next.js, Angular, etc.)
- Language & Version (TypeScript, JavaScript)
- Styling approach (Tailwind, CSS Modules, Styled Components, Material-UI)
- UI Component Library (shadcn/ui, Ant Design, Material-UI, Bootstrap, custom)
- State Management (Redux, Zustand, React Query, Context API, Vuex)
- Form Handling (React Hook Form, Formik, VeeValidate)
- File Upload library (if applicable)
- Routing library (React Router, Next.js router, Vue Router)

### Backend
- Runtime & Version (Node.js, Python, Java, .NET, Go)
- Language & Version (TypeScript, JavaScript, Python 3.x, Java 17)
- Framework (NestJS, Express, FastAPI, Django, Spring Boot)
- API Type (REST, GraphQL, gRPC)
- API Gateway (AWS API Gateway, Azure API Management, Kong)
- Serverless framework (if applicable - AWS Lambda, Azure Functions)

### Database
- Primary Database (PostgreSQL, MySQL, MongoDB, DynamoDB, etc.)
- Schema Design approach (normalized, denormalized, single-table, multi-table)
- Caching layer (Redis, Memcached, ElastiCache)
- Database ORM/ODM (Prisma, TypeORM, Mongoose, Sequelize)

### File Storage
- Service (AWS S3, Azure Blob Storage, Google Cloud Storage)
- Purpose (document storage, media files, backups)
- Bucket/Container structure

### Authentication & Authorization
- Provider (AWS Cognito, Auth0, Firebase Auth, custom)
- Methods (Email/Password, OAuth, SSO, MFA)
- Token Type (JWT, OAuth 2.0, session-based)
- Role-based access control (RBAC) approach

### APIs & Integrations
- Third-party integrations (payment gateways, CRM, email services)
- External APIs used
- Webhooks (incoming/outgoing)
- Data synchronization services

### Infrastructure & DevOps
- Cloud Provider (AWS, Azure, GCP, on-premise)
- Infrastructure as Code (Terraform, AWS CDK, CloudFormation, Pulumi)
- CI/CD Pipeline (GitHub Actions, Jenkins, GitLab CI, CircleCI)
- Secrets Management (AWS Secrets Manager, Azure Key Vault, HashiCorp Vault)
- Monitoring & Logging (CloudWatch, Datadog, New Relic, Sentry)
- Container Orchestration (if applicable - Kubernetes, ECS, Docker Compose)

---

## 3. USER ROLES

For each user role mentioned, document:
- **Role Name:** (e.g., Admin, User, Manager, Guest)
- **Access Level:** (Full, Standard, Read-only, etc.)
- **Capabilities:** List all actions this role can perform
- **Restrictions:** What this role CANNOT do
- **Authentication Requirements:** How they log in

Include authentication flow details (login methods, token management).

---

## 4. KEY DATA MODELS/ENTITIES

For each entity or data model, extract:
- **Entity Name:** (e.g., User, Order, Campaign, Application)
- **Primary Key (PK):** Database identifier pattern
- **Sort Key (SK):** If applicable (for DynamoDB, etc.)
- **Key Fields:** List all important attributes with their data types
- **Business Rules:** Any validation rules, constraints, or business logic
- **Relationships:** How this entity relates to others (one-to-many, many-to-many)
- **Status/State Machine:** If the entity has different states (Draft, Pending, Approved, etc.)

Look for:
- Input data structures (forms, uploads, API requests)
- Output data structures (reports, exports, responses)
- Configuration structures (settings, rules, templates)
- Audit/logging structures

---

## 5. STANDARD PATTERNS & CONVENTIONS

### Frontend Patterns
- Component file structure and naming
- Page/route organization
- API call patterns (hooks, services, utilities)
- Folder organization example
- Code formatting standards

### Backend/API Patterns
- Function/endpoint organization
- Code structure (Controller-Service-Repository, MVC, etc.)
- File naming conventions
- Folder structure example
- Error handling patterns

### API Conventions
- Base URL pattern
- Endpoint naming (RESTful resource-based, RPC-style, etc.)
- Request format (Content-Type, headers required)
- Authentication header format
- Success response structure (with example JSON)
- Error response structure (with example JSON)
- Standard HTTP status codes used
- Common error codes and their meanings

### Naming Conventions
- File naming patterns
- Variable/function naming style (camelCase, snake_case, PascalCase)
- Database table/collection naming
- Constants naming
- Environment variable naming

### Error Handling
- Frontend error display approach
- Backend error logging and reporting
- Retry logic patterns
- User-facing error messages vs technical logs

---

## 6. NON-FUNCTIONAL REQUIREMENTS

### Performance
- Processing time targets
- Expected concurrent users
- API response time targets
- Database query performance goals
- File upload/download time targets

### Security
- Authentication mechanisms
- Authorization approach
- API security (rate limiting, CORS, input validation)
- Secrets management
- Data encryption (at rest, in transit)
- Input sanitization approach
- Security compliance requirements (GDPR, HIPAA, SOC2, etc.)

### Accessibility
- WCAG compliance level (if specified)
- Keyboard navigation requirements
- Screen reader support
- Color contrast requirements
- Internationalization/Localization needs

### Browser/Device Support
- Supported browsers and versions
- Mobile responsiveness requirements
- Operating system compatibility
- Progressive Web App (PWA) features

### Monitoring & Logging
- Application monitoring tools
- Error tracking approach
- Performance monitoring metrics
- User activity logging requirements
- Log retention policies

### Scalability
- Current scale (users, data volume)
- Expected future scale
- Auto-scaling configuration
- Database scaling strategy

---

## 7. PROJECT-SPECIFIC CONFIGURATIONS

Document any unique project requirements:

### File Upload/Processing
- Accepted file formats
- File size limits
- File structure requirements
- Validation steps
- Processing workflow

### Automated Patterns
- Naming conventions for generated files/records
- Template structures
- Automated workflows
- Scheduled jobs/cron tasks

### Export Formats
- Export file types (CSV, Excel, PDF, JSON)
- Column/field mappings
- Formatting requirements
- Encoding standards

### Business Rules Configuration
- How rules are stored (JSON, database, code)
- Who can modify rules
- Rule structure/schema
- Validation approach
- Versioning strategy

### Ticket/Issue Management
- Ticket numbering format
- Issue title format
- Labeling conventions
- Epic/milestone organization
- Bug/feature/tech debt formats

### Domain-Specific Rules
- Industry-specific requirements
- Compliance rules
- Data validation rules
- Business logic constraints
- Exclusion rules
- Special cases or edge cases

---

## 8. RELATED DOCUMENTATION

List all referenced documents:
- Architecture diagrams
- Business requirements documents
- UX/UI design files (Figma, Sketch links)
- Database schema documentation
- API documentation (Swagger, Postman)
- Deployment guides
- Development setup guides
- Testing documentation
- Issue templates
- Runbooks

---

## EXTRACTION GUIDELINES

**When information is NOT found:**
- Mark as `[TODO: ...]` with a specific question
- Example: `[TODO: Which state management library - Redux or Zustand?]`

**When information is PARTIALLY found:**
- Document what you found
- Add `[TODO: ...]` for missing details
- Example: "Database: PostgreSQL [TODO: Version and cluster configuration?]"

**When extracting business rules:**
- Look for words like: "must", "should", "always", "never", "required", "forbidden"
- Document exact conditions and exceptions
- Include examples if provided

**When finding patterns:**
- Look for repeated structures in code examples
- Note consistent naming across documents
- Document any explicit conventions mentioned

**Priority for extraction:**
- Focus on actionable, concrete information
- Prefer specific examples over general descriptions
- Include version numbers and exact configurations
- Document exceptions and edge cases

---

## OUTPUT FORMAT

Please structure your response as a markdown document with:
1. Clear section headers (## 1. PROJECT OVERVIEW, etc.)
2. Bullet points and sub-bullets for organization
3. Code blocks for examples (```json, ```typescript, etc.)
4. `[TODO: ...]` markers for missing information
5. Concrete examples wherever possible

This document will be used by AI assistants to automatically generate detailed GitHub issues, so precision and completeness are critical.
```

---

## 📖 How to Use This Prompt

### Step 1: Upload Documents to NotebookLM
Upload all relevant project documents:
- ✅ Technical specifications
- ✅ Architecture diagrams
- ✅ Business requirements documents (BRDs)
- ✅ API documentation
- ✅ Design files (exported as PDF if needed)
- ✅ Database schema documentation
- ✅ Meeting notes with technical decisions
- ✅ Existing README files
- ✅ Code style guides

### Step 2: Copy & Paste the Prompt
Copy the entire prompt section above (from "Please analyze..." to the end) into NotebookLM's chat interface.

### Step 3: Review & Refine Output
- NotebookLM will generate a structured PROJECT_CONTEXT document
- Review for completeness
- Ask follow-up questions for `[TODO]` items:
  - "What framework is mentioned for the frontend?"
  - "Are there any database schema details?"
  - "What authentication methods are documented?"

### Step 4: Save to Repository
1. Create or replace `.github/PROJECT_CONTEXT.md` with the output
2. Fill in any remaining `[TODO]` items based on team knowledge
3. Commit to your repository

### Step 5: Use with Issue Creator
Your AI Issue Creator will now have comprehensive project context to:
- ✅ Auto-detect relevant entities and data models
- ✅ Apply correct naming conventions
- ✅ Reference appropriate tech stack
- ✅ Include project-specific business rules
- ✅ Generate accurate acceptance criteria

---

## 💡 Pro Tips

**For Best Results:**
1. **Upload comprehensive sources** - More context = better extraction
2. **Include examples** - Code samples, API examples, and screenshots help
3. **Ask iterative questions** - Refine the output by asking NotebookLM follow-ups
4. **Combine with existing docs** - If you have partial PROJECT_CONTEXT, ask NotebookLM to "fill in the missing sections"
5. **Update regularly** - Re-run extraction when project architecture changes

**Follow-Up Questions to Ask NotebookLM:**
- "What business rules or validation logic did you find?"
- "Are there any special cases or exclusions mentioned?"
- "What error handling patterns are described?"
- "List all API endpoints or routes mentioned"
- "What third-party integrations are referenced?"

---

## 🔄 Maintenance

**When to Re-run Extraction:**
- ✓ Major architecture changes
- ✓ New features with different patterns
- ✓ Tech stack upgrades
- ✓ New integrations added
- ✓ Business rule changes

**Version Control:**
- Keep old versions: `PROJECT_CONTEXT_v1.md`, `PROJECT_CONTEXT_v2.md`
- Or use git history to track changes
- Date your updates: `Last Updated: 2026-02-03`

---

## Example NotebookLM Follow-Ups

After initial extraction, refine with:

```
"Can you expand section 4 (Data Models) with more detail about relationships between entities?"

"What validation rules did you find in the documents? Add them to the Business Rules section."

"List all file formats mentioned (for uploads, exports, etc.) and add to section 7."

"What monitoring and logging tools are referenced? Update section 6."

"Find all API endpoint patterns and document the standard response format in section 5."
```

---

**Remember:** The more comprehensive your PROJECT_CONTEXT, the better your AI-generated GitHub issues will be! 🚀
