# Daily Git Commands
Cheatsheet for the Git commands and configuration for my personal use. Feel free to use it as reference.

> [!NOTE]
> Throughout this cheatsheet, `<commit>` can be any reference that identifies a specific commit, such as a commit hash, a branch name (this points to the last commit of that branch), a tag, a symbolic reference (e.g. `HEAD`), or revision expression (e.g. `HEAD~3`).

## Table of Contents

- [Configuration](#configuration) — Configure settings
- [Initialization](#initialization) — Creating repos
- [Cloning](#cloning) — Clone an existing repo
- [Remotes](#remotes) — Configuring remote repos
- [Syncing](#syncing) — Fetching changes from upstream
- [Pushing](#pushing) — Uploading changes to upstream
- [Status](#status) — Checking the current repo state
- [Staging](#staging) — Preparing for a commit
- [Committing](#committing) — Committing changes
- [Branching](#branching) — Working with branches
- [Tagging](#tagging) — Working with tags
- [Integration](#integration) — Combining changes
- [Undoing](#undoing) — Undoing changes
- [Conflicts](#conflicts) — Resolving conflicts
- [History](#history) — Exploring commit history
- [Comparing](#comparing) — Inspecting differences
- [Notes](#notes) — Annotating commits
- [Stashing](#stashing) — Saving work for later
- [Patches](#patches) — Create and apply patches
- [Debugging](#debugging) — Finding buggy commits
- [Worktrees](#worktrees) — Multiple working directories
- [Subtrees](#subtrees) — Vendoring external repos
- [Submodules](#submodules) — Linking external repos
- [LFS](#lfs) — Managing large binary files
- [Sparse](#sparse) — Working with large repos selectively
- [Maintenance](#maintenance) — Optimizing repo performance
- [Diagnostics](#diagnostics) — Check repo health
- [Exporting](#exporting) — Export repo contents
- [Documentation](#documentation) — Manuals and documentation


## Configuration
- `git config --global user.name "<author-name>"` — set author name for commit metadata
- `git config --global user.email "<author-email>"` — set author email for commit metadata
- `git config --global credential.helper 'cache --timeout=<seconds>'` — cache credentials (e.g. GitHub username and PAT) in RAM for the specified number of seconds to avoid repeatedly typing credentials (not supported on Windows)
- `git config --global init.defaultBranch main` — use `main` (instead of `master`) as the default branch name for new repos to match the default branch name used by modern Git hosting providers
- `git config --global merge.conflictStyle zdiff3` — use the better `zdiff3` conflict style instead of the default `merge` style
- `git config --global core.editor "<editor-command>"` — set Git's default text editor (e.g. `vim`, `nano`, `micro`, `notepad`)
- `git config --global core.fsmonitor true` — enable file system monitor to speed up working tree scans
- `git config --global alias.<name> "<command>"` — create a git alias
- `git config --global --unset <configuration-name>` — unset a configuration
- `git config --list --show-origin` — see list of active configurations

## Initialization
- `git init` — initialize a new local git repo in the current directory
- `git init --bare` — initialize a bare repo with no working tree in the current directory (used for hosting a Git server)

## Cloning
- `git clone <repo-url>` — clone a remote repo locally
- `git clone --filter=blob:none --sparse <repo-url>` — clone an extremely large repo by downloading and checking out files as needed (see the [Sparse](#sparse) section)
- `git clone --depth 1 <repo-url>` — clone only the latest commit, minimizing download size when commit history is not needed
- `git clone --mirror <repo-url>` — create a local mirror of a remote repo
- `git clone <file-path>` — clone a repository from a bundle file

## Remotes
- `git remote add origin <repo-url>` — link local repo to a remote repo for fetching, pulling, and pushing
- `git remote add <remote-name> <repo-url>` — link an additional remote repo, such as the original repo your fork was created from or someone else's fork
- `git remote add <remote-name> <file-path>` — add a bundle file as a read-only remote
- `git remote remove <remote-name>` — remove a remote
- `git remote rename <old-name> <new-name>` — rename a configured remote
- `git remote set-url <remote-name> <repo-url>` — change the URL of an existing remote
- `git remote -v` — list configured remotes and their URLs

## Syncing
- `git fetch --prune --all` — update all remote tracking branches and remove stale ones
- `git fetch <remote-name> <tag-name>` — fetch a specific tag from a remote
- `git fetch <remote-name> --tags` — fetch all tags from a remote
- `git fetch <remote-name> --prune --prune-tags` — fetch all tags from a remote and remove local ones that no longer exist upstream
- `git pull` — fetch latest commits from the configured remote branch and merge them into current local branch
- `git pull --rebase` — fetch latest commits from the configured remote branch and then rebase the current local branch

## Pushing
- `git push` — push commits from current local branch to the configured remote branch
- `git push --force` — force sync the configured remote branch to match the current local one
- `git push --mirror <remote-name>` — make a target repo match a local mirror exactly
- `git push -u origin HEAD` — create a remote branch from the current branch (or update it if it already exists) and set it as the upstream
- `git push origin <tag-name>` — push a local tag to remote
- `git push origin --tags` — push all local tags to remote
- `git push origin --delete <branch-name|tag-name>` — delete a remote branch or tag

## Status
- `git status` — show current branch and working tree status

## Staging
- `git add -A` — stage all changes
- `git add <path>` — stage changes in a specific file or directory
- `git restore --staged <path>` — unstage changes in a specific file or directory

## Committing
- `git commit` — commit staged changes locally
- `git commit --amend` — replace the latest commit with a new commit
- `git commit --amend --no-edit` — replace the latest commit with a new commit while keeping the existing commit message

## Branching
- `git switch <branch-name>` — switch to an existing branch (also auto-creates a local branch that tracks a matching remote branch if available)
- `git switch --detach <commit>` — switch to a specific commit (in a detached HEAD state)
- `git switch -c <branch-name>` — create a local branch from the current commit and switch to it
- `git branch <branch-name>` — create a local branch from the current commit without switching
- `git branch -m <new-name>` — rename the current local branch
- `git branch -D <branch-name>` — force delete a local branch
- `git branch -u <remote-name>/<branch-name>` — set the current local branch to track an existing remote branch
- `git branch --unset-upstream` — unlink the remote branch from the current local branch
- `git branch -vva` — list both local and remote branches and their info

## Tagging
- `git tag <tag-name> <commit>` — create a local lightweight tag for a specific commit
- `git tag -a <tag-name> <commit>` — create a local annotated tag for a specific commit
- `git tag -d <tag-name>` — delete a local tag
- `git tag -n` — list all local tags

## Integration
- `git merge <commit>` — merge the changes up to a specified commit into the current branch
- `git merge --no-ff <commit>` — create a merge commit even if a fast-forward merge is possible
- `git merge --ff-only <commit>` — merge only if it can be performed as a fast-forward
- `git merge --squash <commit>` — merge the changes up to a specified commit into the current branch as a single staged change (does not create a commit)
- `git rebase <commit>` — rebase the current branch onto the specified commit
- `git rebase -i <commit>` — interactively rebase the current branch onto the specified commit (usually used for rewriting commit history)
- `git cherry-pick <commit>...` — copy one or more commits onto the current branch

## Undoing
- `git restore <path>` — discard unstaged changes in a specific file or directory
- `git restore -s <commit> <path>` — restore a file or directory from a specific commit
- `git reset --soft HEAD~<number>` — uncommit the last specified number of commits while keeping the working directory unchanged
- `git reset --hard` — reset to last local commit
- `git reset --hard @{u}` — reset to last remote commit
- `git reset --hard <commit>` — reset to a specific commit
- `git revert <commit>...` — create one or more new commits that undoes the specified commits
- `git revert -m 1 <commit>` — create a new commit that undoes a merge commit (reverts a merge)
- `git clean -fd` — remove untracked files and directories
- `git clean -fdx` — same as above but also removes gitignored files

## Conflicts
- `git <merge|rebase|cherry-pick|revert|am> --abort` — aborts the operation if there's a conflict
- `git <merge|rebase|cherry-pick|revert|am> --continue` — continues the operation after resolving conflict
- `git <rebase|cherry-pick|revert|am> --skip` — skips the current conflicting commit and move to the next one

## History
- `git log --oneline --graph --all` — show full commit history
- `git log --oneline --graph <commit>` — show commit history up to a specified commit
- `git log --oneline --graph <commitA>..<commitB>` — show commits reachable from `<commitB>` but not from `<commitA>` (e.g. finding commits unique to a branch)
- `git log --oneline --follow -- <file-path>` — show commit history for a file in the current branch
- `git reflog` — find lost commits for disaster recovery (e.g. after an accidental hard reset)
- `git shortlog <commitA>..<commitB>` — list the contributions by each author in a specific commit range
- `git shortlog -sn <commitA>..<commitB>` — summarize the number of commits by each author in a specific commit range
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
- `git range-diff <commitA>..<commitB> <commitC>..<commitD>` — compare two sequences of commits, matching corresponding commits and showing how each patch changed (e.g. for comparing two slightly different versions of a feature branch)

> [!NOTE]
> Append `--stat` to `git diff` to show a per-file summary with total insertions and deletions instead of the full patch.

## Notes
- `git notes add <commit>` — write and attach a note to a commit
- `git notes show <commit>` — show the note attached to a commit
- `git notes edit <commit>` — edit the note attached to a commit
- `git notes remove <commit>` — remove the note attached to a commit
- `git notes prune` — remove notes that no longer reference existing commits
- `git notes list` — list all notes and the commits they are attached to

## Stashing
- `git stash push -u` — move staged and unstaged changes to a stash (including untracked files)
- `git stash pop` — restore and remove the most recent stash
- `git stash pop stash@{<index-number>}` — restore and remove a specific stash
- `git stash apply` — restore the most recent stash without removing it
- `git stash apply stash@{<index-number>}` — restore a specific stash without removing it
- `git stash drop` — delete the most recent stash
- `git stash drop stash@{<index-number>}` — delete a specific stash
- `git stash clear` — delete all stashes
- `git stash list` — list all stashes

## Patches
- `git format-patch -o <dir-path> -1 <commit>` — create a patch file for a specific commit
- `git format-patch -o <dir-path> <commitA>..<commitB>` — create patches for all commits reachable by `<commitB>` but not from `<commitA>`
- `git apply <file-path>...` — apply the changes from one or more patch files to the working tree without creating a commit
- `git am -3 <file-path>...` — apply and commit the changes from one or more patch files, preserving commit metadata

## Debugging
- `git bisect start` — start a binary search to find the commit that introduced a bug
- `git bisect good <commit>` — mark a known good commit
- `git bisect bad <commit>` — mark a known bad commit
- `git bisect run <command>` — automate the search by running a test script
- `git bisect reset` — exit bisect mode and return to the original branch

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
- `git submodule deinit --all` — unregister all submodules from the working tree and remove their working directory
- `git submodule status --recursive` — show the current commit and status of each submodule
- `git mv <old-path> <new-path>` — move a submodule to a new path
- `git rm <path>` — remove a submodule

## LFS
- `git lfs install` — initialize Git LFS for the current user (only done once per user)
- `git lfs track "<pattern>"` — track matching files with Git LFS
- `git lfs untrack "<pattern>"` — stop tracking matching files with Git LFS
- `git lfs prune` — remove locally cached LFS objects that are no longer needed, to free up disk space
- `git lfs ls-files` — list files tracked by Git LFS
- `git lfs lock <file-path>` — lock a file to prevent others from pushing changes to it
- `git lfs unlock <file-path>` — unlock a locked file
- `git lfs unlock --force <file-path>` — force-unlock a file locked by someone else (typically requires admin permissions)
- `git lfs locks` — list active locks in the repository

> [!NOTE]
> Git LFS is typically not included with Git on Linux and MacOS and must be installed separately before these commands can be used.

## Sparse
- `git sparse-checkout set <dir-path>...` — populate only the specified directories
- `git sparse-checkout add <dir-path>...` — add more directories to the sparse checkout
- `git sparse-checkout reapply` — reapply the sparse checkout rules to the working tree
- `git sparse-checkout disable` — restore the full working tree
- `git sparse-checkout list` — list directories included in the sparse checkout

### Maintenance
- `git maintenance start` — enable scheduled background repository maintenance
- `git maintenance stop` — disable scheduled background repository maintenance
- `git maintenance register` — register the current repository for scheduled maintenance
- `git maintenance unregister` — unregister the current repository from scheduled maintenance
- `git maintenance run` — run the default maintenance tasks immediately
- `git maintenance run --auto` — run maintenance only if Git determines it is needed

## Diagnostics
- `git fsck` — check repo integrity and detect corrupted, missing, or unreachable objects

## Exporting
- `git archive --format=<format> -o <file-path> <commit>` — create an archive (`zip`, `tar`, `tar.gz`, etc.) containing a snapshot of the repo contents at a specific commit (e.g. for distributing versioned releases)
- `git bundle create <file-path> --all` — create a bundle file containing the entire repo and its history (e.g. for creating repo backups)
- `git bundle create <file-path> <branch-name>...` — create a bundle file containing the specified branches and their history
- `git bundle create <file-path> <commit>..<branch-name>` — create a bundle file containing the specified branch and its history while excluding commits reachable from `<commit>` (e.g. for incremental backups)

## Documentation
- `git help -a` — list all available commands and docs as well as their description
- `git help <command|doc>` — show the manual page for a specific command or documentation
