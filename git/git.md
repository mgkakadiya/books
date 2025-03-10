# Git commands to clean up your local branches. Here are the commands for Windows:

## powershel

 1. To delete all local branches that are already merged into the current branch (usually main/master):

```
git branch --merged | findstr /v "* master main" | ForEach-Object { git branch -d $_.Trim() }
```
 2. To delete local branches that track remote branches which no longer exist (prune):
```
## First, fetch and prune
git fetch -p

## Then list and delete branches that are gone on remote
for /f "tokens=1" %G in ('git branch -vv ^| find ": gone]"') do git branch -D %G
```
You can also combine these operations into a single command:

```
git fetch -p && git branch -vv | findstr ": gone]" | ForEach-Object { git branch -D ($_ -split "\s+")[0] } && git branch --merged | findstr /v "* master main" | ForEach-Object { git branch -d $_.Trim() }
```

### Note:

- -d is for safe delete (only deletes if branch is merged)
- -D is for force delete
- fetch -p prunes tracking branches
- Make sure you're on the branch you want to keep (usually main/master) before running these commands
- Be careful with these commands as they will permanently delete local branches

## Command Prompt (cmd):
```
# First, fetch and prune
git fetch -p

# Then list and delete branches that are gone on remote
for /f "tokens=1" %G in ('git branch -vv ^| find ": gone]"') do git branch -D %G
```
## If you're using this in a batch file (.bat), use double % signs:

```
for /f "tokens=1" %%G in ('git branch -vv ^| find ": gone]"') do git branch -D %%G
```