# GitHub Issue Templates & Creation Guides

This directory contains templates and guides for creating well-structured GitHub issues optimized for AI-assisted development.

## 📁 Files Overview

### For Business Analysts

| File | Purpose | When to Use |
|------|---------|-------------|
| **[QUICK_START_BA.md](QUICK_START_BA.md)** | Simple 3-step guide for creating issues with AI | **START HERE** - New to the process |
| **[WORKFLOW_VISUAL.md](WORKFLOW_VISUAL.md)** | Visual flowchart of the complete interactive process | See the big picture with timeline |
| **[ISSUE_CREATION_GUIDE.md](ISSUE_CREATION_GUIDE.md)** | Complete reference guide with examples and prompts | Deep dive into workflows and best practices |
| **[PROJECT_CONTEXT.md](PROJECT_CONTEXT.md)** | Project-specific context (tech stack, data models, patterns) | Reference when creating issues; AI reads this automatically |

### For AI Assistants

| File | Purpose | When to Use |
|------|---------|-------------|
| **[AI_ISSUE_CREATOR_PROMPT.md](AI_ISSUE_CREATOR_PROMPT.md)** | System instructions for interactive issue creation | AI reads this at session start |
| **[PROJECT_CONTEXT.md](PROJECT_CONTEXT.md)** | Project knowledge base | AI references this for all technical details |

### Issue Templates (GitHub Forms)

| File | Purpose |
|------|---------|
| **[ISSUE_TEMPLATE/user-story.yml](ISSUE_TEMPLATE/user-story.yml)** | GitHub issue form template for user stories |
| **[ISSUE_TEMPLATE/config.yml](ISSUE_TEMPLATE/config.yml)** | Issue template configuration |

---

## 🚀 Quick Start for BAs

### Option 1: Interactive Mode (Recommended)

1. **Setup** (once per session):
   ```
   Open GitHub Copilot Chat and paste:
   
   "Please read .github/AI_ISSUE_CREATOR_PROMPT.md and .github/PROJECT_CONTEXT.md, 
   then tell me you're ready to help create GitHub issues."
   ```

2. **Create Issues** (every time):
   ```
   I want to create a GitHub issue with this user story:
   
   As a [user role],
   I want to [action],
   so that [outcome].
   ```

3. **Answer Questions** - AI asks 4-6 targeted questions

4. **Review & Approve** - AI shows complete preview, you approve or request changes

**Full details:** See [QUICK_START_BA.md](QUICK_START_BA.md)

### Option 2: Prompt-Based Mode

1. Gather requirements (design, tech stack, acceptance criteria)
2. Use detailed prompts from [ISSUE_CREATION_GUIDE.md](ISSUE_CREATION_GUIDE.md)
3. Generate content and create issue manually

**Full details:** See [ISSUE_CREATION_GUIDE.md](ISSUE_CREATION_GUIDE.md) → Workflow B

---

## 📖 Documentation Structure

```
.github/
├── README.md (this file)                      ← Overview and quick links
├── QUICK_START_BA.md                          ← Simple 3-step guide for BAs
├── WORKFLOW_VISUAL.md                         ← Visual flowchart with timeline
├── AI_ISSUE_CREATOR_PROMPT.md                 ← AI system instructions
├── ISSUE_CREATION_GUIDE.md                    ← Complete reference guide
├── PROJECT_CONTEXT.md                         ← Project-specific knowledge base
└── ISSUE_TEMPLATE/
    ├── config.yml                             ← Issue template config
    └── user-story.yml                         ← User story form template
```

---

## 🎯 Workflows Comparison

| Aspect | Interactive Mode | Prompt-Based Mode |
|--------|-----------------|-------------------|
| **BA Effort** | Low - just provide user story | High - gather all requirements |
| **AI Guidance** | AI asks questions | BA fills template |
| **Best For** | Quick issues, new BAs | Complex features, experienced BAs |
| **Flexibility** | Conversational, iterative | Batch creation, precise control |
| **Preview** | Always shown | Manual review |
| **Setup** | Read 2 files at session start | Copy prompt templates |

---

