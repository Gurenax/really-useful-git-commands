# Really Useful GITcommands
A summary of GIT commands that I personally use because they're really useful

## Check Incoming Changes before you do a `git pull`
```
git fetch && git log ..origin/master
# You can replace master with your branch
```

## Check Outgoing Changes before you do a `git push`
```
git fetch && git log origin/master..
# You can replace master with your branch
```

## Undo the last commit
```
git rebase -i head~2
# Then delete the 2nd line (e.g. pick XXXXXXX desription)
```
