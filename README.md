# dailygitcommands
git command cheatsheet for my daily use

- `git clone <url>`: clones repo
- `git fetch --prune`: update remote tracking refs and remove deleted remote branches
‎- `git switch <branch name>`: switch branch and also create local branch and connect it to origin branch if available
‎- `git pull`: pull latest changes from origin
‎- `git push`: push local commits to origin
‎- `git add .`: add changes to staging
‎- `git commit -m "message"`: commit staged changes
‎- `git reset --hard`: reset to last local commit
‎- `git reset --hard @{u}`: reset to last remote commit
‎- `git reset --hard <commit hash>`: reset to specific commit
‎- `git branch`: see list of local branches
‎- `git branch -a`: see list of all branches
‎- `git branch -D <branch>`: delete local branch
‎- `git clean -fd`: remove untracked files and directories
‎- `git clean -fdx`: same as above but also deletes gitignored files (be careful)
‎- `git status`: see current branch info
‎- `git log --oneline`: see list of commits
‎- `git diff`: compares current working dir vs staging
‎- `git diff --staged`: compares staging to last commit
‎- `git diff <older commit hash> <newer commit hash>`: compares two commits
‎- `git config --global credential.helper 'cache --timeout=3600'`: cache username and password in RAM for 3600 seconds
‎- `git config --global --unset credential.helper`: revert the above command
‎- `git credential-cache exit`: force clear cached username and password
- `git config --global user.name "<Author Name>"`: set the author name for commit metadata
- `git config --global user.email "<author@email.com>"`: set the author email for commit metadata
