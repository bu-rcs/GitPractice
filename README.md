# Practice
RCS Repository to practice Git tools

### Setup terminal and OnDemand Environment
```{bash}
module load python3
```

### Uncommitted changes

to review the changes that have been done to the files (and has not been committed yet) with the last commit:
```{bash}
git diff
```

To see the changes that you have already moved to the staging area (ready to be committed):
```{bash}
git diff --staged
# or
git diff --cached
```

*******


If you are working in the **VSCode**, click the Git icon on the side bar and then click the name of the modified file
you would like to review:

- The left side is the file as it exists in the last commit (or the Staging Area for unstaged changes).
- The right side is your current modified working file.

If you use **vim** as your code editor, you can set your difftool to use vim:

```{bash}
git config --global diff.tool vimdiff
git config --global difftool.prompt false
```
*******


## Updating the last commit message or adding forgotten files

```{bash}
git commit --amend -m "Your new, corrected commit message here"
```

If you need to add some files to your last commit:
```{bash}
# Stage the specific file(s) you forgot
git add <file1> <file2>

# OR, to stage all tracked, modified files:
# git add .

#
git commit --amend --no-edit
```


Since amending a commit changes the commit's history (it gets a brand new `SHA-1` hash), you should **NEVER** amend a commit that has already been pushed to a shared remote repository and possibly pulled by other developers.

If you must amend a commit that has already been pushed, you will need to force-push the change, which is generally discouraged:
```{bash}
git push --force-with-lease origin <your-branch-name>
```

The `--force-with-lease` option adds a crucial safety check before overwriting the remote branch. This effectively means: "I want to force push, but only if no one else has pushed any new commits to the remote branch since I last fetched."

The `--force` option is a command of pure power that unconditionally overwrites the remote branch. It overwrites the remote branch with your local branch's history, regardless of what has happened on the remote since your last fetch. If another developer has pushed new commits to that same branch (commits you don't have locally), `--force` will wipe out their commits completely and permanently from the remote repository without warning.