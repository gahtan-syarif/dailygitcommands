# Daily Git Commands
Cheatsheet for the git commands and configuration that i personally use. Feel free to use it as reference.

## Setup & Configuration
- `git config --global user.name "<author-name>"` — set author name for commit metadata
- `git config --global user.email "<author-email>"` — set author email for commit metadata
- `git config --global credential.helper 'cache --timeout=<seconds>'` — cache credentials (e.g. GitHub username and PAT) in RAM for the specified number of seconds to avoid repeatedly typing credentials (not supported on Windows)
- `git config --global --unset <configuration-name>` — unset a configuration (revert the above commands)

## Repository Initialization
- `git init` — initialize a new local git repo
- `git remote add origin <repo-url>` — link local repo to a remote repo
- `git remote add upstream <repo-url>` — link local repo to the upstream repo of your fork (in cases where `origin` is a fork of someone else's repo)
- `git clone <repo-url>` — clone a remote repo locally

## Syncing
- `git fetch --prune --all` — update all remote tracking refs and remove stale remote-tracking branches
- `git pull` — fetch latest commits from remote branch and merge them into current local branch
- `git pull --rebase` — fetch latest commits from remote branch and then rebase the current local branch
- `git push` — push commits from current local branch to remote branch
- `git push --force` — force sync a remote branch to match the current local one


## Branching
- `git switch <branch-name>` — switch branch; auto-creates local branch tracking remote branch if available
- `git switch -c <branch-name>` — create a local branch from the current branch
- `git push -u origin HEAD` — create a remote branch from the current branch (or update it if it already exists) and set it as the upstream
- `git branch --set-upstream-to=<remote-name>/<branch-name>` — set the current local branch to track an existing remote branch
- `git branch -D <branch-name>` — force delete a local branch
- `git push origin --delete <branch-name>` — delete a remote branch

## Combining Branches
- `git merge <branch-name>` — merge another branch into the current branch
- `git merge --squash <branch-name>` — merge another branch into the current branch as a single staged change (does not create a commit)
- `git merge --abort` — aborts merge if there's a merge conflict
- `git rebase <branch-name>` — rebases current branch on top of another branch
- `git rebase --abort` — aborts rebase if there's a rebase conflict
- `git rebase --continue` — continues rebase after resolving conflict
- `git cherry-pick <commit-id>` — copy a specific commit from a diverged branch onto the current branch
- `git cherry-pick --abort` — aborts cherry-pick if there's a conflict
- `git cherry-pick --continue` — continue after resolving cherry-pick conflicts

## Staging & Committing
- `git add .` — stage all changes
- `git commit -m "<commit-message>"` — commit staged changes locally

## Undoing
- `git reset` — unstages all currently staged changes while keeping the files unchanged
- `git reset --soft HEAD~<number>` — uncommit the last specified number of commits while keeping the files unchanged
- `git restore .` — reset to last staged state
- `git reset --hard` — reset to last local commit
- `git reset --hard @{u}` — reset to last remote commit
- `git reset --hard <commit-id>` — reset to a specific commit
- `git revert <commit-id>` — create a new commit that undoes a specified commit
- `git revert -m 1 <commit-id>` — same as above but specifically for merge commits
- `git revert --abort` — aborts revert if there's a conflict
- `git revert --continue` — continues revert after resolving conflict
- `git clean -fd` — remove untracked files and directories
- `git clean -fdx` — same as above but also removes gitignored files (be careful)

## Inspecting
- `git status` — show current branch and working tree status
- `git branch -vva` — list both local and remote branches and their info
- `git log --oneline --graph --decorate --all` — show full commit history
- `git log --oneline  --follow -- <file-path>` — show commit history for a file in the current branch
- `git reflog` — find lost commits for disaster recovery (e.g. after an accidental git reset)
- `git show <commit-id>` — show commit info
- `git diff` — compare working directory to staging
- `git diff <commit-id>` — compare working directory to a specific commit
- `git diff --staged` — compare staging to last commit
- `git diff <base-commit-id> <target-commit-id>` — compare two commits
- `git blame -w -M <commit-id> -- <file-path>` — show who last modified each line of a file as of a specific commit
- `git config --list --show-origin` — see list of active configurations
- `git help <git-command>` — show manual for a specific git command (e.g. git help rebase)
