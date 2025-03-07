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
