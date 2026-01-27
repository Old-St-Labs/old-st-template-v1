# GitHub Issue Creation Guide for BAs

> **📌 This is the ONLY file you need.** Everything you need to create issues is here.

---

## 🚀 Super Simple Start

**Just say this to GitHub Copilot Chat:**

```
Please read the following files from this repository:
- .github/AI_ISSUE_CREATOR_PROMPT.md
- .github/PROJECT_CONTEXT.md

I want to create a GitHub issue.
```

**That's it!** The AI will ask you questions and automatically:
- ✅ Determine if you need single-issue or batch mode
- ✅ Ask for your repository and ticket prefix
- ✅ Guide you through the right workflow
- ✅ Create all issues automatically

**No need to decide modes or read documentation first!**

---

## How It Works

### Step 1: You Say "I want to create a GitHub issue"

The AI loads the instructions and asks:

```
Great! I can help you create GitHub issues. Let me ask a few quick questions:

1. How many issues do you want to create?
   - Just 1 issue
   - 2-5 related issues
   - 10+ issues (I have a spreadsheet/list)

2. Do you have the user stories ready?
   - Yes, I have 1 user story ready
   - Yes, I have multiple stories in a CSV/spreadsheet
   - No, I need help writing them
```

### Step 2: AI Routes You Automatically

**Based on your answer, AI routes you to:**

**📝 Single Mode** (1-5 issues)
- Interactive Q&A for each story
- 4-6 targeted questions
- Detailed acceptance criteria

**📊 Batch CSV Mode** (10+ issues)
- Paste your CSV data
- 2-4 global questions
- One approval creates all

### Step 3: AI Collects Setup Info

```
Perfect! To get started, I need:

1. GitHub Repository: (owner/repo)
2. Ticket Prefix: (e.g., DR, DRAPER, AUTH)

[For CSV mode:]
3. Ready to paste your CSV?
```

### Step 4: You're Guided Through Creation

**Single Mode:** Answer questions → Review preview → Approve → Issue created

**Batch CSV Mode:** Paste CSV → Answer 2-4 questions → Review summary → Approve → All issues created

**Simple and straightforward!**

---

## Example: Starting a Session

**You type:**
```
Please read .github/AI_ISSUE_CREATOR_PROMPT.md and .github/PROJECT_CONTEXT.md.

I want to create a GitHub issue.
```

**AI responds:**
```
Great! I can help you create GitHub issues. Let me ask a few quick questions:

1. How many issues do you want to create?
   - Just 1 issue
   - 2-5 related issues  
   - 10+ issues (I have a spreadsheet/list)
```

**You answer:**
```
Just 1 issue
```

**AI responds:**
```
Perfect! To get started, I need:

1. GitHub Repository: (Format: owner/repo)
2. Ticket Prefix: (e.g., DR → DR-01, DR-02...)
```

**You provide:**
```
Repository: Old-St-Labs/draper
Prefix: DR
```

**AI responds:**
```
✅ Setup Complete:
   Repository: Old-St-Labs/draper
   Prefix: DR
   Mode: Single Story

Ready! Tell me your user story, and I'll guide you through creating the issue.
```

**You provide story, AI asks questions, shows preview, you approve, issue created!** ✅

---

## What Happens in Each Mode?

### 📝 Single Issue Mode (1-5 issues)

**You provide:**
```
As a [user role],
I want to [action],
so that [outcome].
```

**AI does:**
1. Reads PROJECT_CONTEXT.md to understand your project
2. Extracts entities, patterns, and tech stack
3. Asks 4-6 targeted questions:
   - Story type? (Frontend / Backend / Full Stack)
   - What should be displayed? (if UI)
   - What data to return? (if API)
   - Priority level?
   - Design reference?
4. Shows complete preview with:
   - Title, description, acceptance criteria (Gherkin format)
   - Technical context (APIs, components, database)
   - Dependencies and assumptions

**You say:** "Approve"

**AI creates:** Issue on GitHub automatically ✅

---

### 📊 Batch CSV Mode (10+ issues)

**You provide CSV:**
```csv
Epic,User_Story,Priority,Backend_Hours,Frontend_Hours,Notes
Rules Management,"As a user, I want to upload JSON rules",Low,0,0,Admin only
Monday Jobs,"As a user, I want to create Monday jobs list",Medium,6-8,4,CSV export
Error Handling,"As a user, I want row-by-row error tracking",Medium,1-2,2,Show row numbers
```

