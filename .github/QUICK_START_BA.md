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
Epic,User Story,Version,BACKEND,FRONTEND,Notes
Authentication,"As an Admin, I want to sign-up using email and password",1,3,3,Use Cognito
Application forms,"As a User, I want to provide my personal details",1,1,2,Name/address/email
Payment,"As a User, I want to pay membership fee via credit card",1,6,2,Online payment
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
   | # | Ticket | Title                    | Type     | Version |
   |---|--------|--------------------------|----------|----------|
   | 1 | DAN-01 | Email/Password Signup [PARENT] | Parent | 1      |
   | 2 | DAN-01-BE | Signup - Backend | Backend (Sub) | 1 |
   | 3 | DAN-01-FE | Signup - Frontend | Frontend (Sub) | 1 |
   | 4 | DAN-02 | Provide Personal Details [PARENT]  | Parent   | 1 |
   | 5 | DAN-02-BE | Personal Details - BE     | Backend (Sub) | 1 |
   | 6 | DAN-02-FE | Personal Details - FE     | Frontend (Sub) | 1 |
   | 7 | DAN-03 | Pay Membership Fee [PARENT]  | Parent   | 1 |
   | 8 | DAN-03-BE | Payment - BE     | Backend (Sub) | 1 |
   | 9 | DAN-03-FE | Payment - FE     | Frontend (Sub) | 1 |
   
   Total: 3 stories → 9 issues (3 parents + 6 sub-issues)
   
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
- #42: DAN-01 Email/Password Signup [PARENT]
  ├── #43: DAN-01-BE Backend sub-issue
  └── #44: DAN-01-FE Frontend sub-issue
- #45: DAN-02 Provide Personal Details [PARENT]
  ├── #46: DAN-02-BE Backend sub-issue
  └── #47: DAN-02-FE Frontend sub-issue
- #48: DAN-03 Pay Membership Fee [PARENT]
  ├── #49: DAN-03-BE Backend sub-issue
  └── #50: DAN-03-FE Frontend sub-issue

──────────────────────────────────────────
✅ BATCH CREATION COMPLETE

Total Stories: 3
✅ Created: 3 stories → 9 issues (3 parents + 6 sub-issues)
⚠️ Skipped: 0 stories

View all: https://github.com/Old-St-Labs/draper/issues
──────────────────────────────────────────
```

**Batch creation makes it easy!** 🎉

---

## 🚨 Large Batch Handling (100+ Issues)

**What happens when you have 437 stories (creating ~1,311 issues)?**

The AI automatically detects large batches and offers **3 smart options:**

### Option 1: Smart Chunking (Recommended - No PowerShell) ✅

**What it does:**
- Automatically creates issues in batches of 50
- Handles rate limits automatically (pauses when needed)
- Shows progress updates every batch
- ONE approval at the start, then runs automatically
- Estimated time: ~2-3 seconds per issue

**Example Progress:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 BATCH 5/27 COMPLETE

Created: 250/1,311 issues (19.1%)
⏱️ Elapsed: 12m 30s | Remaining: ~53m
✅ Success: 250 | ❌ Failed: 0

Next: Batch 6/27 (issues 251-300)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Pros:**
- ✅ Minimal user interaction (approve once, monitor progress)
- ✅ Automatic rate limit handling
- ✅ Error recovery (continues if individual issues fail)
- ✅ Real-time progress updates
- ✅ No PowerShell scripts needed

**Cons:**
- ⚠️ Must keep conversation open (~1-2 hours for 437 stories)
- ⚠️ Cannot pause/resume (but failures are retryable at end)

**When to use:** You can monitor the process for the estimated time

---

### Option 2: Filtered Batches (Reduce Scope) 🎯

**What it does:**
- AI shows you breakdown by Epic/Version/Priority
- You choose which subset to create now
- Repeat for other subsets later (new conversations)

**Example:**
```
Your CSV Breakdown:

By Epic:
- Authentication (47 stories → 141 issues)
- Campaign Management (89 stories → 267 issues)
- Data Processing (143 stories → 429 issues)
- Deliverables (158 stories → 474 issues)

