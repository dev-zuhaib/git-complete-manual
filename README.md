# The Complete Git Command Reference Guide

## Table of Contents
- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Basic Commands](#basic-commands)
- [Branching and Merging](#branching-and-merging)
- [Remote Operations](#remote-operations)
- [Inspection and Comparison](#inspection-and-comparison)
- [Patching](#patching)
- [Debugging](#debugging)
- [Administration](#administration)
- [Advanced Operations](#advanced-operations)
- [Configuration](#configuration)
- [Git Workflows](#git-workflows)

## Introduction

Git is a distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

## Getting Started

### Installation

**Linux (Debian/Ubuntu):**
```bash
sudo apt-get update
sudo apt-get install git
```

**macOS:**
```bash
brew install git
```

**Windows:**
Download the installer from [git-scm.com](https://git-scm.com/)

### Check Git Version
```bash
git --version
```

### Initial Setup

**Setting your identity:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Setting your default editor:**
```bash
git config --global core.editor "vim"  # or "nano", "code --wait", etc.
```

## Basic Commands

### git init

**Purpose:** Initialize a new Git repository

**Syntax:**
```bash
git init [directory]
```

**Options:**
- `--bare`: Create a bare repository (without a working directory)
- `--shared[=permissions]`: Specify permissions for shared repositories

**Examples:**
```bash
# Initialize in current directory
git init

# Initialize in a specific directory
git init my-project

# Create a bare repository
git init --bare project.git
```

### git clone

**Purpose:** Clone an existing repository

**Syntax:**
```bash
git clone [url] [directory]
```

**Options:**
- `--branch, -b <name>`: Checkout specific branch instead of HEAD
- `--depth <depth>`: Create a shallow clone with limited history
- `--recursive`: Clone submodules too
- `--single-branch`: Clone only one branch
- `--mirror`: Set up a mirror of the source repository

**Examples:**
```bash
# Basic clone
git clone https://github.com/username/repository.git

# Clone to specific directory
git clone https://github.com/username/repository.git my-project

# Clone specific branch
git clone -b develop https://github.com/username/repository.git

# Shallow clone (only recent history)
git clone --depth=1 https://github.com/username/repository.git
```

### git add

**Purpose:** Add files to staging area

**Syntax:**
```bash
git add [file(s)]
```

**Options:**
- `-A, --all`: Add all files (modified, new and deleted)
- `-u, --update`: Add modified and deleted files, not new ones
- `-p, --patch`: Interactively choose hunks to stage
- `-n, --dry-run`: Don't actually add files, just show what would be done
- `-f, --force`: Allow adding otherwise ignored files
- `-i, --interactive`: Interactive adding

**Examples:**
```bash
# Add specific file
git add file.txt

# Add multiple files
git add file1.js file2.js

# Add all .js files in current directory
git add *.js

# Add all files in a directory
git add directory/

# Add all files (modified, new and deleted)
git add -A
git add --all
git add .  # In recent Git versions, this behaves like -A

# Add only modified and deleted files (not new)
git add -u

# Interactive staging
git add -i

# Interactively choose parts of files to stage
git add -p
```

### git commit

**Purpose:** Record changes to the repository

**Syntax:**
```bash
git commit
```

**Options:**
- `-m <message>`: Use provided message as commit message
- `-a, --all`: Automatically stage modified and deleted files
- `--amend`: Amend previous commit
- `-S`: Sign commit using GPG
- `--no-verify`: Bypass pre-commit and commit-msg hooks
- `--date`: Specify commit date
- `-p, --patch`: Interactively choose hunks to commit

**Examples:**
```bash
# Basic commit
git commit -m "Add new feature"

# Commit all modified files without staging
git commit -a -m "Fix all bugs"

# Amend the previous commit
git commit --amend -m "New commit message"

# Amend previous commit without changing message
git commit --amend --no-edit

# Commit with signature
git commit -S -m "Signed commit"

# Interactive patch commit
git commit -p
```

### git status

**Purpose:** Show working tree status

**Syntax:**
```bash
git status
```

**Options:**
- `-s, --short`: Give output in short format
- `-b, --branch`: Show branch information
- `-u, --untracked-files[=mode]`: Show untracked files (modes: no, normal, all)
- `--ignored`: Show ignored files as well
- `--column[=options]`: Display in columns

**Examples:**
```bash
# Standard status
git status

# Short format status
git status -s

# Show branch info with short format
git status -sb

# Show untracked directories and files
git status -u

# Show ignored files
git status --ignored
```

### git rm

**Purpose:** Remove files from working tree and index

**Syntax:**
```bash
git rm [file(s)]
```

**Options:**
- `-f, --force`: Override safety checks
- `-r`: Allow recursive removal
- `--cached`: Remove only from the index, not the working directory
- `-n, --dry-run`: Don't actually remove, just show what would happen
- `--ignore-unmatch`: Exit with zero status even if no files match

**Examples:**
```bash
# Remove file from both index and working directory
git rm file.txt

# Remove directory recursively
git rm -r directory/

# Remove file only from the index (keep it in working directory)
git rm --cached file.txt

# Force removal even if file has uncommitted changes
git rm -f file.txt
```

### git mv

**Purpose:** Move or rename files, directories

**Syntax:**
```bash
git mv <source> <destination>
```

**Options:**
- `-f, --force`: Force move even if target exists
- `-k`: Skip move/rename errors
- `-n, --dry-run`: Don't actually move, just show what would happen
- `-v, --verbose`: Report names of files as they are moved

**Examples:**
```bash
# Rename a file
git mv old_name.txt new_name.txt

# Move a file to a different directory
git mv file.txt directory/

# Force move even if target exists
git mv -f source.txt destination.txt
```

## Branching and Merging

### git branch

**Purpose:** List, create, or delete branches

**Syntax:**
```bash
git branch [options] [branch-name]
```

**Options:**
- `-a, --all`: List both remote-tracking and local branches
- `-r, --remotes`: List remote-tracking branches
- `-v, --verbose`: Show commit descriptions
- `-vv`: Show tracking branches
- `-d, --delete`: Delete a branch
- `-D`: Force delete a branch
- `-m, --move`: Move/rename a branch
- `-M`: Force move/rename a branch
- `--merged`: List branches merged into HEAD
- `--no-merged`: List branches not merged into HEAD
- `--contains <commit>`: List branches containing specified commit

**Examples:**
```bash
# List local branches (* marks current branch)
git branch

# List all branches including remote branches
git branch -a

# List only remote branches
git branch -r

# List all branches with last commit message
git branch -av

# Show which remote branches are tracked
git branch -vv

# Create a new branch (without switching to it)
git branch new-feature

# Create a branch at specific commit
git branch new-feature 5e23f12

# Delete branch (safe - won't delete if changes not merged)
git branch -d old-branch

# Force delete branch
git branch -D old-branch

# Rename current branch
git branch -m new-name

# List branches merged into current branch
git branch --merged

# List branches not merged into current branch
git branch --no-merged

# List branches containing specific commit
git branch --contains 5e23f12
```

### git checkout

**Purpose:** Switch branches or restore working tree files

**Syntax:**
```bash
git checkout [options] <branch|commit|file>
```

**Options:**
- `-b <new-branch>`: Create and checkout a new branch
- `-B <new-branch>`: Create/reset and checkout a branch
- `-f, --force`: Force checkout (throw away local changes)
- `-t, --track`: Set upstream info for new branch
- `--orphan <new-branch>`: Create a new orphan branch
- `--detach`: Detach HEAD at named commit
- `--merge`: Merge between starting point and working tree
- `--patch`: Interactively select hunks to discard
- `-q, --quiet`: Suppress progress reports

**Examples:**
```bash
# Switch to an existing branch
git checkout develop

# Create and switch to a new branch
git checkout -b feature/login

# Create and switch to tracking branch
git checkout -t origin/feature 

# Checkout specific commit (detached HEAD)
git checkout a32c105

# Discard changes to a specific file
git checkout -- file.txt

# Discard changes to multiple files
git checkout -- file1.txt file2.txt

# Create new orphan branch
git checkout --orphan new-start

# Force checkout (discard all local changes)
git checkout -f master

# Interactively restore parts of files
git checkout --patch file.txt
```

### git switch (Git 2.23+)

**Purpose:** Switch branches (modern alternative to git checkout for branch operations)

**Syntax:**
```bash
git switch [options] <branch>
```

**Options:**
- `-c, --create <new-branch>`: Create and switch to new branch
- `-C <new-branch>`: Create/reset and switch to new branch
- `--detach`: Detach HEAD at named commit
- `--discard-changes`: Throw away local modifications
- `-f, --force`: Force switch even if working tree is dirty
- `--orphan <new-branch>`: Create a new orphan branch
- `-t, --track`: Set upstream info for new branch

**Examples:**
```bash
# Switch to an existing branch
git switch main

# Create and switch to a new branch
git switch -c feature/auth

# Force switch (discarding local changes)
git switch -f main

# Create an orphan branch
git switch --orphan new-history

# Detach HEAD at specific branch
git switch --detach origin/main
```

### git restore (Git 2.23+)

**Purpose:** Restore working tree files (modern alternative to git checkout for file operations)

**Syntax:**
```bash
git restore [options] [file...]
```

**Options:**
- `-s, --source <tree>`: Restore from specific source
- `-p, --patch`: Interactive selection
- `-W, --worktree`: Restore working tree (default)
- `-S, --staged`: Restore staged content
- `--staged --worktree`: Restore both
- `--no-progress`: Suppress progress reports

**Examples:**
```bash
# Restore a file (discard changes)
git restore file.txt

# Restore multiple files
git restore file1.js file2.js

# Restore a file from specific commit
git restore --source=HEAD~2 file.txt

# Unstage a file (restore index)
git restore --staged file.txt

# Unstage and restore working tree
git restore --staged --worktree file.txt

# Interactive restore
git restore -p file.txt
```

### git merge

**Purpose:** Join two or more development histories together

**Syntax:**
```bash
git merge [options] [branch]
```

**Options:**
- `--ff`: Fast-forward merge when possible (default)
- `--no-ff`: Create a merge commit even if fast-forward possible
- `--ff-only`: Abort if not possible to fast-forward
- `--squash`: Create single commit instead of merge
- `--commit`: Perform the merge and commit the result
- `--no-commit`: Perform the merge but don't commit
- `--stat`: Show a diffstat after merge
- `-m <message>`: Set the commit message
- `--abort`: Abort the current merge
- `--continue`: Continue after resolving conflicts
- `-S`: Sign the merge commit
- `-X<option>`: Pass merge strategy option
  - `-Xignore-all-space`: Ignore whitespace
  - `-Xours`: Favor our version
  - `-Xtheirs`: Favor their version

**Examples:**
```bash
# Standard merge
git merge feature-branch

# Create a merge commit always
git merge --no-ff feature-branch

# Fast-forward only (no commit created)
git merge --ff-only hotfix

# Squash all commits into one without merging
git merge --squash feature-branch

# Set commit message for merge
git merge -m "Merging feature X" feature-branch

# Merge with custom strategy options
git merge -X ignore-all-space feature-branch

# Abort current merge with conflicts
git merge --abort

# Sign the merge commit
git merge -S feature-branch
```

### git rebase

**Purpose:** Reapply commits on top of another base

**Syntax:**
```bash
git rebase [options] [base]
```

**Options:**
- `-i, --interactive`: Interactive rebase
- `--onto <newbase>`: Specify a new base
- `--continue`: Continue after resolving conflicts
- `--abort`: Abort the rebase
- `--skip`: Skip current patch
- `--edit-todo`: Edit the todo list
- `-m, --merge`: Use merging strategies
- `-S`: GPG-sign commits
- `--autosquash`: Automatically squash commits
- `--autostash`: Automatically stash/unstash

**Examples:**
```bash
# Basic rebase
git rebase master

# Rebase with a new base
git rebase --onto master feature parent-branch

# Interactive rebase for last 3 commits
git rebase -i HEAD~3

# Continue rebase after resolving conflicts
git rebase --continue

# Abort the rebase operation
git rebase --abort

# Skip the current patch
git rebase --skip

# Interactive rebase with autosquash
git rebase -i --autosquash HEAD~5

# Rebase with automatic stashing
git rebase --autostash master
```

### git cherry-pick

**Purpose:** Apply changes from specific commits

**Syntax:**
```bash
git cherry-pick [options] <commit>...
```

**Options:**
- `-e, --edit`: Edit commit message
- `-n, --no-commit`: Apply changes without committing
- `-x`: Add "(cherry picked from...)" to message
- `-s, --signoff`: Add Signed-off-by line
- `-m <parent-number>`: Select parent of a merge
- `--continue`: Continue after resolving conflicts
- `--abort`: Cancel cherry-pick
- `--skip`: Skip current commit
- `-S`: GPG-sign commits

**Examples:**
```bash
# Cherry-pick a single commit
git cherry-pick 5e23f12

# Cherry-pick a range of commits
git cherry-pick 5e23f12..8e41abc

# Cherry-pick without committing
git cherry-pick -n 5e23f12

# Cherry-pick with attribution
git cherry-pick -x 5e23f12

# Cherry-pick a specific parent of a merge commit
git cherry-pick -m 1 5e23f12

# Cherry-pick with signed commit
git cherry-pick -S 5e23f12

# Continue cherry-pick after resolving conflicts
git cherry-pick --continue
```

### git tag

**Purpose:** Create, list, delete or verify tags

**Syntax:**
```bash
git tag [options] [tagname] [commit]
```

**Options:**
- `-a`: Create an annotated tag
- `-s`: Make a GPG-signed tag
- `-m <message>`: Tag message
- `-f`: Replace existing tag
- `-d <tagname>`: Delete tag
- `-l, --list`: List tags
- `-n[<num>]`: Print <num> lines of tag message
- `-v`: Verify signature of tag
- `--sort=<key>`: Sort based on key

**Examples:**
```bash
# List all tags
git tag

# List tags matching pattern
git tag -l "v1.8.*"

# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Version 1.0.0"

# Create tag for specific commit
git tag -a v1.0.0 5e23f12 -m "Version 1.0.0"

# Create signed tag
git tag -s v1.0.0 -m "Signed version 1.0.0"

# Delete a tag
git tag -d v0.9.0

# List tags with messages
git tag -n

# Verify a signed tag
git tag -v v1.0.0
```

## Remote Operations

### git remote

**Purpose:** Manage remote repositories

**Syntax:**
```bash
git remote [options] <subcommand>
```

**Options:**
- `-v, --verbose`: Be verbose

**Subcommands:**
- `add`: Add a new remote
- `rename`: Rename a remote
- `remove, rm`: Remove a remote
- `set-url`: Change remote URL
- `get-url`: Print remote URL
- `show`: Show information about remote
- `prune`: Remove stale remote-tracking branches
- `set-head`: Set default branch
- `set-branches`: Change the list of tracked branches

**Examples:**
```bash
# List all remotes
git remote

# List remotes with URLs
git remote -v

# Add a new remote
git remote add origin https://github.com/username/repo.git

# Add another remote
git remote add upstream https://github.com/original/repo.git

# Remove a remote
git remote remove backup

# Rename a remote
git remote rename origin github

# Change remote URL
git remote set-url origin https://github.com/newname/repo.git

# Show info about a remote
git remote show origin

# Prune deleted remote branches
git remote prune origin

# Set default branch for a remote
git remote set-head origin main
```

### git fetch

**Purpose:** Download objects and refs from remote repository

**Syntax:**
```bash
git fetch [options] [remote] [branch]
```

**Options:**
- `--all`: Fetch from all remotes
- `-p, --prune`: Remove remote-tracking branches no longer on remote
- `-t, --tags`: Fetch all tags
- `--dry-run`: Show what would be done
- `-f, --force`: Force overwriting local branches
- `-j <n>`: Number of parallel jobs
- `--depth=<depth>`: Limit history depth
- `-q, --quiet`: Be quiet
- `-v, --verbose`: Be verbose

**Examples:**
```bash
# Fetch from default remote
git fetch

# Fetch from specific remote
git fetch origin

# Fetch specific branch
git fetch origin feature

# Fetch all remotes
git fetch --all

# Fetch with pruning
git fetch -p

# Fetch with tags
git fetch --tags

# Fetch specific tags
git fetch origin tag v1.0.0

# Force fetch
git fetch -f origin

# Shallow fetch (limit depth)
git fetch --depth=1 origin
```

### git pull

**Purpose:** Fetch from and integrate with another repository or branch

**Syntax:**
```bash
git pull [options] [remote] [branch]
```

**Options:**
- `--ff`: Fast-forward if possible (default)
- `--no-ff`: Create a merge commit even if fast-forward possible
- `--ff-only`: Only fast-forward
- `--rebase[=preserve]`: Rebase instead of merge
- `--no-rebase`: Merge instead of rebasing
- `-p, --prune`: Prune remote-tracking branches
- `--autostash`: Stash before pulling and apply afterwards
- `-s, --strategy=<strategy>`: Merge strategy
- `-X<option>`: Pass strategy option
- `--allow-unrelated-histories`: Merge unrelated histories

**Examples:**
```bash
# Standard pull
git pull

# Pull from specific remote and branch
git pull origin main

# Pull using rebase
git pull --rebase

# Pull using rebase and preserve merges
git pull --rebase=preserve

# Pull with fast-forward only
git pull --ff-only

# Pull with prune
git pull --prune

# Pull with autostash
git pull --autostash

# Pull allowing unrelated histories
git pull --allow-unrelated-histories

# Pull with custom merge strategy
git pull -s recursive -X theirs
```

### git push

**Purpose:** Update remote refs along with associated objects

**Syntax:**
```bash
git push [options] [remote] [branch]
```

**Options:**
- `-u, --set-upstream`: Set upstream for git pull/status
- `--all`: Push all branches
- `--mirror`: Push all refs
- `--tags`: Push all tags
- `--follow-tags`: Push commits and tags
- `--force, -f`: Force push
- `--force-with-lease`: Force push if remote hasn't changed
- `--delete`: Delete refs
- `--prune`: Remove remote branches not in local
- `-n, --dry-run`: Do everything except actually push
- `--atomic`: Push all refs or none
- `--push-option=<option>`: Transmit push options

**Examples:**
```bash
# Push to default remote and branch
git push

# Push to specific remote and branch
git push origin main

# Push and set upstream
git push -u origin feature

# Push all branches
git push --all

# Push all tags
git push --tags

# Push commits and relevant tags
git push --follow-tags

# Force push
git push -f origin main

# Force push with safety checks
git push --force-with-lease origin feature

# Delete remote branch
git push origin --delete old-feature

# Push to multiple remotes
git push origin backup

# Dry run (see what would be pushed)
git push --dry-run origin main

# Push with prune
git push --prune origin
```

## Inspection and Comparison

### git log

**Purpose:** Show commit logs

**Syntax:**
```bash
git log [options] [revision range] [[--] path...]
```

**Options:**
- `-p, --patch`: Show diffs
- `--stat`: Show diffstat
- `--shortstat`: Show only changed/insertions/deletions
- `--name-only`: Show only names of changed files
- `--name-status`: Show names and status of changed files
- `--abbrev-commit`: Show short commit hashes
- `--oneline`: One line per commit
- `--graph`: Show ASCII graph of branch and merge history
- `--date=<format>`: Date format (relative, local, iso, etc.)
- `-n <number>`: Limit number of commits
- `--since=<date>`: Show commits more recent than a date
- `--until=<date>`: Show commits older than a date
- `--author=<pattern>`: Limit to specific author
- `--committer=<pattern>`: Limit to specific committer
- `--grep=<pattern>`: Limit to commits with log message matching pattern
- `-S<string>`: Look for differences with string
- `-G<regex>`: Look for differences matching regex
- `--merges`: Show only merge commits
- `--no-merges`: Hide merge commits
- `--first-parent`: Follow only first parent of merges

**Examples:**
```bash
# Standard log
git log

# Show last 5 commits
git log -5

# One commit per line
git log --oneline

# Show log graph
git log --graph --oneline --decorate --all

# Show diffs for each commit
git log -p

# Show stats for each commit
git log --stat

# Show commits since yesterday
git log --since=yesterday

# Show commits between dates
git log --since="2023-01-01" --until="2023-01-31"

# Show commits by author
git log --author="John Doe"

# Show commits containing a specific message
git log --grep="fix"

# Show commits that added or removed a string
git log -S"function getName"

# Show commits modifying specific files
git log -- file.js directory/

# Show merge commits only
git log --merges

# Show non-merge commits only
git log --no-merges

# Show commit details in pretty format
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short
```

### git diff

**Purpose:** Show changes between commits, commit and working tree, etc.

**Syntax:**
```bash
git diff [options] [<commit>] [--] [<path>...]
```

**Options:**
- `--staged, --cached`: Compare staged changes with last commit
- `--name-only`: Show only names of changed files
- `--name-status`: Show names and status of changed files
- `--stat`: Generate a diffstat
- `--check`: Check for whitespace errors
- `-b, --ignore-space-change`: Ignore changes in amount of whitespace
- `-w, --ignore-all-space`: Ignore whitespace
- `--color`: Show colored diff
- `--word-diff`: Show word diff
- `-R`: Swap input, helpful for applying patches
- `--patience`: Use patience diff algorithm
- `--histogram`: Use histogram diff algorithm

**Examples:**
```bash
# Unstaged changes
git diff

# Staged changes
git diff --staged

# Diff between branches
git diff main feature

# Changes between specific commits
git diff 5e23f12 8e41abc

# Changes between HEAD and specific commit
git diff HEAD~3

# Changes to specific files
git diff -- file.js directory/

# Just show names of changed files
git diff --name-only

# Show stats about changes
git diff --stat

# Ignore whitespace changes
git diff -w

# Word-level diffs
git diff --word-diff

# Use better diff algorithm
git diff --patience

# Check for whitespace errors
git diff --check
```

### git show

**Purpose:** Show various types of objects (commits, tags, files)

**Syntax:**
```bash
git show [options] [object]
```

**Options:**
- Same options as git diff
- `--pretty=<format>`: Format output
- `--abbrev-commit`: Show abbreviated commit hash
- `--no-patch`: Suppress diff output

**Examples:**
```bash
# Show current commit
git show

# Show specific commit
git show 5e23f12

# Show commit with stats
git show --stat 5e23f12

# Show tag
git show v1.0.0

# Show file at specific commit
git show 5e23f12:file.js

# Show tree object
git show 5e23f12^{tree}

# Show abbreviated info
git show --abbrev-commit --oneline 5e23f12

# Show pretty format
git show --pretty=format:"%h - %an, %ar : %s" 5e23f12

# Show merge commit with combined diff
git show 5e23f12 -c
```

### git blame

**Purpose:** Show who changed what line, when

**Syntax:**
```bash
git blame [options] [file]
```

**Options:**
- `-L <start>,<end>`: Annotate only lines within range
- `-s`: Suppress author name and timestamp
- `-e`: Show author email instead of name
- `-w`: Ignore whitespace changes
- `--since=<date>`: Ignore changes older than date
- `-M`: Detect moved or copied lines
- `-C`: Detect code moved from other files
- `--color-lines`: Color lines
- `--color-by-age`: Color by age
- `-f, --show-name`: Show filename in output

**Examples:**
```bash
# Blame a file
git blame file.js

# Blame specific line range
git blame -L 10,20 file.js

# Blame ignoring whitespace
git blame -w file.js

# Show email instead of username
git blame -e file.js

# Detect moved lines within same file
git blame -M file.js

# Detect code moved from other files
git blame -C file.js

# Ignore changes older than 3 weeks
git blame --since="3 weeks ago" file.js

# Show filename in each line
git blame -f file.js
```

### git bisect

**Purpose:** Find the commit that introduced a bug using binary search

**Syntax:**
```bash
git bisect <subcommand>
```

**Subcommands:**
- `start`: Start bisect session
- `good [commit]`: Mark commit as good
- `bad [commit]`: Mark commit as bad
- `skip [commit]`: Skip current revision
- `reset`: End bisect session
- `run <cmd>`: Run command to automatically verify each commit

**Examples:**
```bash
# Start a bisect session
git bisect start

# Mark current version as bad
git bisect bad

# Mark older version as good
git bisect good v1.0.0

# After testing the current commit, mark it
git bisect good  # or git bisect bad

# Skip a commit that cannot be tested
git bisect skip

# End the bisect session
git bisect reset

# Automatic bisect with test command
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
git bisect run npm test
```

## Patching

### git apply

**Purpose:** Apply a patch to files and/or index

**Syntax:**
```bash
git apply [options] [patch]
```

**Options:**
- `--stat`: Show diffstat instead of applying
- `--check`: Check if patch applies cleanly
- `--index`: Apply patch to index and worktree
- `--cached`: Apply patch to index only
- `--3way`: Attempt three-way merge
- `-R, --reverse`: Apply the patch in reverse
- `--reject`: Leave rejected hunks in .rej files
- `--ignore-space-change`: Ignore changes in whitespace
- `--whitespace=<action>`: Handle whitespace errors

**Examples:**
```bash
# Apply a patch file
git apply patch.diff

# Check if a patch will apply cleanly
git apply --check patch.diff

# Apply to index only
git apply --cached patch.diff

# Apply with three-way merge
git apply --3way patch.diff

# Apply in reverse
git apply -R patch.diff

# Show stats about the patch
git apply --stat patch.diff

# Apply ignoring whitespace
git apply --ignore-space-change patch.diff
```

### git format-patch

**Purpose:** Create patches for e-mail submission

**Syntax:**
```bash
git format-patch [options] [revision range]
```

**Options:**
- `-o <dir>`: Output to directory
- `--numbered`: Name output in [PATCH n/m] format
- `--cover-letter`: Generate a cover letter
- `--signoff`: Add Signed-off-by line
- `--in-reply-to=<message-id>`: Make first mail a reply
- `--thread`: Thread messages
- `--subject-prefix=<prefix>`: Use [prefix] instead of [PATCH]
- `-n, --numbered-files`: Use numbers for filenames
- `--start-number <n>`: Start numbering at <n>
- `--signature=<signature>`: Add a signature
- `--no-signature`: Don't add a signature

**Examples:**
```bash
# Create patch for last commit
git format-patch -1

# Create patches for all commits since a tag
git format-patch v1.0.0

# Create patches for range
git format-patch HEAD~3..HEAD

# Write patches to directory
git format-patch -o patches/ HEAD~3

# Create numbered patches
git format-patch --numbered HEAD~3

# Add cover letter
git format-patch --cover-letter HEAD~3

# Create patch with signature
git format-patch --signature="John Doe" -1

# Create patch with custom subject prefix
git format-patch --subject-prefix

# Create patch with custom subject prefix
git format-patch --subject-prefix="BUG-FIX" -1

# Create patch as reply to message ID
git format-patch --in-reply-to="<20230215121212.GA12345@example.com>" -1
```

### git am

**Purpose:** Apply patches from mailbox

**Syntax:**
```bash
git am [options] [mailbox]
```

**Options:**
- `-3, --3way`: Use three-way merge if needed
- `--ignore-space-change`: Ignore changes in whitespace
- `--ignore-whitespace`: Ignore all whitespace
- `--whitespace=<action>`: Handle whitespace errors
- `--committer-date-is-author-date`: Use author date as committer date
- `--skip`: Skip the current patch
- `--abort`: Abort the patching operation
- `--resolved`: Continue after resolving conflicts
- `-i, --interactive`: Run interactively
- `--reject`: Leave rejected hunks in .rej files
- `-q, --quiet`: Be quiet
- `-s, --signoff`: Add Signed-off-by line to commit message

**Examples:**
```bash
# Apply all patches in directory
git am patches/*.patch

# Apply with 3-way merge
git am -3 patches/*.patch

# Apply and sign off
git am -s patches/*.patch

# Apply interactively
git am -i patches/*.patch

# Continue after resolving conflicts
git am --resolved

# Skip current patch
git am --skip

# Abort am session
git am --abort

# Apply with committer date same as author date
git am --committer-date-is-author-date patches/*.patch
```

### git stash

**Purpose:** Stash changes in a dirty working directory

**Syntax:**
```bash
git stash [subcommand]
```

**Subcommands:**
- `push [-m <message>]`: Save changes to stash (default if no subcommand)
- `list`: List stashes
- `show [stash@{n}]`: Show changes in stash
- `pop [stash@{n}]`: Apply and remove stash
- `apply [stash@{n}]`: Apply stash without removing it
- `branch <branchname> [stash@{n}]`: Create a branch from stash
- `drop [stash@{n}]`: Remove a stash
- `clear`: Remove all stashes
- `create`: Create a stash without storing it

**Options:**
- `-a, --all`: Include ignored files
- `-u, --include-untracked`: Include untracked files
- `-p, --patch`: Interactively select hunks
- `--keep-index`: Don't stash changes already in the index

**Examples:**
```bash
# Stash current changes
git stash

# Stash with a message
git stash push -m "WIP: feature implementation"

# Stash including untracked files
git stash -u

# Stash with interactive selection
git stash -p

# List all stashes
git stash list

# Show changes in latest stash
git stash show

# Show changes with diff
git stash show -p

# Apply latest stash (keep it in stash list)
git stash apply

# Apply specific stash
git stash apply stash@{2}

# Apply and remove latest stash
git stash pop

# Create a branch from stash
git stash branch new-branch stash@{1}

# Remove a specific stash
git stash drop stash@{1}

# Clear all stashes
git stash clear
```

## Debugging

### git grep

**Purpose:** Print lines matching a pattern

**Syntax:**
```bash
git grep [options] <pattern> [<path>...]
```

**Options:**
- `-n, --line-number`: Show line numbers
- `-i, --ignore-case`: Case insensitive match
- `-l, --files-with-matches`: Show only filenames
- `-L, --files-without-match`: Show only the names of files without match
- `--name-only`: Same as -l
- `-c, --count`: Show the number of matches per file
- `-p, --show-function`: Show function context
- `--and, --or, --not`: Combine patterns
- `-W, --function-context`: Show whole function
- `--cached`: Search in index instead of working tree
- `-A <num>`: Show <num> context lines after match
- `-B <num>`: Show <num> context lines before match
- `-C <num>`: Show <num> context lines

**Examples:**
```bash
# Basic search
git grep "function"

# Case insensitive search
git grep -i "function"

# Show line numbers
git grep -n "TODO"

# Show only filenames with matches
git grep -l "TODO"

# Show files without matches
git grep -L "TODO"

# Count matches per file
git grep -c "function"

# Show function context
git grep -p "getElementById"

# Search in specific path
git grep "import React" src/

# Search in index
git grep --cached "deprecated"

# Search with context
git grep -A 2 -B 2 "error handling"

# Complex search (AND condition)
git grep -e "function" --and -e "return"

# Search in specific commit
git grep "function" 5e23f12
```

### git reflog

**Purpose:** Manage reflog information

**Syntax:**
```bash
git reflog [subcommand] [options]
```

**Subcommands:**
- `show`: Show log of reference states (default)
- `expire`: Prune old reflog entries
- `delete`: Delete entries from reflog
- `exists`: Check if a ref has a reflog

**Options:**
- `--all`: Process all refs
- `--expire=<time>`: Prune entries older than specified time
- `--expire-unreachable=<time>`: Prune unreachable entries older than time
- `-n, --dry-run`: Just show what would be done
- `-v, --verbose`: Be verbose

**Examples:**
```bash
# Show reflog
git reflog

# Show reflog for specific branch
git reflog show feature

# Expire old reflog entries
git reflog expire --expire=30.days

# Expire unreachable entries
git reflog expire --expire-unreachable=7.days --all

# Delete a specific reflog entry
git reflog delete master@{2}

# Check if a ref has a reflog
git reflog exists feature
```

### git fsck

**Purpose:** Verify the connectivity and validity of objects in the database

**Syntax:**
```bash
git fsck [options]
```

**Options:**
- `--unreachable`: Show unreachable objects
- `--dangling`: Show dangling objects
- `--no-reflogs`: Do not use reflogs to find reachability
- `--full`: Check all objects
- `--connectivity-only`: Check connectivity only
- `--strict`: Be more strict in finding issues
- `-v, --verbose`: Be verbose

**Examples:**
```bash
# Basic integrity check
git fsck

# Show dangling objects
git fsck --dangling

# Show unreachable objects
git fsck --unreachable

# Full database check
git fsck --full

# Strict check
git fsck --strict

# Check without using reflogs
git fsck --no-reflogs
```

## Administration

### git gc

**Purpose:** Cleanup unnecessary files and optimize the local repository

**Syntax:**
```bash
git gc [options]
```

**Options:**
- `--aggressive`: More aggressive optimization
- `--auto`: Run if needed
- `--prune=<date>`: Prune objects older than date
- `--no-prune`: Don't prune any loose objects
- `-q, --quiet`: Be quiet

**Examples:**
```bash
# Standard garbage collection
git gc

# More aggressive optimization
git gc --aggressive

# Run only if needed
git gc --auto

# Run with pruning
git gc --prune=now

# Quiet operation
git gc --quiet
```

### git prune

**Purpose:** Prune all unreachable objects

**Syntax:**
```bash
git prune [options]
```

**Options:**
- `--dry-run`: Just show what would be removed
- `--verbose`: Report all removed objects
- `--expire <time>`: Only expire objects older than time

**Examples:**
```bash
# Prune unreachable objects
git prune

# Show what would be pruned
git prune --dry-run

# Show details of pruned objects
git prune --verbose

# Prune objects older than 2 weeks
git prune --expire="2.weeks.ago"
```

### git clean

**Purpose:** Remove untracked files from working tree

**Syntax:**
```bash
git clean [options]
```

**Options:**
- `-n, --dry-run`: Don't actually remove files
- `-f, --force`: Force removal
- `-d`: Remove untracked directories too
- `-x`: Remove ignored files too
- `-X`: Remove only ignored files
- `-i, --interactive`: Interactive cleaning
- `-e <pattern>`: Exclude pattern

**Examples:**
```bash
# Preview what would be deleted
git clean -n

# Force removal of untracked files
git clean -f

# Remove untracked files and directories
git clean -fd

# Remove both untracked and ignored files
git clean -fx

# Remove only ignored files
git clean -fX

# Interactive cleaning
git clean -i

# Clean excluding specific patterns
git clean -f -e "*.log"
```

## Advanced Operations

### git worktree

**Purpose:** Manage multiple working trees

**Syntax:**
```bash
git worktree [subcommand] [options]
```

**Subcommands:**
- `add`: Create a new working tree
- `list`: List details of working trees
- `lock`: Lock a working tree
- `move`: Move a working tree
- `prune`: Prune working tree information
- `remove`: Remove a working tree
- `unlock`: Unlock a working tree

**Examples:**
```bash
# List working trees
git worktree list

# Create a new working tree
git worktree add ../hotfix hotfix-branch

# Create a new branch and working tree
git worktree add -b emergency-fix ../emergency-fix main

# Remove a working tree
git worktree remove ../hotfix

# Prune stale working tree information
git worktree prune

# Lock a working tree
git worktree lock ../hotfix --reason="Sensitive changes"

# Unlock a working tree
git worktree unlock ../hotfix
```

### git submodule

**Purpose:** Initialize, update or inspect submodules

**Syntax:**
```bash
git submodule [subcommand] [options]
```

**Subcommands:**
- `add`: Add a submodule
- `status`: Show status of submodules
- `init`: Initialize submodules
- `update`: Update submodules
- `deinit`: Unregister submodules
- `foreach`: Run command on each submodule
- `sync`: Sync submodules' URL configuration
- `absorbgitdirs`: Move .git directories to superproject

**Examples:**
```bash
# Add a submodule
git submodule add https://github.com/username/library.git lib/library

# Initialize submodules
git submodule init

# Update submodules
git submodule update

# Initialize and update in one command
git submodule update --init

# Update recursively (including nested submodules)
git submodule update --init --recursive

# Execute command in each submodule
git submodule foreach 'git checkout master'

# Sync remote URL changes
git submodule sync

# Remove a submodule
git submodule deinit lib/library
git rm lib/library
```

### git filter-branch

**Purpose:** Rewrite branches

**Syntax:**
```bash
git filter-branch [options] [--] [<rev-list options>]
```

**Options:**
- `--env-filter <command>`: Modify commit environments
- `--tree-filter <command>`: Rewrite the tree and its contents
- `--index-filter <command>`: Rewrite the index
- `--parent-filter <command>`: Rewrite parent relationships
- `--msg-filter <command>`: Rewrite commit messages
- `--commit-filter <command>`: Rewrite commit objects
- `--tag-name-filter <command>`: Rewrite tag names
- `--subdirectory-filter <dir>`: Only look at history in a subdirectory
- `--prune-empty`: Prune empty commits
- `-f, --force`: Force operation

**Examples:**
```bash
# Remove a file from entire history
git filter-branch --index-filter 'git rm --cached --ignore-unmatch password.txt' HEAD

# Change author name/email in history
git filter-branch --env-filter '
  if [ "$GIT_AUTHOR_EMAIL" = "old@example.com" ]; then
    export GIT_AUTHOR_EMAIL="new@example.com"
    export GIT_AUTHOR_NAME="New Name"
  fi
  if [ "$GIT_COMMITTER_EMAIL" = "old@example.com" ]; then
    export GIT_COMMITTER_EMAIL="new@example.com"
    export GIT_COMMITTER_NAME="New Name"
  fi
' HEAD

# Extract subdirectory into its own repo
git filter-branch --subdirectory-filter lib HEAD

# Rewrite all commit messages
git filter-branch --msg-filter 'sed "s/typo/error/g"' HEAD

# Prune empty commits
git filter-branch --prune-empty HEAD
```

### git revert

**Purpose:** Revert some existing commits

**Syntax:**
```bash
git revert [options] <commit>...
```

**Options:**
- `-e, --edit`: Edit commit message
- `--no-edit`: Don't edit commit message
- `--no-commit`: Don't commit immediately
- `-n, --no-commit`: Same as --no-commit
- `-m <parent-number>`: Parent number for reverting merges
- `--strategy=<strategy>`: Merge strategy
- `-s, --signoff`: Add Signed-off-by line
- `--gpg-sign[=<key-id>]`: GPG-sign commit
- `--continue`: Continue revert after resolving conflicts
- `--abort`: Cancel revert operation
- `--quit`: Conclude revert operation

**Examples:**
```bash
# Revert a single commit
git revert 5e23f12

# Revert multiple commits
git revert 5e23f12 6f78e95

# Revert a range of commits
git revert 5e23f12..8e41abc

# Revert without committing
git revert --no-commit 5e23f12

# Revert a merge commit
git revert -m 1 5e23f12

# Revert with signed commit
git revert -S 5e23f12

# Continue revert after resolving conflicts
git revert --continue

# Abort current revert
git revert --abort
```

### git reset

**Purpose:** Reset current HEAD to the specified state

**Syntax:**
```bash
git reset [options] [<commit>] [--] [<paths>...]
```

**Options:**
- `--soft`: Don't touch index or working tree
- `--mixed`: Reset index but not working tree (default)
- `--hard`: Reset index and working tree
- `--merge`: Reset index and update working tree files that differ
- `--keep`: Reset index but keep working tree files
- `-p, --patch`: Interactively select hunks
- `--no-recurse-submodules`: Don't recurse into submodules

**Examples:**
```bash
# Unstage all changes (reset index)
git reset

# Unstage specific file
git reset -- file.js

# Soft reset (move HEAD, keep changes staged)
git reset --soft HEAD~1

# Mixed reset (move HEAD, unstage changes)
git reset --mixed HEAD~1

# Hard reset (move HEAD, discard all changes)
git reset --hard HEAD~1

# Reset to specific commit
git reset --hard 5e23f12

# Interactive reset
git reset -p HEAD

# Reset a branch to match remote
git reset --hard origin/main
```

## Configuration

### git config

**Purpose:** Get and set repository or global options

**Syntax:**
```bash
git config [options] [name] [value]
```

**Options:**
- `--system`: Use system config file
- `--global`: Use global config file
- `--local`: Use repository config file (default)
- `--worktree`: Use per-worktree config file
- `-e, --edit`: Open config file in editor
- `--get`: Get value for name
- `--get-all`: Get all values for a multi-valued name
- `--add`: Add a new value
- `--unset`: Remove a value
- `--unset-all`: Remove all matching values
- `--rename-section`: Rename section
- `--list, -l`: List all variables and values

**Examples:**
```bash
# Set global user information
git config --global user.name "John Doe"
git config --global user.email "john.doe@example.com"

# Set local (repository-specific) information
git config --local user.email "work@example.com"

# Set default editor
git config --global core.editor vim

# Set default branch name
git config --global init.defaultBranch main

# Configure line endings
git config --global core.autocrlf input  # For macOS/Linux
git config --global core.autocrlf true   # For Windows

# Set color UI
git config --global color.ui auto

# Set alias
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.st status
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Get a value
git config user.name

# List all configurations
git config --list

# Edit global config in editor
git config --global --edit

# Unset a value
git config --unset core.autocrlf
```

## Git Workflows

### Basic Workflow

```bash
# Start a new feature
git checkout -b feature-x

# Edit files
echo "New code" >> file.txt

# Stage and commit
git add file.txt
git commit -m "Add new feature X"

# Push to remote
git push -u origin feature-x

# Switch back to main branch
git checkout main

# Get latest changes
git pull

# Merge the feature
git merge feature-x

# Push the merge
git push
```

### Fork and Pull Request Workflow

```bash
# Clone the forked repository
git clone https://github.com/yourusername/project.git

# Add upstream remote
git remote add upstream https://github.com/original/project.git

# Create feature branch
git checkout -b new-feature

# Make changes and commit
git add .
git commit -m "Add new feature"

# Get latest from upstream
git fetch upstream
git rebase upstream/main

# Push to your fork
git push -u origin new-feature

# Now create a pull request on GitHub
```

### GitFlow Workflow

```bash
# Initialize GitFlow
git flow init

# Start a feature
git flow feature start new-feature

# Finish a feature
git flow feature finish new-feature

# Start a release
git flow release start 1.0.0

# Finish a release
git flow release finish 1.0.0

# Start a hotfix
git flow hotfix start bugfix

# Finish a hotfix
git flow hotfix finish bugfix
```

### Useful Tips

- Always pull before pushing to avoid conflicts
- Use meaningful commit messages
- Regularly fetch from upstream when working on forks
- Use branches for features, fixes, and experiments
- Clean up local branches after they're merged
- Set up aliases for commonly used commands
- Configure global `.gitignore` for temporary files

## Conclusion

This comprehensive guide covers most Git commands and their various options. Git is a powerful tool with many capabilities, and mastering these commands will help you manage your source code efficiently and effectively.

Remember that Git documentation is always available via:

```bash
git help <command>
git <command> --help
man git-<command>
```

For the latest information, refer to the official Git documentation at https://git-scm.com/docs.

Current Date: 2025-03-07  
User: dev-zuhaib
