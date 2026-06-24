# Daily Git Commands

## Initial Setup
- `git config --global user.name "<Author Name>"` — set author name for commit metadata
- `git config --global user.email "<author@email.com>"` — set author email for commit metadata
- `git config --global fetch.prune true` — automatically prune stale remote tracking refs when doing a git fetch or git pull

## Credentials
- `git config --global credential.helper 'cache --timeout=3600'` — cache credentials in RAM for 3600 seconds
- `git config --global --unset credential.helper` — clear credential helper config (revert the above command)
- `git credential-cache exit` — force clear cached credentials

## Getting & Syncing
- `git clone <url>` — clone a repo
- `git fetch` — update remote tracking refs
- `git pull` — fetch and merge latest changes from origin
- `git push` — push local commits to origin

## Branching
- `git switch <branch name>` — switch branch; auto-creates local branch tracking origin if available
- `git branch -vv` — list local branches and their latest commits
- `git branch -vva` — list both local and remote branches and their latest commits
- `git branch -D <branch name>` — force delete a local branch
- `git push origin --delete <branch name>` — delete a remote branch
- `git switch -c <branch name> && git push -u origin HEAD` — create both a local and remote branch
- `git remote prune origin` — prune stale remote tracking refs

## Staging & Committing
- `git add .` — stage all changes
- `git commit -m "<insert message here>"` — commit staged changes

## Undoing
- `git reset --hard` — reset to last local commit
- `git reset --hard @{u}` — reset to last remote commit
- `git reset --hard <commit hash>` — reset to a specific commit
- `git clean -fd` — remove untracked files and directories
- `git clean -fdx` — same as above but also removes gitignored files (be careful)

## Inspecting
- `git status` — show current branch and working tree status
- `git log --oneline` — show commit history
- `git diff` — compare working directory to staging
- `git diff --staged` — compare staging to last commit
- `git diff <older commit hash> <newer commit hash>` — compare two commits