Which would you like to create first?
(e.g., "Create Authentication epic only")
```

**Pros:**
- ✅ Manageable batch sizes (under 300 issues per session)
- ✅ Logical organization (one epic or version at a time)
- ✅ Can spread work across days
- ✅ Easier to review and validate

**Cons:**
- ⚠️ Requires multiple sessions
- ⚠️ Need to track which epics/versions are done

**When to use:** You want to create issues incrementally over time

---

### Option 3: Manual CSV Splitting 📦

**What it does:**
- You manually split your 437-row CSV into smaller files (50 rows each)
- Paste each file in a new conversation
- AI automatically continues ticket numbering

**Instructions:**
1. Open CSV in Excel/Google Sheets
2. Save these files:
   - Part 1: Rows 1-50
   - Part 2: Rows 51-100
   - Part 3: Rows 101-150
   - etc. (9 files total)
3. Create new conversation for each part
4. Paste CSV, AI says "Starting from DR-51..."
5. Approve each batch

**Pros:**
- ✅ Full control over batches
- ✅ Guaranteed to work (small batches)
- ✅ Can spread across multiple days
- ✅ Can prioritize certain rows

**Cons:**
- ⚠️ Most manual effort (splitting CSV)
- ⚠️ 9+ conversations needed for 437 stories
- ⚠️ Must track which parts are done

**When to use:** You need maximum control and flexibility

---

### Comparison Table

| Feature | Smart Chunking | Filtered Batches | Manual Split |
|---------|---------------|------------------|--------------|
| **PowerShell** | ❌ No | ❌ No | ❌ No |
| **User Approvals** | 1 | 1 per filter | 1 per part |
| **Conversations** | 1 | 2-5 | 9+ |
| **Time Commitment** | 1-2 hours continuous | 30-60 min per session | 20-30 min per part |
| **Ideal For** | Can monitor for duration | Incremental over days | Maximum control |
| **437 Stories** | ~1h 45m (1 session) | ~4-5 sessions | ~9 sessions |

---

### AI Detection & Recommendation

When you paste a large CSV, AI automatically shows:

```
⚠️ LARGE BATCH DETECTED

Your CSV: 437 stories → 1,311 total issues
Estimated time: ~1 hour 45 minutes

RECOMMENDED: Option 1 (Smart Chunking)
- One approval, automatic batching
- Progress updates every 50 issues
- You can monitor in this conversation

Alternative: Option 2 (Filter by Epic/Version)
- Create "Version 1" now (178 stories)
- Come back for Version 2 later

Your choice? (Reply "Option 1", "Option 2: Filter by Version", or "Option 3")
```

---

## CSV Format Reference

**Required Columns:**
```csv
Epic,User Story,Version,BACKEND,FRONTEND,Notes
```

**Column Guide:**

| Column | Required? | Examples | Auto-Detection |
|--------|-----------|----------|----------------|
| **Epic** | ✅ | Application forms, Authentication, Payment | Groups related issues |
| **User Story** | ✅ | "As a user, I want..." | Must be in quotes |
| **Version** | ✅ | 1, 2, 3 | Milestone/release planning |
| **BACKEND** | Optional | 3, 6, 0, blank | `> 0` = Backend work (rounded) |
| **FRONTEND** | Optional | 2, 5, 0, blank | `> 0` = Frontend work (rounded) |
| **Notes** | Optional | Use Cognito; Admin only | Tech notes, validations |

**Story Type Auto-Detection:**
- `BACKEND > 0, FRONTEND = 0/blank` → **Backend Only** (1 issue)
- `FRONTEND > 0, BACKEND = 0/blank` → **Frontend Only** (1 issue)
- `Both > 0` → **[PARENT] + Sub-issues** (3 issues: parent + 2 sub-issues with clickable links)
- `Both = 0` → **INCOMPLETE** (flagged - user can add hours, add context, create as Parent + Sub-issues with 0 estimates, or skip)

**Parent + Sub-issue Navigation:**
- Parent issues include: `Sub-Issues: #44 (Backend), #45 (Frontend)` - clickable links
- Sub-issues include: `Parent Issue: #43` - clickable link
- Click issue numbers to navigate between parent and sub-issues

**Blank CSV Template:**
```csv
Epic,User Story,Version,BACKEND,FRONTEND,Notes
Authentication,"As a user, I want to...",1,3,2,
Application forms,"As a user, I want to...",1,0,4,
Payment,"As a user, I want to...",1,6,2,Validate payment
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

Epic,User Story,Version,BACKEND,FRONTEND,Notes
Authentication,"As an Admin, I want to sign-up using email and password",1,3,3,Use Cognito
Application forms,"As a User, I want to provide personal details",1,1,2,Name/address/email
Payment,"As a User, I want to pay via credit card",1,6,2,Online payment
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
- #42: DAN-01 Email/Password Signup [PARENT]
  ├── #43: DAN-01-BE Backend sub-issue
  └── #44: DAN-01-FE Frontend sub-issue
- #45: DAN-02 Provide Personal Details [PARENT]
  ├── #46: DAN-02-BE Backend sub-issue
  └── #47: DAN-02-FE Frontend sub-issue
- #48: DAN-03 Pay via Credit Card [PARENT]
  ├── #49: DAN-03-BE Backend sub-issue
  └── #50: DAN-03-FE Frontend sub-issue

──────────────────────────────────────────
✅ BATCH CREATION COMPLETE

Total Stories: 3
✅ Created: 3 stories → 9 issues (3 parents + 6 sub-issues)
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
