# Really Useful GIT commands
A collection of GIT commands that I personally use because they're really useful. This is a work in progress, please feel free to Contribute.

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

### See all branches
```
git branch -a
```

### Delete new branch
```
git branch -d new-branch
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
git rebase -i head~2
# Then delete the 2nd line (e.g. pick XXXXXXX desription)
```

### Remove git commited files or folders (e.g. sensitive data which were accidentally pushed)
```
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

### ...more to come
