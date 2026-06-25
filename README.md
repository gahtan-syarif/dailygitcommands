# Daily Git Commands
Cheatsheet for the git commands that i personally use. Feel free to use it as reference.

## Setup & Configuration
- `git config --global user.name "<Author Name>"` — set author name for commit metadata
- `git config --global user.email "<author@email.com>"` — set author email for commit metadata
- `git config --global fetch.prune true` — automatically prune stale remote tracking refs when doing a git fetch or git pull
- `git config --global credential.helper 'cache --timeout=<insert seconds here>'` — cache credentials in RAM for specified number of seconds
- `git config --global --unset <configuration name>` — unset a configuration (revert the above commands)
- `git credential-cache exit` — force clear cached credentials

## Getting & Syncing
- `git clone <url>` — clone a repo
- `git fetch` — update remote tracking refs
- `git pull` — fetch and merge latest changes from remote branch
- `git merge --abort` — aborts merge if there's a merge conflict
- `git remote prune origin` — prune stale remote tracking refs (not needed if fetch.prune config is set to true)

## Branching
- `git switch <branch name>` — switch branch; auto-creates local branch tracking remote branch if available
- `git branch -D <branch name>` — force delete a local branch
- `git push origin --delete <branch name>` — delete a remote branch
- `git switch -c <branch name> && git push -u origin HEAD` — create both a local and remote branch from current branch

## Staging, Committing & Pushing
- `git add .` — stage all changes
- `git commit -m "<insert message here>"` — commit staged changes locally
- `git commit --amend -m "<insert message here>"` — recreate the last commit with modifications
- `git push` — push local commits to remote branch

## Undoing
- `git restore .` — reset to last staged state
- `git reset --hard` — reset to last local commit
- `git reset --hard @{u}` — reset to last remote commit
- `git reset --hard <commit hash>` — reset to a specific commit
- `git revert <commit hash>` — create a new commit that undoes a previous specified commit
- `git revert --abort` — aborts revert if there's a conflict
- `git clean -fd` — remove untracked files and directories
- `git clean -fdx` — same as above but also removes gitignored files (be careful)

## Inspecting
- `git status` — show current branch and working tree status
- `git branch -vva` — list both local and remote branches and their info
- `git log --oneline --graph --decorate --all` — show full commit history
- `git reflog` — find lost commits for disaster recovery (e.g. after an accidental git reset)
- `git show <commit hash>` — show commit info
- `git diff` — compare working directory to staging
- `git diff --staged` — compare staging to last commit
- `git diff <older commit hash> <newer commit hash>` — compare two commits
