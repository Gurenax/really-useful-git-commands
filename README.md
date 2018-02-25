# Really Useful GIT commands
A collection of GIT commands that I personally use because they're really useful. This is a work in progress, please feel free to Contribute.

## Contents
* **[Basic Add, Commit, Push](#BasicAddCommitPush)**
* **[Basic Pull](#BasicPull)**
* **[Create new branch](#CreateNewBranch)**
* **[Merge new branch to master](#MergeNewBranchToMaster)**
* **[See all branches](#SeeAllBranches)**
* **[Delete new branch](#DeleteNewBranch)**
* **[See a summary of changes between the Branch and the Origin](#SeeASummaryOfChangesBetweenTheBranchAndTheOrigin)**
* **[See a log of Incoming Changes before you do a git pull](#SeeALogOfIncomingChangesBeforeYouDoAGitPull)**
* **[See a log of Outgoing Changes before you do a git push](#SeeALogOfOutgoingChangesBeforeYouDoAGitPush)**
* **[Undo the last git commit](#UndoTheLastGitCommit)**
* **[Remove git commited files or folders](#RemoveGitCommitedFilesOrFolders)**
* **[Tell git to remember your git login](#TellGitToRememberYourGitLogin)**


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

### <a id="SeeAllBranches"></a>See all branches
```
git branch -a
```

### <a id="DeleteNewBranch"></a>Delete new branch
```
git branch -d new-branch
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
Warning: Once deleted, you will lose all files and changes pertaining to that commit and you cannot revert back and to a time.
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

## ...more to come
