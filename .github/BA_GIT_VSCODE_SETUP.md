# VS Code Setup Guide for Business Analysts & Project Managers

This guide will help you set up Visual Studio Code (VS Code) and GitHub Copilot to create GitHub issues for the Cousteau project.

**You'll use VS Code + GitHub Copilot to create issues - no coding required!**

## What You'll Do

As a BA or PM, you'll use GitHub Copilot (an AI assistant) to create issues. The AI asks you questions, and then automatically creates properly formatted GitHub issues for the development team.

**Your workflow:**
1. Open VS Code
2. Open the project folder
3. Open Copilot Chat
4. Tell Copilot you want to create an issue
5. Answer some questions
6. Copilot creates the issue automatically ✅

**That's it!** No Git commands, no coding needed.

---

## Table of Contents
1. [Install Git](#install-git)
2. [VS Code Installation](#vs-code-installation)
3. [GitHub Copilot Setup](#github-copilot-setup)
4. [Opening the Project](#opening-the-project)
5. [Creating Your First Issue](#creating-your-first-issue)
6. [Quick Reference](#quick-reference)

---

## Install Git

Git is required for VS Code to clone repositories. Install it first:

### Windows

1. **Download Git:**
   - Visit [https://git-scm.com/download/win](https://git-scm.com/download/win)
   - Download will start automatically

2. **Install Git:**
   - Run the downloaded installer
   - **Just click "Next" through all options** - the defaults are fine
   - Click "Install"
   - Click "Finish"

### macOS

Git is usually pre-installed on macOS. To verify or install:

1. **Open Terminal:**
   - Press `Cmd + Space`
   - Type "Terminal" and press Enter

2. **Check if Git is installed:**
   ```bash
   git --version
   ```
   - If you see a version number (e.g., "git version 2.39.0"), you're done! ✅
   - If you see "command not found," continue to step 3

3. **Install Git:**
   - Visit [https://git-scm.com/download/mac](https://git-scm.com/download/mac)
   - Download and run the installer
   - Or install via Homebrew (if you have it): `brew install git`

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install git
```

**✅ Git is now installed!** You can close the terminal - VS Code will use Git automatically.

---

## VS Code Installation and Setup

### Windows

1. **Download VS Code:**
   - Visit [https://code.visualstudio.com/](https://code.visualstudio.com/)
   - Click "Download for Windows"

2. **Install VS Code:**
   - Run the downloaded installer
   - **Important checkboxes to select:**
     - ✅ Add "Open with Code" action to Windows Explorer file context menu
     - ✅ Add "Open with Code" action to Windows Explorer directory context menu
     - ✅ Add to PATH

3. **Launch VS Code** after installation

### macOS

1. **Download VS Code:**
   - Visit [https://code.visualstudio.com/](https://code.visualstudio.com/)
   - Click "Download for Mac"

2. **Install VS Code:**
   - Open the downloaded `.zip` file
   - Drag `Visual Studio Code.app` to your Applications folder
   - Open VS Code from Applications

3. **Add to PATH (for terminal access):**
   - Press `Cmd + Shift + P`
   - Type "shell command" and select "Shell Command: Install 'code' command in PATH"
   - Click "Install"

### Linux (Ubuntu/Debian)

```bash
# Download and install
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code
```

Then launch VS Code from applications or by typing `code` in terminal.

### Install GitHub Copilot Extension

After installing VS Code, install GitHub Copilot:

1. **Open Extensions Panel:**
   - Click the Extensions icon in the left sidebar (4 squares icon)
   - Or press `Ctrl/Cmd + Shift + X`

2. **Install GitHub Copilot:**
   - Search for "GitHub Copilot"
   - Click Install
   - Sign in with your GitHub account when prompted

**Optional but helpful:**
- **GitLens** - Makes Git much easier to visualize (who changed what, file history, etc.)

---

## GitHub Copilot Setup

### Step 1: Install GitHub Copilot Extension

1. **In VS Code, open Extensions Panel:**
   - Click the Extensions icon in the left sidebar (looks like 4 squares)
   - Or press `Ctrl/Cmd + Shift + X`

2. **Search and Install:**
   - Type "GitHub Copilot" in the search box
   - Click the **Install** button on "GitHub Copilot" extension
   - Also install "GitHub Copilot Chat" (should install automatically)

### Step 2: Sign In to GitHub

1. **After installation, VS Code will prompt:**
   - Click "Sign in to GitHub"
   - Your browser will open
   
2. **Authorize in Browser:**
   - Sign in to your GitHub account if needed
   - Click "Authorize Visual-Studio-Code"
   - You may see a prompt "Open Visual Studio Code?" - Click "Open"

3. **Back in VS Code:**
   - You should see "GitHub Copilot is active"
   - Look for a Copilot icon in the bottom-right status bar

**✅ You're ready to use Copilot!**

---

## Opening the Project

### Clone the Repository

Before you can work with the project, you need to clone (download) it from GitHub:

1. **Make sure you have GitHub access:**
   - Ask your team lead to add you as a collaborator on the repository
   - You'll receive an email invitation from GitHub - accept it

2. **Clone using VS Code:**
   - In VS Code, press `Ctrl/Cmd + Shift + P` to open Command Palette
   - Type "Git: Clone" and select it
   - Choose "Clone from GitHub"
   - Sign in to GitHub if prompted
   - Search for the repository name (e.g., "cousteau")
   - Select where to save it on your computer
   - Click "Select Repository Location"

3. **Open the cloned folder:**
   - VS Code will ask "Would you like to open the cloned repository?"
   - Click **"Open"**

**Alternative: If you already have the folder**

If someone already shared the project folder with you:

### Open in VS Code

1. **Launch VS Code**

2. **Open the Folder:**
   - Click **File → Open Folder** (Windows/Linux)
   - Or **File → Open** (macOS)
   - Navigate to the project repo folder
   - Click "Select Folder" or "Open"

3. **Trust the Workspace:**
   - VS Code may ask "Do you trust the authors?"
   - Click **"Yes, I trust the authors"** (this is your team's project)

**✅ Project is open!** You should see the file tree in the left sidebar.

---

## Creating Your First Issue

### Open Copilot Chat

1. **Open Chat Panel:**
   - Click the Copilot Chat icon in the left sidebar (looks like a chat bubble)
   - Or press `Ctrl/Cmd + Shift + I`
   - Or click the Copilot icon in bottom-right status bar and select "Open Chat"

2. **You'll see a chat interface** where you can type messages to the AI

### Your First Prompt

To start creating issues, paste this into Copilot Chat:

```
Please read the following files from this repository:
- .github/AI_ISSUE_CREATOR_PROMPT.md
- .github/PROJECT_CONTEXT.md

I want to create a GitHub issue.
```

Press **Enter** and Copilot will guide you through the rest!

### What Happens Next?

Copilot will ask you questions and guide you through creating issues. For the complete workflow, detailed examples, and CSV batch mode instructions, see:

👉 **[QUICK_START_BA.md](.github/QUICK_START_BA.md)** - Complete issue creation guide

---

## Quick Reference

### Opening VS Code & Starting Work

1. **Launch VS Code**
2. **Open Folder:** File → Open → Select project folder
3. **Open Copilot Chat:** Click chat icon in left sidebar or `Ctrl/Cmd + Shift + I`
4. **Start prompt:** \"Please read .github/AI_ISSUE_CREATOR_PROMPT.md and .github/PROJECT_CONTEXT.md. I want to create a GitHub issue.\"

### Keyboard Shortcuts

- `Ctrl/Cmd + Shift + P` - Command palette (run any VS Code command)
- `Ctrl/Cmd + Shift + I` - Open Copilot Chat
- `Ctrl/Cmd + Shift + E` - Show file Explorer
- `Ctrl/Cmd + P` - Quick file search
- `Ctrl/Cmd + F` - Find in current file
- `Ctrl/Cmd + S` - Save file

### Useful Copilot Commands

In Copilot Chat, you can ask:

```
# Create issues
\"I want to create a GitHub issue\"

# Get help understanding the project
\"Explain the structure of this project\"

# Find information
\"Where are the business rules documented?\"

# Learn about workflows
\"How do I create batch issues from a CSV?\"
```

### Tips

✅ **Keep Copilot Chat open** - Pin it to the left sidebar for easy access

✅ **Ask questions** - Copilot knows the project context, just ask!

✅ **Review before approving** - Always check the issue preview before Copilot creates it

✅ **Use batch mode for multiple issues** - If you have 10+ issues, use CSV batch mode (see QUICK_START_BA.md)

---

## Troubleshooting

### \"Copilot is not active\"
**Solution:** 
1. Click the Copilot icon in bottom-right status bar
2. Select \"Sign in to GitHub\"
3. Authorize in your browser

### \"Can't find the project folder\"
**Solution:** 
- Ask your team lead for the folder location or repository access
- They may need to add you as a collaborator on GitHub first

### \"Copilot says it can't create issues\"
**Solution:**
- Make sure you're signed in to GitHub (check status bar)
- Make sure you have collaborator access to the repository
- Check that you provided the correct repository name (format: owner/repo)

### \"I made a mistake in an issue\"
**Solution:**
- Go to the issue on GitHub.com
- Click \"Edit\" to update the title or description
- Or add a comment with corrections
- Or close the issue if it's not needed

---

## Next Steps

After setup is complete:

1. ✅ **Read [QUICK_START_BA.md](.github/QUICK_START_BA.md)** - Detailed guide for creating issues
2. ✅ **Practice creating an issue** - Try creating a test issue to get comfortable
3. ✅ **Explore CSV batch mode** - If you create many issues at once
4. ✅ **Ask questions** - Your team lead can help with any confusion

---

## Getting Help

- **Copilot Chat** - Ask Copilot directly in VS Code!
- **Team Lead** - For project-specific questions
- **VS Code Docs** - [https://code.visualstudio.com/docs](https://code.visualstudio.com/docs)
- **QUICK_START_BA.md** - Complete issue creation guide

---

**You're all set!** 🎉

**Remember:** You're using AI to create issues - no coding needed. Just open VS Code, open Copilot Chat, and tell it what you want to do!
