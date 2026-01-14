# AI Context Router & General Chat Instructions

## Purpose
This document serves as the **master decision tree** for AI assistants working in this repository. It helps determine which specialized guide to reference based on conversation context and ensures consistent, appropriate responses across different types of requests.

---

## How to Use This Guide

**For AI Assistants:**
1. **First**: Read the user's request and identify its primary intent
2. **Then**: Use the decision tree below to determine which guide(s) to reference
3. **Finally**: Apply the appropriate guide while maintaining awareness of project context

**For Developers:**
- Reference this when asking AI for help to get better, more contextual responses
- Update this when adding new guides or changing workflows

---

## Decision Tree: Which Guide to Use?

### 1️⃣ **Is the request about creating GitHub issues?**

**Indicators:**
- Keywords: "create issue", "add issue", "new issue", "issue template"
- User wants to document a task, bug, feature, or user story
- Discussion about issue structure, labels, or assignments

**→ Use:** `AI_ISSUE_CREATOR_PROMPT.md`  
**→ Also Reference:** `ISSUE_CREATION_GUIDE.md`, `ISSUE_TEMPLATE/user-story.yml`  
**→ Context Needed:** `PROJECT_CONTEXT.md` for domain understanding

**Special Considerations:**
- Always validate against issue template requirements
- Check if issue type matches available templates
- Consider project-specific labels and workflows

---

### 2️⃣ **Is the request about documenting code?**

**Indicators:**
- Keywords: "document this code", "add comments", "JSDoc", "docstring", "explain this function"
- User provides code blocks asking for documentation
- Questions about comment style, documentation standards
- Requests to improve existing documentation

**→ Use:** `AI_CODE_DOCUMENTATION_PROMPT.md`

**Apply These Principles:**
- Follow the decision tree (Always/Sometimes/Never document)
- Use language-appropriate format (JSDoc for JS/TS, Docstrings for Python)
- Focus on WHY over WHAT
- Skip obvious documentation
- Document public APIs comprehensively

**Special Considerations:**
- Check if code is public API (needs more docs) vs. internal (minimal docs)
- Identify complex business logic requiring explanation
- Note any non-obvious decisions or gotchas

---

### 3️⃣ **Is the request about project setup or onboarding?**

**Indicators:**
- Keywords: "how do I start", "setup", "getting started", "onboarding"
- Questions about project structure, dependencies, or configuration
- New team member trying to understand the project

**→ Use:** `QUICK_START_BA.md` (if user is Business Analyst role)  
**→ Use:** `README.md` (for general project overview)  
**→ Reference:** `PROJECT_CONTEXT.md` for background

**Special Considerations:**
- Tailor response to user's role (BA, developer, QA, etc.)
- Point to specific sections rather than overwhelming with all docs
- Highlight prerequisites and common gotchas

---

### 4️⃣ **Is the request about understanding workflows or processes?**

**Indicators:**
- Keywords: "how does", "workflow", "process", "flow", "lifecycle"
- Questions about how different components interact
- Requests for visual representations or step-by-step explanations

**→ Use:** `WORKFLOW_VISUAL.md`  
**→ Reference:** `PROJECT_CONTEXT.md` for context

**Special Considerations:**
- Provide both high-level overview and detailed steps
- Mention key integration points
- Reference related workflows when applicable

---

### 5️⃣ **Is the request about general project understanding?**

**Indicators:**
- Keywords: "what is this project", "what does it do", "architecture"
- Questions about business purpose, goals, or domain
- High-level conceptual questions

**→ Use:** `PROJECT_CONTEXT.md` as primary source  
**→ Use:** `README.md` for technical overview

**Special Considerations:**
- Start with business context before diving into technical details
- Connect technical decisions to business requirements
- Reference specific sections of PROJECT_CONTEXT.md

---

### 6️⃣ **Is the request about code implementation (not documentation)?**

**Indicators:**
- User asking to write new code, refactor existing code, fix bugs
- Implementation requests without specific mention of documentation
- Technical problem-solving

**→ Primary Focus:** Implement the solution  
**→ Secondary:** Apply `AI_CODE_DOCUMENTATION_PROMPT.md` to new/modified code  
**→ Reference:** `PROJECT_CONTEXT.md` for domain knowledge

