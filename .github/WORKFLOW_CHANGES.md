# GitHub Issue Creator Workflow Changes

> **Date:** January 27, 2026  
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
  - OR skip the ticket
- Skipped tickets tracked in summary report

**Why:** Ensures quality, prevents incomplete issues, provides accountability.

**Example:**
```
⚠️ Row 5: "Upload JSON Rules" has 0 hours for both BE and FE.

Options:
1. Add estimated hours (e.g., "0" → "2-3" for BE)
2. Add context in Notes (e.g., "Admin only config change")
3. Skip this ticket

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

## 6. ✅ Updated Labels

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
- AI will ask user to fix, add context, or skip

---

## 🚀 Benefits

| Before | After |
|--------|-------|
| "Full Stack" terminology | `[PARENT]` notation |
| Inconsistent parent creation | ALWAYS create parent + subs |
| 100 approvals for 100 issues | 1 approval for 100 issues |
| Incomplete tickets created | Incomplete tickets flagged |
| No visibility on skipped items | Clear summary report |

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
