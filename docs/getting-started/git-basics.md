# Getting Started with Git

## Overview

This lab provides a quick introduction to Git version control system. You'll learn the basic commands needed to start using Git for your projects.

## Prerequisites

- A computer with terminal/command prompt access
- 15-20 minutes to complete
- No prior Git experience required

## Objectives

By the end of this lab, you will be able to:
- Initialize a Git repository
- Make commits to track changes
- Check the status of your repository
- View commit history

## Lab Environment

- Operating system: Windows, macOS, or Linux
- Software: Git (version 2.0 or higher)
- Hardware: Any modern computer

## Steps

### Step 1: Verify Git Installation

First, let's verify that Git is installed on your system.

```bash
git --version
```

**Expected Output:**
```
git version 2.x.x
```

If Git is not installed, visit [git-scm.com](https://git-scm.com/) to download and install it.

### Step 2: Configure Git

Set up your name and email for Git commits.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Explanation:**
These settings identify you as the author of commits. The `--global` flag applies these settings to all repositories on your system.

### Step 3: Create a New Repository

Create a new directory and initialize it as a Git repository.

```bash
mkdir my-first-repo
cd my-first-repo
git init
```

**Expected Output:**
```
Initialized empty Git repository in /path/to/my-first-repo/.git/
```

### Step 4: Create and Track Files

Create a new file and add it to Git.

```bash
echo "# My First Repository" > README.md
git status
```

**Expected Output:**
```
On branch main
Untracked files:
  README.md
```

### Step 5: Stage and Commit Changes

Add the file to the staging area and commit it.

```bash
git add README.md
git commit -m "Initial commit: Add README"
```

**Expected Output:**
```
[main (root-commit) abc1234] Initial commit: Add README
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

### Step 6: View Commit History

Check your commit history.

```bash
git log --oneline
```

**Expected Output:**
```
abc1234 Initial commit: Add README
```

## Verification

You have successfully completed this lab if:
- ✓ Git is installed and configured
- ✓ You created a new repository
- ✓ You made your first commit
- ✓ You can view the commit history

## Troubleshooting

### Issue 1: Git command not found
**Solution:** Git is not installed or not in your PATH. Download and install Git from [git-scm.com](https://git-scm.com/) and restart your terminal.

### Issue 2: Permission denied error
**Solution:** Make sure you have write permissions in the directory where you're trying to create the repository.

## Cleanup

To remove the test repository:
```bash
cd ..
rm -rf my-first-repo
```

## Summary

In this lab, you learned:
- How to verify and configure Git
- How to initialize a Git repository
- How to stage and commit changes
- How to view commit history

## Next Steps

- Learn about branching and merging
- Explore remote repositories with GitHub
- Practice with more complex Git workflows

## Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [Pro Git Book](https://git-scm.com/book)
- [GitHub Git Guides](https://github.com/git-guides)

## Notes

Git is a powerful tool that becomes easier with practice. Don't worry about memorizing all commands - you'll naturally remember the ones you use frequently.

---

**Last Updated:** 2025-12-24  
**Author:** Nadeem Labs  
**Difficulty:** Beginner