**AI does:**
1. Analyzes all stories and auto-detects:
   - Story types (Frontend/Backend/Full Stack) from hours
   - Priority levels
   - Epic groupings
   - Sequential ticket numbers (DR-01, DR-02, DR-03...)
2. Asks 2-4 global questions:
   - Full Stack splitting? (Parent + sub-issues recommended)
   - Design references?
   - Auto-add dependencies?
   - Preview preference?
3. Shows summary table:
   ```
   | # | Ticket | Title                    | Type     | Priority |
   |---|--------|--------------------------|----------|----------|
   | 1 | DR-01  | Upload JSON Rules - BE   | Backend  | Low      |
   | 2 | DR-02  | Create Monday Jobs [PARENT] | Parent | Medium |
   | 3 | DR-02-BE | Create Monday Jobs - BE | Backend (Sub) | Medium |
   | 4 | DR-02-FE | Create Monday Jobs - FE | Frontend (Sub) | Medium |
   | 5 | DR-03  | Error Tracking [PARENT]  | Parent   | Medium |
   | 6 | DR-03-BE | Error Tracking - BE     | Backend (Sub) | Medium |
   | 7 | DR-03-FE | Error Tracking - FE     | Frontend (Sub) | Medium |
   
   Total: 3 stories → 7 issues (2 parents + 4 sub-issues + 1 single)
   
   ⚠️ Note: First issue will trigger MCP approval. 
   After you approve, all remaining issues will be created automatically.
   ```

**You say:** "Approve" or "Create all"

**AI creates:** ALL issues automatically with one command ✅

```
✅ Creating first issue to enable MCP approval...

✅ DR-01 Upload JSON Rules - Backend created!
   https://github.com/Old-St-Labs/draper/issues/42

✅ MCP approval set for session. Creating remaining 6 issues...

Successfully created:
- #42: DR-01 Upload JSON Rules - Backend
- #43: DR-02 Create Monday Jobs [PARENT]
  ├── #44: DR-02-BE Backend sub-issue
  └── #45: DR-02-FE Frontend sub-issue
- #46: DR-03 Error Tracking [PARENT]
  ├── #47: DR-03-BE Backend sub-issue
  └── #48: DR-03-FE Frontend sub-issue

──────────────────────────────────────────
✅ BATCH CREATION COMPLETE

Total Stories: 3
✅ Created: 3 stories → 7 issues (2 parents + 4 sub-issues + 1 single)
⚠️ Skipped: 0 stories

View all: https://github.com/Old-St-Labs/draper/issues
──────────────────────────────────────────
```

**Batch creation makes it easy!** 🎉

---

## CSV Format Reference

**Required Columns:**
```csv
Epic,User_Story,Priority,Backend_Hours,Frontend_Hours,Notes
```

**Column Guide:**

| Column | Required? | Examples | Auto-Detection |
|--------|-----------|----------|----------------|
| **Epic** | ✅ | Authentication, Campaign, Rules | Groups related issues |
| **User_Story** | ✅ | "As a user, I want..." | Must be in quotes |
| **Priority** | ✅ | Critical, High, Medium, Low | Case-insensitive |
| **Backend_Hours** | Optional | 4, 2-3, 0, blank | `> 0` = Backend work |
| **Frontend_Hours** | Optional | 12, 4-6, 0, blank | `> 0` = Frontend work |
| **Notes** | Optional | Use Zustand; Admin only | Tech notes, validations |

**Story Type Auto-Detection:**
- `Backend > 0, Frontend = 0/blank` → **Backend Only** (1 issue)
- `Frontend > 0, Backend = 0/blank` → **Frontend Only** (1 issue)
- `Both > 0` → **[PARENT] + Sub-issues** (3 issues: parent + 2 sub-issues)
- `Both = 0` → **INCOMPLETE** (flagged for user review or skipped)

**Blank CSV Template:**
```csv
Epic,User_Story,Priority,Backend_Hours,Frontend_Hours,Notes
Authentication,"As a user, I want to...",High,4-6,2,
Campaign,"As a user, I want to...",Medium,0,4,
Data Processing,"As a user, I want to...",Medium,2-3,1,Validate structure
```

---

## Examples

### Example 1: Single Issue Request

**You to Copilot:**
```
I want to create a GitHub issue
```

**AI:**
```
How many issues do you want to create?
- Just 1 issue
- 2-5 related issues
- 10+ issues (I have a spreadsheet)
```

**You:**
```
Just 1 issue

Repository: Old-St-Labs/draper
Prefix: DR
```

**You:**
```
As a user, I want to view all campaigns.
```

**AI:** *(Asks 4-6 questions)*

