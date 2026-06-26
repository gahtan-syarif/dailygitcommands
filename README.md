# Daily Git Commands
Cheatsheet for the git commands that i personally use. Feel free to use it as reference.

## Setup & Configuration
- `git config --global user.name "<author-name>"` — set author name for commit metadata
- `git config --global user.email "<author-email>"` — set author email for commit metadata
- `git config --global fetch.prune true` — automatically prune stale remote tracking refs when doing a git fetch or git pull (equivalent to always using git fetch --prune)
- `git config --global credential.helper 'cache --timeout=<seconds>'` — cache credentials in RAM for specified number of seconds
- `git config --global --unset <configuration-name>` — unset a configuration (revert the above commands)
- `git credential-cache exit` — force clear cached credentials

## Repo Initialization
- `git init` — initialize a new local git repo
- `git remote add origin <repo-url>` — link local repo to a remote repo
- `git clone <repo-url>` — clone a remote repo locally

## Syncing
- `git fetch` — update remote tracking refs
- `git pull` — fetch and merge commits from remote branch into current local branch
- `git push` — push commits from current local branch to remote branch
- `git push --force` — force sync a remote branch to match the current local one


## Branching
- `git switch <branch-name>` — switch branch; auto-creates local branch tracking remote branch if available
- `git switch -c <branch-name>` — create a local branch from the current branch
- `git push -u origin HEAD` — create a remote branch from the current branch (or update it if it already exists) and set it as the upstream
- `git branch -D <branch-name>` — force delete a local branch
- `git push origin --delete <branch-name>` — delete a remote branch

## Merging & Rebasing
- `git merge <branch-name>` — merge another branch into the current branch
- `git merge --squash <branch-name>` — merge another branch into the current branch as a single staged change (does not create a commit)
- `git merge --abort` — aborts merge if there's a merge conflict
- `git rebase <branch-name>` — rebases current branch on top of another branch
- `git rebase --abort` — aborts rebase if there's a rebase conflict
- `git rebase --continue` — continues rebase after resolving conflict

## Staging & Committing
- `git add .` — stage all changes
- `git commit -m "<commit-message>"` — commit staged changes locally

## Undoing
- `git reset --soft HEAD~1` — uncommit the last commit while keeping the files unchanged
- `git restore .` — reset to last staged state
- `git reset --hard` — reset to last local commit
- `git reset --hard @{u}` — reset to last remote commit
- `git reset --hard <commit-hash>` — reset to a specific commit
- `git revert <commit-hash>` — create a new commit that undoes a specified commit
- `git revert -m 1 <commit-hash>` — same as above but specifically for merge commits
- `git revert --abort` — aborts revert if there's a conflict
- `git revert --continue` — continues revert after resolving conflict
- `git clean -fd` — remove untracked files and directories
- `git clean -fdx` — same as above but also removes gitignored files (be careful)

## Inspecting
- `git status` — show current branch and working tree status
- `git branch -vva` — list both local and remote branches and their info
- `git log --oneline --graph --decorate --all` — show full commit history
- `git reflog` — find lost commits for disaster recovery (e.g. after an accidental git reset)
- `git show <commit-hash>` — show commit info
- `git diff` — compare working directory to staging
- `git diff --staged` — compare staging to last commit
- `git diff <base-commit-hash> <target-commit-hash>` — compare two commits
- `git blame -w <commit-hash> -- <file-path>` — show who last modified each line of a file as of a specific commit
- `git config --list --show-origin` — see list of active configurations