**Special Considerations:**
- Document as you implement (don't skip this step)
- Follow existing code patterns in the project
- Ask clarifying questions if requirements are ambiguous

---

### 7️⃣ **Multiple contexts apply?**

**When request spans multiple areas:**
- Example: "Create an issue for documenting this service"
- Example: "Implement this feature and create tracking issue"

**→ Strategy:**
1. Identify primary action (implementation vs. issue creation vs. documentation)
2. Apply primary guide first
3. Reference secondary guides as needed
4. Maintain consistency across outputs

**Prioritization Order:**
1. Implementation/Action items (do the work)
2. Documentation (explain the work)
3. Issue tracking (record the work)
4. Process adherence (follow the workflow)

---

## Context Awareness Rules

### Always Consider:

1. **Project Context** (`PROJECT_CONTEXT.md`)
   - What domain are we in? (Media planning, campaign management, etc.)
   - What are the business goals?
   - Who are the stakeholders?

2. **User's Role**
   - Developer → Focus on technical details, code quality
   - Business Analyst → Focus on requirements, workflows, user stories
   - Product Manager → Focus on features, priorities, outcomes
   - QA/Tester → Focus on test cases, edge cases, validation

3. **Conversation History**
   - Has user mentioned specific components before?
   - Are we continuing a previous discussion?
   - Has context been established that affects this request?

4. **Repository State**
   - Are there existing patterns to follow?
   - What conventions are already in use?
   - Are there related files that need updating?

---

## Response Quality Guidelines

### DO:

✅ **Start with understanding**
- Confirm you understand the request before acting
- Ask clarifying questions if context is missing

✅ **Reference appropriate guides explicitly**
- "Following the AI_CODE_DOCUMENTATION_PROMPT guidelines..."
- "According to ISSUE_CREATION_GUIDE, this should be..."

✅ **Provide context-aware responses**
- Tailor technical depth to user's apparent expertise
- Connect answers to project-specific context

✅ **Maintain consistency**
- Use established patterns from guides
- Follow project conventions
- Reference previous decisions when relevant

✅ **Be concise but complete**
- Answer the question directly
- Provide additional context when helpful
- Don't overwhelm with unnecessary information

### DON'T:

❌ **Don't mix conflicting guidance**
- If guides conflict, prioritize based on request type
- Explain any deviations from standard patterns

❌ **Don't ignore project context**
- Don't give generic answers when project-specific context exists
- Always check PROJECT_CONTEXT.md for domain knowledge

❌ **Don't over-document or under-document**
- Follow AI_CODE_DOCUMENTATION_PROMPT decision tree
- Skip obvious, add value where needed

❌ **Don't create unnecessary artifacts**
- Don't create new docs unless specifically requested
- Don't generate summary files after simple tasks

---

## Guide Priority Matrix

When multiple guides could apply, use this priority matrix:

| Request Type | Primary Guide | Secondary Guides | Context |
|--------------|---------------|------------------|---------|
| Create Issue | ISSUE_CREATOR | ISSUE_CREATION_GUIDE | PROJECT_CONTEXT |
| Document Code | CODE_DOCUMENTATION | - | - |
| Implement Feature | (Standard coding) | CODE_DOCUMENTATION, PROJECT_CONTEXT | All relevant |
| Fix Bug | (Standard coding) | CODE_DOCUMENTATION | PROJECT_CONTEXT |
| Explain Workflow | WORKFLOW_VISUAL | PROJECT_CONTEXT | - |
| Onboarding | QUICK_START_BA / README | PROJECT_CONTEXT | User role |
| Architecture Questions | PROJECT_CONTEXT | README | - |
| Process Questions | WORKFLOW_VISUAL | PROJECT_CONTEXT | - |

---

## Special Scenarios

### Scenario: User Provides Undocumented Code

**Decision Flow:**
1. Is user asking to document it? → Use CODE_DOCUMENTATION guide
2. Is user asking to fix/improve it? → Implement changes + document
3. Is user just sharing it? → Acknowledge, offer to document if helpful

### Scenario: Issue Already Exists for This Topic

**Decision Flow:**
1. Reference existing issue number
2. Suggest updating existing issue vs. creating new one
3. If creating new, explain relationship to existing issue

### Scenario: Request Conflicts with Project Standards

**Decision Flow:**
1. Acknowledge the request
2. Explain the conflict with project standards (reference guide)
3. Suggest alternative that aligns with standards
4. If user insists, document the deviation and rationale

### Scenario: Ambiguous or Unclear Request

**Decision Flow:**
1. Don't guess - ask clarifying questions
2. Offer multiple interpretations: "Did you mean X or Y?"
3. Wait for clarification before proceeding
4. Once clear, route to appropriate guide

---

## Quick Reference: Keyword → Guide Mapping

| Keywords | Route To |
|----------|----------|
| "create issue", "new issue", "user story" | ISSUE_CREATOR |
| "document", "JSDoc", "docstring", "comments" | CODE_DOCUMENTATION |
| "getting started", "setup", "onboarding" | QUICK_START_BA / README |
| "workflow", "process", "how does" | WORKFLOW_VISUAL |
| "what is", "context", "background" | PROJECT_CONTEXT |
| "implement", "build", "create feature" | Standard + CODE_DOCUMENTATION |
| "fix bug", "debug", "issue with" | Standard + PROJECT_CONTEXT |
| "explain code", "what does this do" | Analysis + CODE_DOCUMENTATION (if needed) |

---

## Example Routing Decisions

### Example 1: "Document this service class"

**Analysis:**
- Primary intent: Documentation
- Code type: Service class (likely public API)

**Routing:**
→ Primary: `AI_CODE_DOCUMENTATION_PROMPT.md`  
→ Apply: Comprehensive documentation (public API)  
→ Reference: `PROJECT_CONTEXT.md` for business context

**Response Strategy:**
1. Add class-level JSDoc explaining purpose
2. Document public methods with params, returns, examples
3. Add inline comments for complex logic
4. Skip obvious private methods

---

### Example 2: "Create an issue for the Monday grouping service"

**Analysis:**
- Primary intent: Issue creation
- Context: Existing service needs tracking

**Routing:**
→ Primary: `AI_ISSUE_CREATOR_PROMPT.md`  
→ Template: `ISSUE_TEMPLATE/user-story.yml`  
→ Context: `PROJECT_CONTEXT.md` for business understanding

**Response Strategy:**
1. Determine issue type (feature, bug, task, user story)
2. Follow template structure
3. Include acceptance criteria
4. Suggest appropriate labels
5. Reference related code/components

---

### Example 3: "How do I start working on this project as a BA?"

**Analysis:**
- Primary intent: Onboarding
- Role: Business Analyst

**Routing:**
→ Primary: `QUICK_START_BA.md`  
→ Reference: `PROJECT_CONTEXT.md`, `WORKFLOW_VISUAL.md`  
→ Context: BA-specific workflows

**Response Strategy:**
1. Point to QUICK_START_BA.md
2. Highlight BA-specific sections
3. Explain workflows relevant to BA role
4. Provide next steps

---

### Example 4: "Implement a new validation rule and create an issue for it"

**Analysis:**
- Primary intent: Implementation
- Secondary: Issue tracking
- Multiple contexts

**Routing:**
→ Primary: Standard implementation  
→ Secondary: `AI_CODE_DOCUMENTATION_PROMPT.md` for new code  
→ Then: `AI_ISSUE_CREATOR_PROMPT.md` for tracking  
→ Context: `PROJECT_CONTEXT.md` for validation rules

**Response Strategy:**
1. Implement the validation rule
2. Document the implementation
3. Create tracking issue with implementation details
4. Link code to issue for traceability

---

## Feedback Loop

This routing guide should evolve based on usage. Consider updating when:

- New guides are added to the repository
- Patterns emerge in commonly confused scenarios
- User feedback indicates routing issues
- Project context or workflows change

**Update Triggers:**
- ✏️ New guide added → Add to decision tree
- ✏️ Guide renamed/moved → Update references
- ✏️ Workflow changes → Update WORKFLOW_VISUAL routing
- ✏️ Common routing mistakes → Add to special scenarios

---

## Meta-Instructions for AI

When processing any request:

1. **Read this guide first** to determine routing
2. **Check conversation history** for established context
3. **Identify user's role** (if known or inferable)
4. **Select primary guide** using decision tree
5. **Gather context** from referenced guides
6. **Respond appropriately** with guide-specific rules
7. **Be transparent** about which guides you're following

**Remember:**
- This repository has MULTIPLE specialized guides for a reason
- Using the right guide ensures consistency and quality
- When in doubt, ask which guide the user prefers
- Context switching between guides should be explicit and clear

---

**Last Updated:** January 2026  
**Version:** 1.0  
**Maintained By:** Development Team

---

## Quick Start for AI

**Every time you receive a request:**

```
1. Read user request
2. Scan keywords → Check Quick Reference table
3. Identify primary intent → Use Decision Tree
4. Load appropriate guide(s)
5. Check PROJECT_CONTEXT.md for domain knowledge
6. Respond using guide-specific rules
7. Be explicit about which guide you're following
```

**Template Response Start:**
```
"I'll help you with [request]. Based on [keywords/context], I'm following 
the [GUIDE_NAME] guidelines..."
```

This ensures transparency and sets proper expectations.
