# GitHub Issue Creator Workflow Changes

> **Date:** February 18, 2026 (Last Updated)  
> **Status:** ✅ Implemented

---

## 🎯 Summary of Changes

The GitHub issue creator workflow has been updated for **consistency, scalability, and efficiency**. Below are the key improvements:

---

## 1. ✅ [PARENT] Notation (No More "Full Stack")

### Before:
- Issues labeled as "Full Stack"
- Title: `DR-03 Review Deliverables - Full Stack`

### After:
- Issues labeled as `[PARENT]`
- Title: `DR-03 Review Deliverables [PARENT]`
- Sub-issues: `DR-03-BE`, `DR-03-FE`

**Why:** Clearer parent-child relationship, more professional terminology.

---

## 2. ✅ Mandatory Parent + Sub-issue Creation

### Before:
- Stories with both BE and FE hours *could* create 1 combined issue or 3 separate issues

### After:
- Stories with both BE and FE hours **ALWAYS** create:
  - 1 Parent issue `[PARENT]` 
  - 1 Backend sub-issue `-BE`
  - 1 Frontend sub-issue `-FE`

**Why:** Consistent tracking, better progress visibility, clearer work separation.

**Example:**
```
DR-05 Campaign Management [PARENT]
├── DR-05-BE Campaign Management - Backend
└── DR-05-FE Campaign Management - Frontend
```

---

## 3. ✅ MCP Approval Workflow (Scalability Fix)

### Before:
- 100 issues = 100 approval clicks
- Each issue required individual MCP approval

### After:
- **Step 1:** Create first issue → Triggers MCP approval
- **Step 2:** User approves ONCE → "Allow for this conversation"
- **Step 3:** All remaining issues created automatically

**Why:** Scales from 1 ticket to 200+ tickets seamlessly. No more clicking hundreds of times.

**Flow:**
```
1. AI creates first issue (DR-01)
2. User sees MCP approval → Clicks "Allow for this conversation"
3. AI auto-creates all remaining issues (DR-02 through DR-200)
4. Summary report shows created vs skipped
```

---

## 4. ✅ Incomplete Ticket Validation

### Before:
- Stories with 0 BE + 0 FE hours created anyway
- Led to vague, incomplete issues

### After:
- Stories with `0 BE hours + 0 FE hours` are **FLAGGED**
- AI asks user to:
  - Add estimated hours
  - Provide context in Notes
  - Create as Parent + Sub-issues (maintains structure, tracks 0 hours)
  - OR skip the ticket
- Skipped tickets tracked in summary report

**Why:** Ensures quality, prevents incomplete issues, provides accountability, while allowing organizational flexibility.

**Example:**
```
⚠️ Row 5: "Upload JSON Rules" has 0 hours for both BE and FE.

Options:
1. Add estimated hours (e.g., "0" → "2-3" for BE)
2. Add context in Notes (e.g., "Admin only config change")
3. Create as Parent + Sub-issues (0 hours tracked, maintains FE/BE structure)
4. Skip this ticket

Your choice?
```

---

## 5. ✅ Summary Reporting

### Before:
- No visibility into what was created vs skipped
- Users had to manually count issues

### After:
- Clear summary report after batch creation:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ BATCH CREATION COMPLETE

Total Stories: 10
✅ Created: 7 stories → 15 issues (3 parents + 6 subs + 6 singles)
⚠️ Skipped: 3 stories (incomplete estimates)

Skipped Stories:
- Row 5: "Upload rules" (0 BE, 0 FE - user chose to skip)
- Row 8: "Admin config" (0 BE, 0 FE - user chose to skip)
- Row 12: "Update docs" (0 BE, 0 FE - user chose to skip)

View all: https://github.com/Old-St-Labs/draper/issues
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Why:** Transparency, accountability, easy verification.

---

## 6. ✅ Clickable Sub-Issue Links

### Before:
- Parent issues referenced sub-issues by ticket number only (e.g., "DR-03-BE")
- No clickable navigation between parent and sub-issues
- Manual search required to find related issues

### After:
- Parent issues include **clickable GitHub issue links**: `Sub-Issues: #44 (Backend), #45 (Frontend)`
- Sub-issues reference parent: `Parent Issue: #43`
- **Bidirectional navigation**: Click issue numbers to jump between parent and sub-issues
- Parent issue updated automatically after sub-issues are created

**Why:** Faster navigation, better developer experience, easier issue management.

**Creation Flow:**
```
1. Create parent issue #43 → "DR-03 Campaign Management [PARENT]"
2. Create backend sub-issue #44 → "DR-03-BE Campaign Management - Backend"
   └── Body includes: "Parent Issue: #43" (clickable)
3. Create frontend sub-issue #45 → "DR-03-FE Campaign Management - Frontend"
   └── Body includes: "Parent Issue: #43" (clickable)
4. Update parent issue #43 → Add: "Sub-Issues: #44 (Backend), #45 (Frontend)" (clickable)
```

**Example Parent Issue:**
```
**Ticket Number:** DR-03
**Sub-Issues:** #44 (Backend), #45 (Frontend)  ← Clickable links
**Estimated Effort:** 3 hours (Backend), 4 hours (Frontend)
```

---

## 7. ✅ Updated Labels

### Before:
- `full-stack` label for parent issues
- No `sub-issue` label

### After:
- `parent-issue` label for parent issues
- `sub-issue` label for sub-issues
- Backend/Frontend labels remain

