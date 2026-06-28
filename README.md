# Daily Git Commands
Cheatsheet for the git commands and configuration that i personally use. Feel free to use it as reference.

## Setup & Configuration
- `git config --global user.name "<author-name>"` — set author name for commit metadata
- `git config --global user.email "<author-email>"` — set author email for commit metadata
- `git config --global credential.helper 'cache --timeout=<seconds>'` — cache credentials (e.g. GitHub username and PAT) in RAM for the specified number of seconds to avoid repeatedly typing credentials (not supported on Windows)
- `git config --global --unset <configuration-name>` — unset a configuration (revert the above commands)

## Repository Initialization
- `git init` — initialize a new local git repo in the current directory 
- `git remote add origin <repo-url>` — link local repo to a remote repo for fetching, pulling, and pushing
- `git remote add upstream <repo-url>` — link local repo to the upstream repo of your fork (in cases where `origin` is a fork of someone else's repo)
- `git remote remove <remote-name>` — remove a remote (e.g. when migrating to a different git hosting provider)
- `git clone <repo-url>` — clone a remote repo locally

## Syncing
- `git fetch --prune --all` — update all remote tracking refs and remove stale remote-tracking branches
- `git pull` — fetch latest commits from remote branch and merge them into current local branch
- `git pull --rebase` — fetch latest commits from remote branch and then rebase the current local branch
- `git push` — push commits from current local branch to remote branch
- `git push --force` — force sync a remote branch to match the current local one


## Branching
- `git switch <branch-name>` — switch to an existing branch (also auto-creates a local branch that tracks a matching remote branch if available)
- `git switch --detach <commit>` — switch to a specific commit (in a detached HEAD state)
- `git branch <branch-name>` — create a local branch from the current branch or commit
- `git branch -D <branch-name>` — force delete a local branch
- `git branch --set-upstream-to=<remote-name>/<branch-name>` — set the current local branch to track an existing remote branch
- `git branch --unset-upstream` — unlink the remote branch from the current local branch
- `git push -u origin HEAD` — create a remote branch from the current branch (or update it if it already exists) and set it as the upstream
- `git push origin --delete <branch-name>` — delete a remote branch
- `git worktree add <path> <branch-name>` — check out an existing branch in a separate directory (creates a new working tree)
- `git worktree remove <path>` — remove a working tree

## Tagging
- `git tag <tag-name> <commit>` — create a lightweight tag for a specific commit
- `git tag -a <tag-name> -m "<tag-message>" <commit>` — create an annotated tag for a specific commit
- `git tag -d <tag-name>` — delete a local tag
- `git push origin <tag-name>` — push a local tag to remote
- `git push origin --tags` — push all local tags to remote
- `git push origin --delete <tag-name>` — delete a remote tag

## Combining Branches
- `git merge <branch-name>` — merge another branch into the current branch
- `git merge --squash <branch-name>` — merge another branch into the current branch as a single staged change (does not create a commit)
- `git rebase <branch-name>` — rebases current branch on top of another branch
- `git cherry-pick <commit>` — copy a specific commit from a diverged branch onto the current branch

## Staging & Committing
- `git add .` — stage all changes
- `git commit -m "<message>"` — commit staged changes locally

## Stashing
- `git stash` — move staged and unstaged changes to a stash (untracked files are excluded)
- `git stash pop` — restore and remove the most recent stash
- `git stash pop stash@{<index-number>}` — restore and remove a specific stash
- `git stash drop stash@{<index>}` — delete a specific stash
- `git stash clear` — delete all stashes

## Undoing
- `git restore .` — discard unstaged changes in the working directory
- `git reset --soft HEAD~<number>` — uncommit the last specified number of commits while keeping the working directory unchanged
- `git reset --hard` — reset to last local commit
- `git reset --hard @{u}` — reset to last remote commit
- `git reset --hard <commit>` — reset to a specific commit
- `git revert <commit>` — create a new commit that undoes a specified commit
- `git revert -m 1 <commit>` — same as above but specifically for merge commits
- `git clean -fd` — remove untracked files and directories
- `git clean -fdx` — same as above but also removes gitignored files (be careful)

## Conflict Resolution
- `git <merge|rebase|cherry-pick|revert> --abort` — aborts the operation if there's a conflict
- `git <merge|rebase|cherry-pick|revert> --continue` — continues the operation after resolving conflict
- `git <rebase|cherry-pick> --skip` — skips the current conflicting commit and move to the next one

## Debugging
- `git bisect start` — start a binary search to find the commit that introduced a bug
- `git bisect good <commit>` — mark a known good commit
- `git bisect bad <commit>` — mark a known bad commit
- `git bisect run <command>` — automate the search by running a test script
- `git bisect reset` — exit bisect mode and return to the original branch

## Repository Mirroring
- `git clone --mirror <source-repo-url>` — create a local mirror of the original repo
- `git fetch --prune --all && git push --mirror <target-repo-url>` — update the local mirror and make the target repo match it exactly

## Inspecting
- `git status` — show current branch and working tree status
- `git branch -vva` — list both local and remote branches and their info
- `git tag -n` — list all local tags
- `git stash list` — list all stashes
- `git worktree list` — list working trees
- `git remote -v` — list configured remotes and their URLs
- `git log --oneline --graph --decorate --all` — show full commit history
- `git log --oneline  --follow -- <file-path>` — show commit history for a file in the current branch
- `git reflog` — find lost commits for disaster recovery (e.g. after an accidental hard reset)
- `git show <commit>` — show commit info
- `git diff` — compare working directory to staging
- `git diff <commit>` — compare working directory to a specific commit
- `git diff --staged` — compare staging to last commit
- `git diff <base-commit> <target-commit>` — compare two commits
- `git blame -w -M -C <commit> -- <file-path>` — show who was last responsible for each line in a file as of a specific commit
- `git config --list --show-origin` — see list of active configurations
- `git help <git-command>` — show manual for a specific git command

Note: `<commit>` here can be anything that identifies a specific commit, whether it be a commit hash/ID, a branch name (this points to the last commit of that branch), a tag, a symbolic reference (e.g. `HEAD`), or a revision expression that resolves to a single commit (e.g. `HEAD~3`).