## 🔄 Workflow Examples

### Interactive Mode Flow
```
BA: "I want to create a GitHub issue: As a user, I want to view all campaigns."

AI: "I found: Project Draper, Campaign entity exists, General User role.
     
     Questions:
     1. Frontend Only, Backend Only, or Full Stack?
     2. What should be displayed? (Name, Client, Status, etc.)
     3. Table, cards, or list view?
     4. Filtering/sorting needed?
     5. Priority level?
     6. Design reference?"

BA: [Answers questions]

AI: [Shows complete preview with all sections]

BA: "Approve"

AI: [Creates GitHub issue]
```

### Prompt-Based Mode Flow
```
BA: [Gathers all requirements: design, tech stack, acceptance criteria]

BA: [Copies Frontend/Backend/Full Stack prompt template]

BA: [Fills in all [bracketed] sections with gathered info]

BA: [Sends to Copilot Chat]

Copilot: [Generates issue content]

BA: [Reviews and creates issue via GitHub Issue Form]
```

---

## 📝 Maintaining This System

### For Project Maintainers

**When to Update:**
- Tech stack changes → Update [PROJECT_CONTEXT.md](PROJECT_CONTEXT.md)
- New data models added → Update [PROJECT_CONTEXT.md](PROJECT_CONTEXT.md)
- API patterns change → Update [PROJECT_CONTEXT.md](PROJECT_CONTEXT.md)
- Issue template needs new fields → Update [ISSUE_TEMPLATE/user-story.yml](ISSUE_TEMPLATE/user-story.yml)

**Filling in Placeholders:**
- [PROJECT_CONTEXT.md](PROJECT_CONTEXT.md) has `[TODO: ...]` sections
- Fill these in as implementation details are finalized
- Better context = better AI-generated issues

### For BAs

**Providing Feedback:**
- If AI consistently asks for the same info, add it to [PROJECT_CONTEXT.md](PROJECT_CONTEXT.md)
- If acceptance criteria patterns are unclear, suggest examples for the guide
- If preview format is unclear, request formatting improvements

---

## 🤝 Support

**Questions about using the templates:**
- See [QUICK_START_BA.md](QUICK_START_BA.md) for basics
- See [ISSUE_CREATION_GUIDE.md](ISSUE_CREATION_GUIDE.md) for deep dive

**Questions about the project:**
- Review [PROJECT_CONTEXT.md](PROJECT_CONTEXT.md)
- Ask your development team

**Discussions:**
- Use [GitHub Discussions](../../../discussions) for questions not covered here

---

## 📚 Additional Resources

- **GitHub Issue Forms Documentation:** https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms
- **Gherkin Syntax Guide:** https://cucumber.io/docs/gherkin/reference/
- **GitHub Copilot Chat:** https://docs.github.com/en/copilot/using-github-copilot/asking-github-copilot-questions-in-your-ide

---

## 🎓 Learning Path

### For New BAs
1. Read [QUICK_START_BA.md](QUICK_START_BA.md) (5 minutes)
2. See [WORKFLOW_VISUAL.md](WORKFLOW_VISUAL.md) for the big picture (5 minutes)
3. Review [PROJECT_CONTEXT.md](PROJECT_CONTEXT.md) (10 minutes)
4. Try creating your first issue using Interactive Mode (20 minutes)
5. Skim [ISSUE_CREATION_GUIDE.md](ISSUE_CREATION_GUIDE.md) for deeper understanding (optional)

### For Experienced BAs
1. Skim [QUICK_START_BA.md](QUICK_START_BA.md) (2 minutes)
2. Read [ISSUE_CREATION_GUIDE.md](ISSUE_CREATION_GUIDE.md) → Workflow B (15 minutes)
3. Choose your preferred workflow and start creating issues

### For AI Developers
1. Read [AI_ISSUE_CREATOR_PROMPT.md](AI_ISSUE_CREATOR_PROMPT.md) (10 minutes)
2. Understand the preview format and question patterns
3. Review example interactions in [ISSUE_CREATION_GUIDE.md](ISSUE_CREATION_GUIDE.md)