**Examples:**
- Parent: `["user-story", "campaign", "priority-medium", "parent-issue"]`
- Sub-issue: `["user-story", "campaign", "priority-medium", "backend", "sub-issue"]`
- Single: `["user-story", "auth", "priority-high", "backend"]`

---

## 📋 Updated CSV Format

No changes to CSV structure, but updated validation:

```csv
Epic,User_Story,Priority,Backend_Hours,Frontend_Hours,Notes
Authentication,"As a user, I want to...",High,4-6,2,Use Cognito
Campaign,"As a user, I want to...",Medium,0,4,Zustand state
Rules,"As a user, I want to...",Low,0,0,Admin only ← FLAGGED (0+0 hours)
```

**New Behavior:**
- Row 3 will be **flagged** because both BE and FE = 0
- AI will ask user to: add hours, add context, create as Parent + Sub-issues (0 estimates), or skip

---

## 8. ✅ Large Batch Handling (100+ Issues)

### Before:
- No guidance for handling 100+ issue batches
- Risk of timeouts, rate limits with large CSVs
- PowerShell script as only alternative
- Manual CSV splitting with no guidance

### After:
- **Automatic detection** when CSV would create 100+ issues
- **3 smart options presented** with pros/cons:
  
  **Option 1: Smart Chunking (No PowerShell)**
  - Auto-batches in groups of 50 issues
  - Handles rate limits automatically (pauses when needed)
  - Progress updates every batch
  - One approval, runs ~1-2 hours for large batches
  - Error recovery and retry for failures
  
  **Option 2: Filtered Batches**
  - Filter by Epic/Version/Priority
  - Create logical subsets (e.g., "Version 1 only")
  - Multiple sessions, manageable sizes
  - Clear breakdown shown to user
  
  **Option 3: Manual Split**
  - Detailed instructions for splitting CSV
  - Automatic ticket number continuation
  - Full control over batch sizes

### Why:
- Handles edge case of 200-1,500+ issue creation
- Prevents timeouts and rate limit errors
- **No PowerShell required** for automated approach
- Clear guidance removes guesswork
- Maintains single-approval workflow within batches

### Example (437 Stories):

**Detection Message:**
```
⚠️ LARGE BATCH DETECTED

Your CSV: 437 stories → 1,311 total issues
(437 parents + 437 BE subs + 437 FE subs)

Estimated time: ~1 hour 45 minutes

RECOMMENDED: Option 1 (Smart Chunking)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
- Automatic batching (50 issues per batch = 27 batches)
- Rate limit handling (auto-pause if needed)
- Progress updates: "Batch 5/27 complete (250/1,311)"
- One approval at start
- ~2-3 seconds per issue

Your choice? (Reply "Option 1", "Option 2: Filter by Epic", or "Option 3")
```

**Progress During Creation:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 BATCH 8/27 COMPLETE

Created: 400/1,311 issues (30.5%)
⏱️ Elapsed: 20m 15s | Remaining: ~47m
✅ Success: 400 | ❌ Failed: 0
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## 🚀 Benefits

| Before | After |
|--------|-------|
| "Full Stack" terminology | `[PARENT]` notation |
| Inconsistent parent creation | ALWAYS create parent + subs |
| 100 approvals for 100 issues | 1 approval for 100 issues |
| Incomplete tickets created | Incomplete tickets flagged |
| No visibility on skipped items | Clear summary report |
| Manual navigation between issues | Clickable #issue links for parent ↔ sub-issues |
| No guidance for 100+ issues | Smart chunking, filtering, or manual split options |
| PowerShell script required for large batches | Auto-batching with rate limit handling (no script) |

---

## 📖 Updated Documentation

The following files have been updated:
- ✅ `.github/AI_ISSUE_CREATOR_PROMPT.md` - AI workflow instructions
- ✅ `.github/QUICK_START_BA.md` - BA user guide with examples
- ✅ `.github/PROJECT_CONTEXT.md` - Ticket format standards

---

## 🎯 Usage Example

**Before (Old Workflow):**
```
1. Paste CSV with 50 stories
2. Approve each of 50 issues individually = 50 clicks
3. No idea which were skipped
4. Issues titled "Full Stack"
```

**After (New Workflow):**
```
1. Paste CSV with 50 stories
2. AI validates → Flags 3 incomplete tickets
3. User fixes or skips those 3
4. AI creates issue #1 → User approves MCP ONCE
5. AI auto-creates remaining 46 issues
6. Summary report:
   ✅ Created: 47 stories → 120 issues (15 parents + 30 subs + 75 singles)
   ⚠️ Skipped: 3 stories (incomplete)
```

---

## ✅ Implementation Status

- [x] Update AI_ISSUE_CREATOR_PROMPT.md
- [x] Update QUICK_START_BA.md
- [x] Update PROJECT_CONTEXT.md
- [x] Document changes (this file)
- [x] Test with sample CSV
- [ ] Update copilot-instructions.md (if needed)

---

## 🔄 Migration Notes

**For existing issues:**
- No retroactive changes required
- New issues follow new format going forward

**For BAs:**
- Use same CSV format
- Expect validation prompts for 0+0 hour stories
- Approve MCP ONCE per session (not per issue)
- Review summary report after batch creation

**For developers:**
- Look for `[PARENT]` in titles, not "Full Stack"
- Use `parent-issue` and `sub-issue` labels for filtering

---

**Questions?** See `.github/QUICK_START_BA.md` for detailed examples.
