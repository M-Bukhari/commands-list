# Git and Github

## Command list

## I want to save these changes into a new branch. Give me the GIT commands to run them on my WSL

### Here are the Git commands to save your changes into a new branch:

```bash
### Create and switch to a new branch

git checkout -b feature/save-endpoint-and-button-fixes

### Add all the changed files to staging

git add .

### Create a commit with a descriptive message

git commit -m "$(cat <<'EOF'
Fix save endpoint and button visibility issues

-   Debug and resolve save endpoint error caused by missing database columns
-   Fix migration conflicts for normalized tables structure
-   Add missing columns to application_form_sessions table
-   Fix save button visibility consistency with form filler extensions
-   Implement debounced auto-save for rapid form changes
-   Update button state management to keep save button always visible
-   Test complete save/resume workflow functionality
-   Resolve /investor/qualification/save endpoint functionality

🤖 Generated with [Claude Code](https://claude.ai/code)

Co-Authored-By: Claude <noreply@anthropic.com>
EOF
)"

### Push the new branch to remote repository

git push -u origin feature/save-endpoint-and-button-fixes

Alternative shorter version:

### Create new branch and switch to it

git checkout -b feature/save-endpoint-fixes

### Stage and commit all changes

git add .
git commit -m "Fix save endpoint and button visibility issues
```

### Push to remote

```bash
  git push -u origin feature/save-endpoint-fixes
```

Run these commands in your WSL terminal from the project directory. The first command creates a new branch, the second stages
your changes, the third commits them with a descriptive message, and the fourth pushes the branch to your remote repository.

● To check your changes on your UAT environment, you'll need to pull the new branch and
switch to it. Here are the commands to run on your UAT server:

```bash
# Fetch the latest branches from remote
git fetch origin

# Switch to your new branch
git checkout feature/save-endpoint-and-button-fixes

# Pull the latest changes (if needed)
git pull origin feature/save-endpoint-and-button-fixes

# If the branch doesn't exist locally on UAT yet, use:
git checkout -b feature/save-endpoint-and-button-fixes origin/feature/save-endpoint-and-button-fixes

# After switching branches, make sure to run any necessary deployment commands for your Laravel app
# (like composer install, php artisan migrate, etc.) if your UAT environment requires them.

<!-- ## GIT Commands -->

#…or create a new repository on the command line
echo "# investment-hub" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Mbukhari-Abam/investment-hub.git
git push -u origin main

# …or push an existing repository from the command line

git remote add origin https://github.com/Mbukhari-Abam/investment-hub.git
git branch -M main
git push -u origin main

# <!-- Remove Git index lock file   -->
rm "/mnt/d/01 Apps/Development/Web/abam-investment-hub/.git/index.lock"
```

```bash
# You can check the differences between CSS files in the backup branch and your current
# branch using these git commands:

  Compare specific CSS files:
  # Compare a single CSS file
  git diff backup/broken-code-ref..HEAD -- public/css/styles.css

  # Compare multiple CSS files
  git diff backup/broken-code-ref..HEAD -- public/css/components.css
  public/css/forms.css

  # Compare all CSS files in public/css/
  git diff backup/broken-code-ref..HEAD -- public/css/

  Get a summary of what files changed:
  # Show only file names that differ
  git diff --name-only backup/broken-code-ref..HEAD -- public/css/

  # Show file names with change status (M=modified, A=added, D=deleted)
  git diff --name-status backup/broken-code-ref..HEAD -- public/css/

  Compare specific files you mentioned:
  # Check the main CSS files that were modified
  git diff backup/broken-code-ref..HEAD -- public/css/components.css
  git diff backup/broken-code-ref..HEAD -- public/css/components/file-upload.css
  git diff backup/broken-code-ref..HEAD -- public/css/forms.css
  git diff backup/broken-code-ref..HEAD -- public/css/styles.css

  For a side-by-side view in VS Code:
  # Open VS Code diff view for a specific file
  code --diff <(git show backup/broken-code-ref:public/css/styles.css)
  public/css/styles.css

  The format is backup-branch..current-branch -- file-path where HEAD represents your
  current branch.
```

## When facing ReBase Issues

    branch feature/file-upload-component -> FETCH_HEAD
    hint: You have divergent branches and need to specify how to reconcile them.
    hint: You can do so by running one of the following commands sometime before
    hint: your next pull:
    hint:
    hint: git config pull.rebase false # merge
    hint: git config pull.rebase true # rebase
    hint: git config pull.ff only # fast-forward only
    hint:
    hint: You can replace "git config" with "git config --global" to set a default
    hint: preference for all repositories. You can also pass --rebase, --no-rebase,
    hint: or --ff-only on the command line to override the configured default per
    hint: invocation.
    fatal: Need to specify how to reconcile divergent branches.

This error occurs because your UAT server's local branch has commits that the remote branch doesn't have (divergent branches).
You need to choose how to reconcile them.

