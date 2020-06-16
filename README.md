# Really Useful GIT commands
A collection of GIT commands that I personally use because they're really useful. This is a work in progress, please feel free to Contribute.

## Contents
* **[Basic Add, Commit, Push](#basic-add-commit-push)**
* **[Basic Pull](#basic-pull)**
* **[Create new branch](#create-new-branch)**
* **[Merge new branch to master](#merge-new-branch-to-master)**
* **[Rebase master onto new branch](#rebase-master-onto-new-branch)**
* **[Merge vs Rebase](#merge-vs-rebase)**
* **[See all branches](#see-all-branches)**
* **[Delete new branch](#delete-new-branch)**
* **[Show list of files changed in a Commit](#show-list-of-files-changed-in-a-commit)**
* **[Show contents of a Commit](#show-contents-of-a-commit)**
* **[Revert a Commit](#revert-a-commit)**
* **[Revert a Commit from History](#revert-a-commit-from-history)**
* **[See a summary of changes between the Branch and the Origin](#see-a-summary-of-changes-between-the-branch-and-the-origin)**
* **[See a log of Incoming Changes before you do a git pull](#see-a-log-of-incoming-changes-before-you-do-a-git-pull)**
* **[See a log of Outgoing Changes before you do a git push](#see-a-log-of-outgoing-changes-before-you-do-a-git-push)**
* **[Undo the last git commit](#undo-the-last-git-commit)**
* **[Undo the last git commit without rebasing](#undo-the-last-git-commit-without-rebasing)**
* **[Remove git commited files or folders](#remove-git-commited-files-or-folders)**
* **[Tell git to remember your git login](#tell-git-to-remember-your-git-login)**
* **[Pretty Git Log](#pretty-git-log)**
* **[Stash Changes](#StashChanges)**
* **[Re-apply Stashed Changes and delete from Stash List](#re-apply-stashed-changes-and-delete-from-stash-list)**
* **[Re-apply Stashed Changes but do not delete from Stash List](#re-apply-stashed-changes-but-do-not-delete-from-stash-list)**
* **[View Stashed Changes](#view-stashed-changes)**
* **[Stash Changes and Pull Updates](#stash-changes-and-pull-updates)**
* **[Stash Changes and Merge a Branch](#stash-changes-and-merge-a-branch)**
* **[Push to all remote branches](#push-to-all-remote-branches)**
* **[Push a specific branch to all remotes](#push-a-specific-branch-to-all-remotes)**
* **[Create an alias for pushing to all remote branches](#create-an-alias-for-pushing-to-all-remote-branches)**
* **[Bundle a git repo to a zip file](#bundle-a-git-repo-to-a-zip-file)**
* **[Overwrite a branch entirely with another branch](#overwrite-a-branch-entirely-with-another-branch)**

### Basic Add, Commit, Push
```
git add .
git commit -m "Description"
git push origin master
```

### Basic Pull
```
git pull origin master
```

### Create new branch
```
git checkout -b new-branch
```

### Merge new branch to master
```
git checkout master
git merge new-branch
```

### Rebase master onto new branch
```
Warning: Never rebase a public/shared branch.

git checkout new-branch
git rebase master
```

### Merge vs Rebase
- `Merge` just means you are combining two branches together.
- `Rebase` on the otherhand means you are moving the base of the branch to a different position. (e.g. When you checkout to a new branch, you basically copy all the commits from the source branch. That separation is called the base of the new branch. Now, Rebasing means you will no longer use that separation because you will move the base to the latest commit of the source branch a.k.a. Rebase).
- Anyways, here is [The best explanation](https://hackernoon.com/git-merge-vs-rebase-whats-the-diff-76413c117333)

### See all branches
```
git branch -a
```

### Delete new branch
```
git branch -d new-branch
```

### Show list of files changed in a Commit
```
git diff-tree --no-commit-id --name-only -r <commit hash>
```

### Show contents of a Commit
```
git show <commit hash>
```

### Revert a Commit
```
git revert <commit hash>
```

### Revert a Commit from History
```
git revert --strategy resolve <commit hash>
```

### See a summary of changes between the Branch and the Origin
```
# You can replace master with your branch
git diff --stat origin/master
```
```
# or just use the following to dynamically check your current branch
git diff --stat @{u}
```

### See a log of Incoming Changes before you do a `git pull`
```
# You can replace master with your branch
git fetch && git log ..origin/master
```
```
# or just use the following to dynamically check your current branch
git fetch && git log ..@{u}
```

### See a log of Outgoing Changes before you do a `git push`
```
# You can replace master with your branch
git fetch && git log origin/master..
```
```
# or just use the following to dynamically check your current branch
git fetch && git log @{u}..
```

### Undo the last `git commit`
```
Warning: Create a new branch before rebasing to undo the last commit. Never rebase a public/shared branch.

git rebase -i head~2
# Then delete the 2nd line (e.g. pick XXXXXXX desription)
```

### Undo the last `git commit` without rebasing
```
git reset --soft head~1
```

### Remove git commited files or folders
```
(e.g. sensitive data which were accidentally pushed)

git filter-branch --tag-name-filter cat --index-filter 'git rm -r --cached --ignore-unmatch <name of file or folder>' --prune-empty -f -- --all
```

### Tell git to remember your git login
```
# Mac Only
git credential-osxkeychain
git config --global credential.helper osxkeychain
```
```
# Windows Only
git config --global credential.helper wincred
```
```
# Linux Only
git config --global credential.helper cache
# Set the cache to timeout after 1 hour (setting is in seconds)
git config --global credential.helper 'cache --timeout=3600'
```

### Pretty Git Log
```
# Variation 1
git log --date-order --graph --format="%C(green)%h%Creset %C(yellow)%an%Creset %C(blue bold)%ar%Creset %C(red bold)%d%Creset%s"
```
```
# Variation 1 with --all
git log --date-order --all --graph --format="%C(green)%h%Creset %C(yellow)%an%Creset %C(blue bold)%ar%Creset %C(red bold)%d%Creset%s"
```

```
# Variation 2
git log --graph --pretty=format:"%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset" --abbrev-commit
```
```
# Variation 2 with --all
git log --all --graph --pretty=format:"%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset" --abbrev-commit
```

### Stash Changes
```
git stash
```

### Re-apply Stashed Changes and delete from Stash List
```
git stash pop
```

### Re-apply Stashed Changes but do not delete from Stash List
- Useful when applying the stash to multiple branches
```
git stash apply
```

### View Stashed Changes
```
git stash list
```

### Stash Changes and Pull Updates
```
git stash
git pull
git stash pop
```

### Stash Changes and Merge a Branch
```
git stash
git merge <branch name>
git stash pop
```

### Push to all remote branches
```
git remote | xargs -L1 git push --all
```

### Push a specific branch to all remotes
```
git remote | xargs -L1 -I R git push R master
```

### Create an alias for pushing to all remote branches
```
git config --global alias.pushall '!git remote | xargs -L1 git push --all'
git pushall
```

### Bundle a GIT repo to a zip file
```
git bundle create <Destination Folder> --all
```

### Overwrite a branch entirely with another branch
For example, we want to overwrite `master` entirely with `dummy`
```
git checkout dummy
git merge -s ours master
git checkout master
git merge dummy
```

## ...more to come
