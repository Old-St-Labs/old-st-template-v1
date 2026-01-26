# Automated GitHub Issue Creation System

This repository provides **AI-powered automated GitHub issue creation** with two powerful modes:
- 🎯 **Single Story Mode** - Interactive creation from one user story (4-6 questions)
- 📊 **Batch CSV Mode** - Bulk creation from CSV files (create 10-20+ issues at once)

**Key Features:**
- ✅ Automated issue creation directly to GitHub (no copy/paste)
- ✅ Flexible ticket numbering: `PREFIX-##` (e.g., `DR-01`, `DRAPER-15`)
- ✅ Auto-generates acceptance criteria, technical context, and dependencies
- ✅ Reads project context for consistency
- ✅ Full Stack, Frontend, or Backend story types

## 📁 Repository Structure

```
.github/
├── ISSUE_TEMPLATE/
│   ├── user-story.yml              # GitHub issue form template
│   └── config.yml                  # Template chooser configuration
├── AI_ISSUE_CREATOR_PROMPT.md      # AI system instructions (copy to Copilot)
├── PROJECT_CONTEXT.md              # Project knowledge base (tech stack, patterns)
├── ISSUE_CREATION_GUIDE.md         # Complete reference guide
├── QUICK_START_BA.md               # Simple 3-step quick start
└── copilot-instructions.md         # GitHub Copilot workspace config
```

## 🚀 Quick Start

### Option 1: Interactive Single Story Mode (Best for 1-3 issues)

**Step 1:** Setup (once per session)
```
Open GitHub Copilot and paste:

"Please read .github/AI_ISSUE_CREATOR_PROMPT.md and .github/PROJECT_CONTEXT.md.

My GitHub repository is: [owner/repo]
My ticket prefix is: [PREFIX] (e.g., DR, DRAPER, AUTH)

Then tell me you're ready to create GitHub issues."
```

**Step 2:** Create an issue
```
I want to create a GitHub issue with this user story:

As a [user role],
I want to [action],
so that [outcome].
```

**Step 3:** Answer 4-6 questions, review preview, approve

Copilot will **automatically create the issue on GitHub** ✅

---

### Option 2: Batch CSV Mode (Best for 10+ issues)

**Step 1:** Create a CSV file with your user stories

```csv
Epic,User_Story,Priority,Backend_Hours,Frontend_Hours,Notes
Authentication,"As a user, I want to login with Google SSO",High,4-6,2,Email/Password for MVP
Campaign Management,"As a user, I want to view all campaigns",Medium,0,4,Use Zustand; Manual refresh
Deliverables,"As a user, I want to review deliverables in a table",High,2-3,12,Table component; Inline editing
```

**Step 2:** Setup and provide CSV
```
Open GitHub Copilot and paste:

"Please read .github/AI_ISSUE_CREATOR_PROMPT.md in BATCH CSV MODE.

My GitHub repository is: [owner/repo]
My ticket prefix is: [PREFIX]

Here's my CSV data:
[paste CSV]"
```

**Step 3:** Answer 2-4 global questions, review summary, approve

Copilot will **create all issues automatically** with sequential numbering ✅

---

## 🎯 Creating Issues Manually

1. Go to **Issues** → **New Issue**
2. Select **📋 User Story** template
3. Use ticket format: `[PREFIX]-[##]` (e.g., `DR-01`, `DRAPER-15`)
4. Fill in all required fields
5. Submit the issue

## 📋 Story Types

| Type | Use When | Batch CSV Detection |
|------|----------|---------------------|
| **Full Stack** | Feature requires both UI and API changes | `Backend_Hours > 0` AND `Frontend_Hours > 0` |
| **Frontend Only** | UI-only changes, API already exists | `Frontend_Hours > 0`, `Backend_Hours = 0/blank` |
| **Backend Only** | API/service changes, no UI work | `Backend_Hours > 0`, `Frontend_Hours = 0/blank` |
| **Integration** | Connecting FE + BE, contract verification | Specified in Notes column |

## 📊 Batch CSV Format

**Required Columns:**
- `Epic` - Feature group (Authentication, Campaign Management, etc.)
- `User_Story` - Full user story in quotes
- `Priority` - Critical / High / Medium / Low
- `Backend_Hours` - Estimate: `4`, `2-3`, or `0`/blank
- `Frontend_Hours` - Estimate: `12`, `4-6`, or `0`/blank  
- `Notes` - Tech choices, validations, business rules (optional)

**Example:**
```csv
Epic,User_Story,Priority,Backend_Hours,Frontend_Hours,Notes
Auth,"As a user, I want Google SSO",High,4-6,2,Use AWS Cognito
Campaign,"As a user, I want to view campaigns",Medium,0,4,Zustand state management
```

**Auto-Generated:**
- ✅ Story type (Frontend/Backend/Full Stack)
- ✅ Ticket numbers (`PREFIX-01`, `PREFIX-02`, etc.)
- ✅ Labels (`user-story`, `authentication`, `priority-high`, `backend`)
- ✅ Dependencies (inferred from epic order)
- ✅ Technical context (from PROJECT_CONTEXT.md)
- ✅ Acceptance criteria (Gherkin format)

## ✅ Definition of Done

Every story includes a built-in checklist:
- [ ] All acceptance criteria met
- [ ] Code reviewed and approved
- [ ] Unit tests written and passing
- [ ] Integration/E2E tests passing
- [ ] Documentation updated
- [ ] QA validated
- [ ] Merged to main branch

## 🎫 Ticket Numbering System

**Format:** `[PREFIX]-[NUMBER]`

**Examples:**
- `DR-01` → First ticket (prefix: "DR")
- `DRAPER-15` → 15th ticket (prefix: "DRAPER")
- `AUTH-03` → 3rd ticket (prefix: "AUTH")

**Title Format:** `[PREFIX]-[##] [Feature Name] - [Story Type]`
```
DR-01 Google SSO Authentication - Backend
DR-02 View All Campaigns - Frontend  
DR-03 Review Deliverables Table - Full Stack
```

**Split Stories:** When separating Frontend/Backend:
- Sequential: `DR-29` (Backend), `DR-30` (Frontend)
- Suffixed: `DR-29-BE` (Backend), `DR-29-FE` (Frontend)

---

## 📚 Documentation

### For Business Analysts
- **[QUICK_START_BA.md](.github/QUICK_START_BA.md)** - Simple 3-step guide ⭐ START HERE
- **[ISSUE_CREATION_GUIDE.md](.github/ISSUE_CREATION_GUIDE.md)** - Complete reference with examples
- **[WORKFLOW_VISUAL.md](.github/WORKFLOW_VISUAL.md)** - Visual flowchart of the process

### For AI Assistants
- **[AI_ISSUE_CREATOR_PROMPT.md](.github/AI_ISSUE_CREATOR_PROMPT.md)** - System instructions (copy to Copilot)
- **[PROJECT_CONTEXT.md](.github/PROJECT_CONTEXT.md)** - Project knowledge base

### Reference
- [GitHub Issue Forms Syntax](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)
- [GitHub Sub-Issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/adding-sub-issues)

## 🤝 Contributing

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

MIT License - Feel free to use and modify for your projects.
