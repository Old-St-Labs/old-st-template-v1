# Quick Start: Interactive Issue Creation for BAs

## Setup (Do Once Per Session)

**Step 1:** Open GitHub Copilot Chat

**Step 2:** Paste this message:
```
Please read the following files from this repository:
- .github/AI_ISSUE_CREATOR_PROMPT.md
- .github/PROJECT_CONTEXT.md

My GitHub repository is: [owner/repo]
(e.g., Old-St-Labs/old-st-template-v1)

Then tell me you're ready to help create GitHub issues.
```

**Step 3:** Wait for Copilot to confirm it's ready

---

## Creating an Issue (Every Time)

### Simple 3-Step Process

**1. Provide Your User Story**
```
I want to create a GitHub issue with this user story:

As a [user role],
I want to [action/goal],
so that [desired outcome].
```

**2. Answer AI's Questions**

AI will ask 4-6 specific questions like:
- Story type? (Frontend / Backend / Full Stack)
- What should be displayed? (if UI)
- What data to return? (if API)
- Priority level?
- Design reference?

Just answer naturally - examples and details welcome!

**3. Review & Approve**

AI shows you a complete preview of the issue.

Reply with:
- `Approve` - Create the issue as shown
- `Change [section]` - Modify a specific part
- `Add [detail]` - Include something missing

---

## Examples

### Example 1: Simple Request

**You:**
```
I want to create a GitHub issue with this user story:

As a user, I want to view all campaigns.
```

**AI:** *(Extracts context, asks 4-6 questions)*

**You:** *(Answers questions)*

**AI:** *(Shows complete preview)*

**You:**
```
Approve
```

**AI:** *(Automatically creates the GitHub issue and provides the URL)*
```
✅ GitHub issue #42 created successfully!
   https://github.com/Old-St-Labs/draper/issues/42
```

---

### Example 2: With More Details Upfront

**You:**
```
I want to create a GitHub issue with this user story:

As a General User, I want to filter campaigns by status in a table view, 
so that I can quickly find campaigns that are in progress.

This should be full stack with:
- Table showing: Campaign Name, Client, Status, Delivery Date
- Filter dropdown for status
- 20 items per page
- Medium priority
- No Figma, follow existing table patterns
```

**AI:** *(May only ask 1-2 clarifying questions or go straight to preview)*

**You:**
```
Approve
```

---

## Tips

✅ **Start simple** - Just give the user story; AI will ask what it needs

✅ **Be specific** - When answering, include examples when helpful

✅ **Review carefully** - The preview is your last check before creation

✅ **Request changes** - Don't approve if something's wrong; ask for changes

✅ **Check PROJECT_CONTEXT.md** - Periodically review to know what context AI has

❌ **Don't gather everything first** - Let AI guide you with questions

❌ **Don't skip the preview** - Always review before approving

---

## Common Questions

**Q: What if I don't know the answer to a question?**
A: Ask AI for options or say "I'm not sure - what do you recommend?" AI can suggest based on common patterns.

**Q: Can I create multiple related issues?**
A: Yes! Create them one at a time. For split stories (FE/BE), create the first, get its ticket number, then reference it when creating the second.

**Q: What if the preview is too long/detailed?**
A: Say "Make [section] more concise" or "Remove [detail] from acceptance criteria"

**Q: Can I edit the issue after creation?**
A: Yes, but it's better to get it right during preview. Request changes before approving.

**Q: Does AI remember previous issues?**
A: Not automatically. If creating related issues, mention "This is related to DRAPER-42" in your user story.

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
