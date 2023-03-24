# Git Command Fondue before forgot it again

## Abstract

- [Initialize repository](#Initialize-repository)
- [Add changes to staging area and commit](#Add-changes-to-staging-area-and-commit)
- [Undo git commit](#Undo-git-commit)
  - Undo git commit
  - Undo git commit + git add + unstage
  - Undo git commit and remove changes
- [Undo a commit that's already been pushed](#Undo-a-commit-thats-already-been-pushed)
- [Unstage all changes that are currently staged](#Unstage-all-changes-that-are-currently-staged)
- [See only wanted directory in git status](#See-only-wanted-directory-in-git-status)
- [General commands](#General-commands)
- [Merge branch to main](#Merge-branch-to-main)
- [Different push commands](#Different-push-commands)
  - git push
  - git push origin main
  - git push -u origin main
  - git push --set-upstream <repo-name> Changes

## [Initialize repository](#Initializing-a-repository)

```
git init
git remote add origin <you-git-link>
git add .
git commit -m "Initial commit"
git branch -M main
git push -u origin main
```

Before anything: Change directory into the relevant root directory for the project  
`init` - initialize repository  
`origin` - default given name to remote repository, can be named differently

## [Add changes to staging area and commit](#Add-changes-to-staging-area-and-commit)

```
git add .
git commit -m "Initial commit"
```

- `git add .` - add _all_ changes to the staging area
- `git add <filename>` - add _specific file_ changes to the staging area
- `git commit` - creates new commit from the changes in the staging area

## [Undo git commit](#Undo-git-commit)

1. Undo `git commit`. Changes still exist in the working tree _(project's files and directories)_ + index _(staging area)_ (--cached):

   ```
   git reset HEAD^ --soft
   ```

`HEAD` - points to the tip of that branch (most recent commit)  
`^` - one commit before  
`HEAD^` - refers to the parent commit of the current `HEAD`  
`--soft` - Changes made in the last commit are uncommitted and goes back to the staging area so that you can modify them before committing again.

2. Undo `git commit` + `git add` + unstage. Changes still exist in the working tree:

   ```
   git reset HEAD^ --mixed
   ```

`--mixed` - resets the current branch and index to the specified commit but does not modify the working tree. The changes that were previously staged are not carried over, so you'll have to stage them again using `git add`.

3. Undo `git commit` and remove changes. Removes the most recent commit and all of the changes made in that commit.

   ```
   git reset HEAD^ --hard
   ```

`--hard` - remove the commit and all the changes introduced in that commit will not be recoverable through Git. Changes are gone from the working tree, index, and local repository. This option resets everything **back to the state of the last commit**.

## [Undo a commit that's already been pushed](#Undo-a-commit-thats-already-been-pushed)

Create a new commit that _reverses the changes_ made by specified commit, without applying that it.

```
git revert -n <sha>
```

`SHA` - commit identifier in Git. Stands for Secure Hash Algorithm. It's a 40-character string that identifies the state of a particular commit, tree or blob.  
`<sha>` - your commit's SHA  
`-n` - flag that allows you to make additional changes to the files before committing them

Example:

If you want to undo commit with SHA _a1b2c3_, command `git revert -n a1b2c3` will undo the changes introduced by the commit _a1b2c3_. Changes will be staged, you can review them before committing.

## [Unstage all changes that are currently staged](#Unstage-all-changes-that-are-currently-staged)

```
git reset
```

## [See only wanted directory in git status](#See-only-wanted-directory-in-git-status)

```
git status <directory-name>
```

## [General commands](#General-commands)

```
git commit -m "Add new feature"
```

```
git fetch origin
```

```
git merge origin/main
```

```
git pull origin
```

```
git push origin main
```

## [Merge branch to main](#Merge-branch-to-main)

```
git checkout main
git pull
git merge <feature-branch>
```

\* _Resolve any conflicts and then push the changes to the remote main branch_ \*:

```
git add .
git commit
git push
```

## [Different push commands](#Different-push-commands)

1. Default. Pushes changes to the corresponding branch on the upstream repository (the configured remote destination) of the local branch that your current branch is tracking. If the upstream branch doesn't exist yet, you'll need to set up an upstream branch.

```
git push
```

2. "Push changes of `main` to `origin`"

```
git push origin main
```

`main` - local branch whose contents should be pushed to the remote repository

3. Same as [2.] but also sets the upstream branch to use git pull going forward, without specifying any arguments (`-u` or `--set-upstream`).

```
git push -u origin main
```

`-u` - required for the first time you're pushing a new branch. After that `git push` for all future pushes.

4. "Not your repo but still want to push".

```
git push --set-upstream <repo-name> Changes
```

`--set-upstream` - sets up the current branch to track a remote branch (which was created by someone else)
`Changes` - refers to whatever changes you want to push