### Quick Solution (Recommended for UAT)

If you want to discard local UAT changes and match the remote branch exactly:

```bash
### Save current state (just in case)
git stash

### Force your local branch to match remote exactly
git fetch origin feature/file-upload-component
git reset --hard origin/feature/file-upload-component

```

### Alternative Solutions

Option 1: Merge (keeps both histories)

```bash
git pull origin feature/file-upload-component --no-rebase
```

Or set it permanently:

```bash
git config pull.rebase false
git pull origin feature/file-upload-component
```

Option 2: Rebase (cleaner history)

```bash
git pull origin feature/file-upload-component --rebase
```

Or set it permanently:

```bash
git config pull.rebase true
git pull origin feature/file-upload-component
```

Option 3: Fast-forward only (safest, but will fail if diverged)

```bash
git pull origin feature/file-upload-component --ff-only
```

Recommended Workflow for UAT Server
Since UAT should typically mirror your repository exactly:

```bash
# 1. Check what local changes exist
git status

# 2. If you have uncommitted changes, stash them
git stash

# 3. Fetch latest from remote
git fetch origin

# 4. See the difference between local and remote
git log HEAD..origin/feature/file-upload-component --oneline

# 5. Reset to match remote exactly (CAUTION: loses local commits)
git reset --hard origin/feature/file-upload-component

# 6. If you stashed changes and need them back
git stash pop
Check What's Different First
Before deciding, see what's different:
bash# See commits on your UAT server that aren't on remote
git log origin/feature/file-upload-component..HEAD

# See commits on remote that aren't on your UAT server
git log HEAD..origin/feature/file-upload-component
Best Practice for UAT Going Forward
Set up your UAT to always match remote:
bash# Make future pulls always reset to remote
git config pull.rebase false

# Or create a deployment script
#!/bin/bash
git fetch origin
git reset --hard origin/feature/file-upload-component

php artisan migrate
php artisan config:clear
php artisan cache:clear

```

Which approach should you use?
For a UAT server, I'd recommend the git reset --hard approach since UAT should match your repository exactly and shouldn't have unique local commits.

# GitHub Commands Cheat Sheet @

## General Commands

Setup & Config

```bash
git config -- global user.name "Your Name"
git config -- global user.email "you@example.com"
git config -- list

# --- Starting a Repo

git init  # Start new local repo


git clone <url> # Clone repo from GitHub

# --- Basic Workflow

git status  # Check status

git add <file>  # Stage a file

git add  # Stage all changes

git commit -m "message"  # Commit staged changes

git log  # Show commit history

# --- Branching
git branch

# List branches
git branch <name>

# Create new branch
git checkout <name>

# Switch to branch
git checkout -b <name>

# Create + switch branch

git merge <branch>

# Merge branch into current

git branch -d <name>

# Delete branch

# --- Remote (GitHub)
git remote -v # Show remotes

git remote add origin <url>  # Add remote origin

git push -u origin main # Push first time

git push  # Push changes

git pull # Pull latest changes

git fetch  # Fetch branches/tags

# --- Undo & Fix --
git checkout -- <file> # Discard changes (before staging)

git reset HEAD <file> # Unstage a file

git reset -- hard HEAD # Reset to last commit ( loses changes)

git revert <commit> # New commit that undoes a commit

# --- Stash
git stash # Save uncommitted changes

git stash pop # Reapply last stash

git stash list # Show stashes

# --- Tags -
git tag v1.0  # Create tag

git tag # List tags

git push origin v1.0 # Push tag to GitHub
```

## Working with Branch es

```bash
# on the same branch
git branch -m feature/resolve-reviewer-decisions # renames the current branch as "feature/resolve-reviewer-decisions"

# One liner without changing the branch
git branch -m old-branch-name new-branch-name

# Actual exmple I used to rename a branch
git branch -m featureresolve-reviewer-decisions feature/resolve-reviewer-decisions

```

## New Repo and Local Files

```bash
  🐉 > git init

  hint: Using 'master' as the name for the initial branch. This default branch name
  hint: is subject to change. To configure the initial branch name to use in all
  hint: of your new repositories, which will suppress this warning, call:

  hint:
  hint:   git config --global init.defaultBranch <name>

  hint:
  hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and

  hint: 'development'. The just-created branch can be renamed via this command:
  hint:

  hint:   git branch -m <name>

  # Initialized empty Git repository in /mnt/d/01 Apps/Development/Logs/CommandLists/.git/

  # Changed branch name to 'main' instead of "master"
  $ git branch -m main

  # Added the remote repo SSH to link it with the local files
  $ git remote add origin git@github.com:M-Bukhari/commands-list.git

  # Stage your files
  git add .     | #My shortcut
  gaa     # with my Bash Profile

  # Commit your files
  git commit -m "Initial commit"
  gcm "Initial commit"    # with my Bash Profile

  # Push your branch to GitHub
  git push -u origin main


  # Pull command with merge strategy
  git pull origin main --no-rebase --allow-unrelated-histories

  # Why this works
  --no-rebase: This explicitly tells Git to use the merge strategy. This satisfies the error Need to specify how to reconcile divergent branches (by choosing the merge option from the hint).

  --allow-unrelated-histories: This is still needed to combine the two different "Initial commits."
```

