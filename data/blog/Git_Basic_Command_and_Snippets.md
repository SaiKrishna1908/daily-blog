---
title: Git Basic Command and Snippets 🚀
date: '2020-12-20'
tags: ['git', 'vcs', 'basics']
draft: false
summary: Git commands to get you started with git vcs
images: []
layout: PostLayout
canonicalUrl:
---

# Git Basic Command and Snippets

### Git account setup in local

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

### Git list branches

```
List local branches

git branch -l

List remote branches

git branch -r
```

### Create a new repository and need to add it to local code as remote.

```
git remote add origin <url>
git push --set-upstream origin master
git pull
```

or

```
git remote add origin git@github.com:SaiKrishna1908/FactSO.git
git branch -M main
git push -u origin main

(or)

git push --set-upstream origin main
```

### Set a local branch to track a remote branch

```
git branch --set-upstream-to=upstream/foo
```

If your branch is ahead of remote repository and your local changes are bad, you can reset the local copy using

the following command

```
git reset --hard origin/<remote_tracking_branch>
```

### Pushing your changes on top of remote repository changes

```
git pull --rebase
```

### Make git pull do rebase by default

rebase makes your changes on top of remote changes. This is useful when you want to catch up with commits on other branches

```
git config --global pull.rebase true
```

Moving or combining a sequence of commits to a new base commit using rebase.

```
git rebase <base>  (where base is ID, a branch name, a tag, or a relative reference to HEAD).

git rebase --onto <main_branch>
```

###

### Resolving Merge Conflicts

```
git merge origin/<remote_branch>
merge conflicts..
Make changes to files
git add .
git rebase --continue
```

### Discard staged commits but keep Changes

```
git reset HEAD^
```

###

### Discard staged commits in local \(You will lose your changes\)

```
git reset --hard orgin/master
```

###

### Remove Files which are tracked using git add .

```
git rm --cached <filename>
```

### If you make changes in wrong branch and want to carry these changes to new branch do the following

```
git stash
git checkout <new-branch>
git stash apply (or) git stash pop
```

### Add only tracked files and ignore new files which are created by IDE or tools\!

```
git add -u
git checkout -b <new_branch_name>
git commit -m "Changes"
git push --set-upstream origin <new_branch_name>
```

### Revert a commit and push to remote

```
git log

git revert <commit_hash>

# Revert a range of commits

git revert <oldest_commit_hash>..<latest_commit_hash>
```

## **Git Amend**

Git Amend is the most convenient way to modify the most recent commit. Changes include rewriting the commit message or adding files which we forgot to add.

Usecase:

```
git add pub.yaml
git commit -m "initial commit"

# Forgot to add other files ?

git add main.dart
git commit --amend --no-edit
```

**Git Log**

Git log can be used to show commit logs of the repository

```
git log

# To view commit logs in one line
git log --oneline

# To show summary of git log output
git shortlog

# To summarize shortlog use the --summary flag
git shortlog --summary

# To view graph of commits
git log --graph --oneline --decorat

# To show only merged commit we can add --merges flag to log and shortlog
git log --oneline --merges
git shortlog --merges
```

At lot of filters can be applied to git log.

[https://www.atlassian.com/git/tutorials/git\-log](https://www.atlassian.com/git/tutorials/git-log)
