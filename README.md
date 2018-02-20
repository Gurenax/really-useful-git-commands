# Really Useful GIT commands
A collection of GIT commands that I personally use because they're really useful. This is a work in progress, please feel free to Contribute.


## See a summary of changes between the Branch and the Origin
```
git diff --stat origin/master
# You can replace master with your branch
```

## See a log of Incoming Changes before you do a `git pull`
```
git fetch && git log ..origin/master
# You can replace master with your branch
```

## See a log of Outgoing Changes before you do a `git push`
```
git fetch && git log origin/master..
# You can replace master with your branch
```

## Undo the last `git commit`
```
git rebase -i head~2
# Then delete the 2nd line (e.g. pick XXXXXXX desription)
```
