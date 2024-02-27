### `restore`

What if we want to restore changes from a previous version of our program? We can use `git restore`! There are a couple ways to do this.

If we want to restore files to the versions in the most recent commit, then we can run `git restore` without specifying a commit id:

```
git restore [path_to_file]
```

If we want to restore to a **specific** commit, we can identify that commit’s id and restore the files from that commit.

```
git restore --source=[commitID] [path_to_file]
```

or from remote: 
```
git restore --source=[remote-name]/[branch-name] [file_name]
```

### `switch`

Switching between branches: 
```
git switch [branch-name]
```

### Fatal: refusing to merge unrelated histories

This usually occurs when someone has changed files in the skeleton code after you have pulled. To fix, run `git pull <remote-repo> main --allow-unrelated-histories --no-rebase`. This may force a merge conflict (more information below).

The reason we add the flags `--allow-unrelated-histories` and `--no-rebase` is because our two repositories don’t have any related history, so we’re going to try to merge these two branches (our local one and the one we’re pulling from).

In merge conflict files, everything between `<<<<<<< HEAD` and `=======` is from your local version. Everything between `=======` and `27ddd0c71515e5cfc7f58a43bcf0e2144c127aed` is from your remote repository. 

### Your branch is ahead of ‘origin/main’ by X commits.

This occurs when the local repo is no longer in sync with its remote counterpart. If you want to keep the local versions of your files, use `git push`. If you want to overwrite your local changes with the versions in the remote repo, use `git reset --hard origin/main`.

### `git pull`

In the command `git pull origin main`, the term `main` refers to the branch on the remote repository (in this case, the remote repository named "origin"). It specifies that you want to pull changes from the remote repository's "main" branch and merge them into your currently checked-out local branch.

If you want to be more explicit and specify both the remote and local branches, you can use the following syntax:

`git pull origin main:main`

This explicitly states that you want to pull changes from the remote branch named "main" and merge them into the local branch also named "main".

### `git push`

in the command `git push origin main`, the term `main` refers to the local branch. It indicates that you want to push the changes from your local branch named "main" to the remote repository named "origin."


## Visualizing Git 

https://git-school.github.io/visualizing-git/#free-remote - visualizing Git 