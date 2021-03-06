---
layout: post
title: "Git Basics: Rename local and remote branch"
categories: ['Programming']
tags:
 - Git
---

Sometimes we name a git branch with something temporary and would like to change to more meaningful name etc, it does not happen every day but happens time to time.

Following git commands can be used to rename local and remote branches.

Make sure the branch is clean, not changes or pending commits/pushes etc.

**1. Rename local branch**
If you already on the branch that you would like to rename

 ```bash
 git branch -m new-name
  ```
If you are on some other branch
  ```bash
  git branch -m old-name new-name
  ```

**2. Delete the remote branch with the old-name and push the local branch with new-name.**

Following command renames the old branch and pushes the local change to the new branch
```bash
git push origin :old-name new-name
```

**3. Reset the upstream branch.**

If you have not switched to new branch then switch to the branch and then use the following command

```bash
git push origin -u new-name
```


git push [reference](https://git-scm.com/docs/git-push)