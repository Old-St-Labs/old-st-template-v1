# Copilot Instructions for Project Draper

## Context Router - Start Here

**First**: Read `AI_CONTEXT_ROUTER.md` to determine which specialized guide to use based on request type.

**Available Guides:**
- `AI_ISSUE_CREATOR_PROMPT.md` - Interactive GitHub issue creation
- `AI_CODE_DOCUMENTATION_PROMPT.md` - Code documentation standards
- `PROJECT_CONTEXT.md` - Project knowledge base (tech stack, data models, patterns)
- `ISSUE_CREATION_GUIDE.md` - Detailed issue creation workflows
- `QUICK_START_BA.md` - BA onboarding and quick reference

## Project-Specific Patterns

### Tech Stack
- **Backend:** AWS Lambda (Node.js/TypeScript), NestJS framework
- **Database:** DynamoDB (single-table design with domain-based partition keys)
- **Storage:** AWS S3 for Excel files
- **Auth:** AWS Cognito (Email/Password + Google SSO)
- **Integrations:** Monday.com (CSV export), AWS SQS, AWS Secrets Manager

### Naming Conventions
- **Issues:** `DRAPER-##` (e.g., DRAPER-42)
- **Files:** Deliverables follow: `{DeliveryDate}_{ProjectCode}_{Season}_{Language}_{Creative}_{Duration}_{AspectRatio}_{FileFormat}_{Platform}`
- **Services:** `{feature}.service.ts` (e.g., `monday-grouping.service.ts`)

### Code Organization
- **NestJS Services:** Use dependency injection, document with JSDoc
- **AWS Integrations:** Centralize S3/SQS/DynamoDB access in dedicated services
- **Business Logic:** Document complex rules referencing source documents

### Critical Business Rules
- **US Market Exclusion:** en-US deliverables are ALWAYS excluded
- **Meta 9:16 Split:** Generate separate `IG_FB_Story` and `IG_FB_Reel` deliverables
- **Excel Validation:** Skip rows with "strikethrough", "delete", or "cancelled"
- **Dynamic Columns:** Variant Map headers vary by client (e.g., "Variants US/CA")

### API Conventions
- **Success Response:** `{ "success": true, "data": {...} }`
- **Error Response:** `{ "error": "ERROR_CODE", "message": "...", "details": [...] }`
- **Auth Header:** `Authorization: Bearer <Cognito JWT>`
- **Error Codes:** `VALIDATION_ERROR`, `UNAUTHORIZED`, `FORBIDDEN`, `NOT_FOUND`, `SERVER_ERROR`

## Documentation Approach

- **Public Services/APIs:** Comprehensive JSDoc with examples
- **Business Logic:** Explain WHY (rules from "Media Plan Rules" doc)
- **Complex Algorithms:** Document approach and performance considerations
- **AWS Integrations:** Note retry logic, error handling, and resource limits
- **Skip:** Obvious operations, type information (TypeScript handles this)

## Workflow

### When Asked to Create Issue
1. Read `PROJECT_CONTEXT.md` for domain knowledge
2. Follow `AI_ISSUE_CREATOR_PROMPT.md` workflow
3. Use `DRAPER-##` ticket format
4. Include relevant business rules in acceptance criteria

### When Asked to Document Code
1. Check code visibility (public API vs. internal)
2. Apply `AI_CODE_DOCUMENTATION_PROMPT.md` decision tree
3. Focus on business context, not obvious mechanics
4. Reference "Media Plan Rules" doc when documenting business logic

### When Implementing Features
1. Follow NestJS patterns (services, controllers, DTOs)
2. Use dependency injection for AWS services
3. Document as you implement (JSDoc for public methods)
4. Handle errors per API conventions above
5. Consider PROJECT_CONTEXT.md for data models and patterns

## Key Files to Reference

- **Tech Details:** `PROJECT_CONTEXT.md` (Section 2: Tech Stack)
- **Data Models:** `PROJECT_CONTEXT.md` (Section 4: Entities)
- **API Standards:** `PROJECT_CONTEXT.md` (Section 5: API Conventions)
- **Business Rules:** Reference "Complete Media Plan Deliverables Generation Rules"
- **Issue Templates:** `.github/ISSUE_TEMPLATE/user-story.yml`

## Quick Reminders

✅ Document WHY, not WHAT  
✅ Use existing guides for detailed workflows  
✅ Reference PROJECT_CONTEXT.md for all domain knowledge  
✅ Follow DRAPER-## ticket format  
✅ Apply US exclusion and Meta 9:16 split rules  
✅ Validate Excel inputs per business rules  

🚫 Don't create generic solutions - use project-specific context  
🚫 Don't skip error handling - AWS integrations need retries  
🚫 Don't over-document - see AI_CODE_DOCUMENTATION_PROMPT.md decision tree  

---

**For comprehensive guidance**, always start with `AI_CONTEXT_ROUTER.md` to route to the right specialized guide.