**You:** *(Answers questions)*

**AI:** *(Shows complete preview)*

**You:**
```
Approve
```

**AI:** *(Creates issue)*
```
✅ Issue created successfully!

DR-42: View All Campaigns - Frontend
https://github.com/Old-St-Labs/draper/issues/42
```

---

### Example 2: Bulk CSV Request

**You to Copilot:**
```
I want to create a GitHub issue
```

**AI:**
```
How many issues? (1 / 2-5 / 10+)
```

**You:**
```
10+ issues - I have a CSV

Repository: Old-St-Labs/draper
Prefix: DR

Here's my CSV:

Epic,User_Story,Priority,Backend_Hours,Frontend_Hours,Notes
Auth,"As a user, I want Google SSO",High,4-6,2,Use Cognito
Campaign,"As a user, I want to view campaigns",Medium,0,4,Zustand state
Rules,"As a user, I want to upload JSON rules",Low,0,0,Admin only
```

**AI:** *(Analyzes CSV, asks 2-4 global questions)*

**You:** *(Answers questions)*

**AI:** *(Shows summary table)*

**You:**
```
Approve
```

**AI:** *(Creates all issues)*
```
✅ Creating first issue to enable MCP approval...

✅ DR-01 Google SSO [PARENT] created!
   You'll see an MCP approval prompt. Click "Allow for this conversation"

✅ MCP approved! Creating remaining 4 issues automatically...

Successfully created:
- #42: DR-01 Google SSO [PARENT]
  ├── #43: DR-01-BE Backend sub-issue
  └── #44: DR-01-FE Frontend sub-issue
- #45: DR-02 View Campaigns - Frontend
- #46: DR-03 Upload JSON Rules - Backend

──────────────────────────────────────────
✅ BATCH CREATION COMPLETE

Total Stories: 3
✅ Created: 3 stories → 5 issues (1 parent + 2 sub-issues + 2 singles)
⚠️ Skipped: 0 stories

View all: https://github.com/Old-St-Labs/draper/issues
──────────────────────────────────────────
```

---

## Tips

✅ **Just say "I want to create a GitHub issue"** - AI will guide you from there

✅ **Let AI determine the mode** - Answer honestly about how many issues you need

✅ **Be specific when answering** - Include examples when helpful

✅ **Review carefully** - Preview/summary is your last check before creation

✅ **Request changes** - Don't approve if something's wrong; ask for modifications

✅ **For CSV mode:** Prepare in Excel/Sheets, export as CSV, paste all at once

❌ **Don't decide mode yourself** - Let AI route you based on your needs

❌ **Don't skip setup questions** - Repository and prefix are required

❌ **Don't split CSV batches** - Upload all rows at once for consistent numbering

---

## Common Questions

**Q: Do I need to know which mode to use?**
A: No! Just say "I want to create a GitHub issue" and answer the AI's questions. It will automatically route you to single or batch mode.

**Q: What if I don't know the answer to a question?**
A: Ask AI for options or say "I'm not sure - what do you recommend?" AI can suggest based on common patterns.

**Q: Can I create multiple related issues?**
A: Yes! Just answer "2-5 issues" or "10+ issues" when AI asks how many. It will route you to the right mode.

**Q: What if the preview is too long/detailed?**
A: Say "Make [section] more concise" or "Remove [detail] from acceptance criteria"

**Q: Can I edit the issue after creation?**
A: Yes, but it's better to get it right during preview. Request changes before approving.

**Q: Does AI remember previous issues?**
A: Not automatically in Single Mode. In **Bulk CSV Mode**, AI auto-links related issues in the same batch. For references across batches, mention "Related to DR-42" in Notes column or user story.

**Q: How many issues can I create in one CSV batch?**
A: Recommended: 10-50 issues per batch. For 100+ issues, split into batches of ~25 to avoid timeouts. AI continues numbering automatically (DR-01 to DR-25, then DR-26 to DR-50, etc.).

**Q: What if CSV batch creation fails halfway?**
A: AI tracks which issues were successfully created. If failure occurs, note the last created issue number and remove completed rows from your CSV before retrying.

---

## That's It!

The AI handles:
- ✓ Reading project context
- ✓ Extracting entities and patterns
- ✓ Asking targeted questions
- ✓ Generating complete Gherkin acceptance criteria
- ✓ Adding technical context from standards
- ✓ Formatting for GitHub
- ✓ Creating the issue

You just:
- ✓ Provide the user story
- ✓ Answer a few questions
- ✓ Approve the preview

Happy issue creating! 🚀
