# Really Useful GIT commands
A collection of GIT commands that I personally use because they're really useful. This is a work in progress, please feel free to Contribute.

## Contents
* **[Basic Add, Commit, Push](#BasicAddCommitPush)**
* **[Basic Pull](#BasicPull)**
* **[Create new branch](#CreateNewBranch)**
* **[Merge new branch to master](#MergeNewBranchToMaster)**
* **[Rebase master onto new branch](#RebaseMasterOntoNewBranch)**
* **[Merge vs Rebase](#MergeVsRebase)**
* **[See all branches](#SeeAllBranches)**
* **[Delete new branch](#DeleteNewBranch)**
* **[Revert a Commit](#RevertACommit)**
* **[See a summary of changes between the Branch and the Origin](#SeeASummaryOfChangesBetweenTheBranchAndTheOrigin)**
* **[See a log of Incoming Changes before you do a git pull](#SeeALogOfIncomingChangesBeforeYouDoAGitPull)**
* **[See a log of Outgoing Changes before you do a git push](#SeeALogOfOutgoingChangesBeforeYouDoAGitPush)**
* **[Undo the last git commit](#UndoTheLastGitCommit)**
* **[Remove git commited files or folders](#RemoveGitCommitedFilesOrFolders)**
* **[Tell git to remember your git login](#TellGitToRememberYourGitLogin)**
* **[Pretty Git Log](#PrettyGitLog)**

### <a id="BasicAddCommitPush"></a>Basic Add, Commit, Push
```
git add .
git commit -m "Description"
git push origin master
```

### <a id="BasicPull"></a>Basic Pull
```
git pull origin master
```

### <a id="CreateNewBranch"></a>Create new branch
```
git checkout -b new-branch
```

### <a id="MergeNewBranchToMaster"></a>Merge new branch to master
```
git checkout master
git merge new-branch
```

### <a id="RebaseMasterOntoNewBranch"></a>Rebase master onto new branch
*Warning: Never rebase a public/shared branch.*
```
git checkout new-branch
git rebase master
```

### <a id="MergeVsRebase"></a>Merge vs Rebase
- `Merge` just means you are combining two branches together.
- `Rebase` on the otherhand means you are moving the base of the branch to a different position. (e.g. When you checkout to a new branch, you basically copy all the commits from the source branch. That separation is called the base of the new branch. Now, Rebasing means you will no longer use that separation because you will move the base to the latest commit of the source branch a.k.a. Rebase).
- Anyways, here is [The best explanation](https://hackernoon.com/git-merge-vs-rebase-whats-the-diff-76413c117333)

### <a id="SeeAllBranches"></a>See all branches
```
git branch -a
```

### <a id="DeleteNewBranch"></a>Delete new branch
```
git branch -d new-branch
```

### <a id="RevertACommit"></a>RevertACommit
```
git revert <commit hash>
```

### <a id="SeeASummaryOfChangesBetweenTheBranchAndTheOrigin"></a>See a summary of changes between the Branch and the Origin
```
# You can replace master with your branch
git diff --stat origin/master
```
```
# or just use the following to dynamically check your current branch
git diff --stat @{u}
```

### <a id="SeeALogOfIncomingChangesBeforeYouDoAGitPull"></a>See a log of Incoming Changes before you do a `git pull`
```
# You can replace master with your branch
git fetch && git log ..origin/master
```
```
# or just use the following to dynamically check your current branch
git fetch && git log ..@{u}
```

### <a id="SeeALogOfOutgoingChangesBeforeYouDoAGitPush"></a>See a log of Outgoing Changes before you do a `git push`
```
# You can replace master with your branch
git fetch && git log origin/master..
```
```
# or just use the following to dynamically check your current branch
git fetch && git log @{u}..
```

### <a id="UndoTheLastGitCommit"></a>Undo the last `git commit`
*Warning: Create a new branch before rebasing to undo the last commit. Never rebase a public/shared branch.*
```
git rebase -i head~2
# Then delete the 2nd line (e.g. pick XXXXXXX desription)
```

### <a id="RemoveGitCommitedFilesOrFolders"></a>Remove git commited files or folders (e.g. sensitive data which were accidentally pushed)
```
git filter-branch --tag-name-filter cat --index-filter 'git rm -r --cached --ignore-unmatch <name of file or folder>' --prune-empty -f -- --all
```

### <a id="TellGitToRememberYourGitLogin"></a>Tell git to remember your git login
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

### <a id="PrettyGitLog"></a>Pretty Git Log
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

## ...more to come