Merge Commit: Running this command will likely open a text editor (like Vim or Nano) asking you to confirm a "merge commit message."

The default message is usually fine.

To save and exit:
If it's Vim (looks complex): Type :wq and press Enter.
If it's Nano (bottom menu): Press Ctrl+X, then Y, then Enter.

The Final Push: After the pull is successful and your local files are merged, you can finally push your code to GitHub.

```bash
  git push -u origin main
```

### How to get to a previous point even if you have committed to the remote repo

Before we reset, let's create another backup branch pointing to your current HEAD (bc42382, the remote state) to preserve it, just in case you need to switch back later or to be extra cautious, let's create a backup branch specifically pointing to origin/main (bc42382) in case you need to reference or revert to the remote's state later. This won't change your current HEAD:

```bash
  git branch backup-origin-main

  git branch backup-origin-main origin/main
```

Once done, confirm by running:

```bash
  git branch -v
```

Run this command to switch back to main:

```bash
  git checkout main

  # After that, verify you're on main with:
  git branch -v

  # We'll reset it to the desired commit (b821feb). This will discard all changes and history after that commit on main
  git reset --hard b821feb

  # verify the reset worked by running:
  git log --oneline --graph --decorate -n 5

  # Output Result :
  # This will output the parent commit hash of bc42382 (it should be a single hash like b821feb if that's the case, or possibly more if it was a merge commit).
   $ git show --pretty=format:%P bc42382

    b821feb855385aafa3939db5e21dfe12fd3bc06f
    diff --git a/.env.example b/.env.example
    index c402466..f304d72 100644
    --- a/.env.example
    +++ b/.env.example
    @@ -96,3 +96,21 @@ ACTIVITY_LOG_QUEUE_NAME=default
    ACTIVITY_LOG_ALERTS_ENABLED=true
    ACTIVITY_LOG_ALERT_EMAIL=m.bukhari@abam.sa
    ACTIVITY_LOG_FAILED_LOGIN_THRESHOLD=5
    +
    +# Draft Management Configuration
    +DRAFTS_ENABLED=false
    +AUTO_SAVE_ENABLED=false
    +AUTO_SAVE_INTERVAL=60000
    +DRAFT_EXPIRY_DAYS=7
    +DRAFT_AUTO_CLEANUP=true
    +DRAFT_CLEANUP_THRESHOLD=30
    +DRAFT_ALLOW_RESUMPTION=false
    +DRAFT_SHOW_PROMPTS=false

```

Now that we've confirmed b821feb is indeed the parent (previous commit) of the remote's latest (bc42382), your local main is at the desired state. If you want to update the remote repository to match this (effectively removing the "New draft mgmt system implemented" commit from history, as shown in the diff), you can force-push your local main to origin/main. This rewrites remote history but is safe since you're the only developer—no one else will be affected.

```bash
  # Use --force-with-lease instead of plain --force for safety: it will fail if the remote has unexpected new commits (e.g., from another device).
  # Run the following command:

  git push origin main --force-with-lease


  # If it succeeds, verify the remote is updated by running:
  git fetch origin
  git log --oneline --graph --decorate -n 5 origin/main

```

### Get a file from another branch

There are several ways to get a file from another branch in Git:

#### Method 1: Checkout a Single File (Without Switching Branches)

```bash
  git checkout <branch-name> -- <file-path>

  #  Example:
  git checkout feature/new-design -- app/Models/User.php
  # This will bring the file from the specified branch into your current working directory (and stage it).
```

#### Method 2: View File Content Without Checking Out

If you just want to view or copy the content without modifying your working directory:

```bash
  git show <branch-name>:<file-path>

  # Example:
  git show feature/new-design:app/Models/User.php

  # You can redirect this to a new file:
  git show feature/new-design:app/Models/User.php > User_from_feature.php

```

#### Method 3: List Files in Another Branch

To see what files exist in another branch:
git ls-tree -r --name-only <branch-name>
Or to search for a specific file:
git ls-tree -r --name-only <branch-name> | grep "filename"

#### Method 4: Compare Files Between Branches

To see the differences between a file in your current branch and another branch:
git diff <branch-name> -- <file-path>
Example:
git diff feature/new-design -- app/Models/User.php

#### Method 5: Merge Just One File

If you want to merge changes from a specific file in another branch:
git checkout <branch-name> -- <file-path>
git add <file-path>
git commit -m "Merged <file-path> from <branch-name>"
Which method would you like to use? If you tell me which branch and which file you need, I can help you get it.
