# Daily Git Commands
Cheatsheet for the Git commands and configuration that i personally use. Feel free to use it as reference.

> [!NOTE]
> Throughout this cheatsheet, `<commit>` can be any reference that identifies a specific commit, such as a commit hash, a branch name (this points to the last commit of that branch), a tag, a symbolic reference (e.g. `HEAD`), or revision expression (e.g. `HEAD~3`).

## Table of Contents

- [Configuration](#configuration) — Configure settings
- [Initialization](#initialization) — Creating repos and remotes
- [Syncing](#syncing) — Synchronizing with remote repos
- [Status](#status) — Checking the current repo state
- [Staging](#staging) — Preparing for a commit
- [Committing](#committing) — Committing changes
- [Branching](#branching) — Working with branches
- [Tagging](#tagging) — Working with tags
- [Integration](#integration) — Combining branches
- [Undoing](#undoing) — Undoing changes
- [Conflicts](#conflicts) — Resolving conflicts
- [History](#history) — Exploring commit history
- [Comparing](#comparing) — Inspecting differences
- [Stashing](#stashing) — Saving work for later
- [Debugging](#debugging) — Finding buggy commits
- [Mirroring](#mirroring) — Mirroring repos
- [Worktrees](#worktrees) — Multiple working directories
- [Subtrees](#subtrees) — Vendoring external repos
- [Submodules](#submodules) — Linking external repos
- [LFS](#lfs) — Managing large binary files
- [Documentation](#documentation) — Manuals and documentation


## Configuration
- `git config --global user.name "<author-name>"` — set author name for commit metadata
- `git config --global user.email "<author-email>"` — set author email for commit metadata
- `git config --global credential.helper 'cache --timeout=<seconds>'` — cache credentials (e.g. GitHub username and PAT) in RAM for the specified number of seconds to avoid repeatedly typing credentials (not supported on Windows)
- `git config --global init.defaultBranch main` — use `main` (instead of `master`) as the default branch name for new repos to match the default branch name used by modern Git hosting providers
- `git config --global merge.conflictStyle zdiff3` — use the better `zdiff3` conflict style instead of the default `merge` style
- `git config --global alias.<name> "<command>"` — create a git alias
- `git config --global --unset <configuration-name>` — unset a configuration
- `git config --list --show-origin` — see list of active configurations

## Initialization
- `git clone <repo-url>` — clone a remote repo locally
- `git init` — initialize a new local git repo in the current directory 
- `git remote add origin <repo-url>` — link local repo to a remote repo for fetching, pulling, and pushing
- `git remote add upstream <repo-url>` — link local repo to the upstream repo of your fork (in cases where `origin` is a fork of someone else's repo)
- `git remote remove <remote-name>` — remove a remote
- `git remote -v` — list configured remotes and their URLs

## Syncing
- `git fetch --prune --all` — update all remote tracking refs and remove stale remote-tracking branches
- `git pull` — fetch latest commits from remote branch and merge them into current local branch
- `git pull --rebase` — fetch latest commits from remote branch and then rebase the current local branch
- `git push` — push commits from current local branch to remote branch
- `git push --force` — force sync a remote branch to match the current local one

## Status
- `git status` — show current branch and working tree status

## Staging
- `git add <path>` — stage a specific file or directory
- `git add .` — stage all changes in the current directory 
- `git restore --staged <path>` — unstage a specific file or directory
- `git restore --staged .` — unstage all changes in the current directory 

## Committing
- `git commit -m "<message>"` — commit staged changes locally
- `git commit --amend -m "<message>"` — replace the latest commit with a new commit
- `git commit --amend --no-edit` — replace the latest commit with a new commit while keeping the existing commit message

## Branching
- `git switch <branch-name>` — switch to an existing branch (also auto-creates a local branch that tracks a matching remote branch if available)
- `git switch --detach <commit>` — switch to a specific commit (in a detached HEAD state)
- `git switch -c <branch-name>` — create a local branch from the current branch or commit and switch to it
- `git branch <branch-name>` — create a local branch from the current branch or commit without switching
- `git branch -D <branch-name>` — force delete a local branch
- `git branch -u <remote-name>/<branch-name>` — set the current local branch to track an existing remote branch
- `git branch --unset-upstream` — unlink the remote branch from the current local branch
- `git branch -vva` — list both local and remote branches and their info
- `git push -u origin HEAD` — create a remote branch from the current branch (or update it if it already exists) and set it as the upstream
- `git push origin --delete <branch-name>` — delete a remote branch

## Tagging
- `git tag -a <tag-name> -m "<tag-message>" <commit>` — create a local tag for a specific commit
- `git tag -d <tag-name>` — delete a local tag
- `git tag -n` — list all local tags
- `git push origin <tag-name>` — push a local tag to remote
- `git push origin --tags` — push all local tags to remote
- `git push origin --delete <tag-name>` — delete a remote tag

## Integration
- `git merge <branch-name>` — merge another branch into the current branch
- `git merge --squash <branch-name>` — merge another branch into the current branch as a single staged change (does not create a commit)
- `git rebase <branch-name>` — rebases current branch on top of another branch
- `git cherry-pick <commit>` — copy a specific commit from a diverged branch onto the current branch

## Undoing
- `git restore <path>` — discard unstaged changes in a specific file or directory
- `git restore .` — discard unstaged changes in the current directory
- `git reset --soft HEAD~<number>` — uncommit the last specified number of commits while keeping the working directory unchanged
- `git reset --hard` — reset to last local commit
- `git reset --hard @{u}` — reset to last remote commit
- `git reset --hard <commit>` — reset to a specific commit
- `git revert <commit>` — create a new commit that undoes a specified commit
- `git revert -m 1 <commit>` — same as above but specifically for merge commits (reverts a merge)
- `git clean -fd` — remove untracked files and directories
- `git clean -fdx` — same as above but also removes gitignored files (be careful)

## Conflicts
- `git <merge|rebase|cherry-pick|revert> --abort` — aborts the operation if there's a conflict
- `git <merge|rebase|cherry-pick|revert> --continue` — continues the operation after resolving conflict
- `git <rebase|cherry-pick|revert> --skip` — skips the current conflicting commit and move to the next one

## History
- `git log --oneline --graph --all` — show full commit history
- `git log --oneline --graph <commit>` — show commit history up to a specified commit
- `git log --oneline --graph <commitA>..<commitB>` — show commits reachable from `<commitB>` but not from `<commitA>` (e.g. finding commits unique to a branch)
- `git log --oneline --follow -- <file-path>` — show commit history for a file in the current branch
- `git reflog` — find lost commits for disaster recovery (e.g. after an accidental hard reset)
- `git show <commit>` — show commit info
- `git blame -w -M -C <commit> -- <file-path>` — show who was last responsible for each line in a file as of a specific commit
- `git describe --contains <commit>` — show the earliest tag that contains a commit (e.g. to find which version release a commit is part of)

> [!NOTE]
> `git log` also supports filters such as `--author="<name>"`, `--since="<date>"`, `--until="<date>"`, and `--grep="<pattern>"`, which can be combined as needed.

## Comparing
- `git diff` — compare working directory to staging
- `git diff <commit>` — compare working directory to a specific commit
- `git diff --staged` — compare staging to last commit
- `git diff <base-commit> <target-commit>` — compare two commits
- `git diff <base-commit>...<target-commit>` — compare the target commit to the merge base (common ancestor) of the two commits

## Stashing
- `git stash push -u` — move staged and unstaged changes to a stash (including untracked files)
- `git stash pop` — restore and remove the most recent stash
- `git stash pop stash@{<index-number>}` — restore and remove a specific stash
- `git stash apply` — restore the most recent stash without removing it
- `git stash apply stash@{<index-number>}` — restore a specific stash without removing it
- `git stash drop` — delete the most recent stash
- `git stash drop stash@{<index-number>}` — delete a specific stash
- `git stash list` — list all stashes

## Debugging
- `git bisect start` — start a binary search to find the commit that introduced a bug
- `git bisect good <commit>` — mark a known good commit
- `git bisect bad <commit>` — mark a known bad commit
- `git bisect run <command>` — automate the search by running a test script
- `git bisect reset` — exit bisect mode and return to the original branch

## Mirroring
- `git clone --mirror <source-repo-url>` — create a local mirror of the original repo
- `git push --mirror <target-repo-url>` — make the target repo match the local mirror exactly

## Worktrees
- `git worktree add <path> <branch-name>` — check out an existing branch in a separate directory (creates a new working tree)
- `git worktree remove <path>` — remove a working tree
- `git worktree list` — list working trees

## Subtrees
- `git subtree add --squash --prefix=<path> <repo-url> <commit>` — add a repo as a subtree (e.g. a third party library)
- `git subtree pull --squash --prefix=<path> <repo-url> <commit>` — sync the subtree to a specific commit from its upstream repo

## Submodules
- `git submodule add <repo-url> <path>` — add a repo as a submodule
- `git submodule sync --recursive` — refresh local submodule remote URLs
- `git submodule update --init --recursive` — initialize missing submodules and sync all submodules to the commits recorded in the superproject
- `git submodule status --recursive` — show the current commit and status of each submodule

## LFS
- `git lfs install` — initialize Git LFS for the current user (only done once per user)
- `git lfs track "<pattern>"` — track matching files with Git LFS
- `git lfs untrack "<pattern>"` — stop tracking matching files with Git LFS
- `git lfs prune` — remove locally cached LFS objects that are no longer needed, to free up disk space
- `git lfs ls-files` — list files tracked by Git LFS

> [!NOTE]
> Git LFS is typically not included with Git on Linux and MacOS and must be installed separately before these commands can be used.

## Documentation
- `git help <command|doc>` — show the manual page for a specific command or documentation
- `git help -a` — list all available commands and docs as well as their description
