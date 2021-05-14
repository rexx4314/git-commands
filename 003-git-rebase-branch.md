# GIT REBASE BRANCH
1. initialize (configure main branch)
2. configure secondary branch
3. rebase main branch
4. merge secondary branch to main branch
5. show commit logs
6. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. create empty git repository (main branch)
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-rebase-branch/.git/
```

### 1.2. create sample file
- on main branch

```console
$ vi 003-git-rebase-branch.txt
```

```shell
init 003-git-rebase-branch
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
- on main branch

```console
$ git add 003-git-rebase-branch.txt
```

#### 1.3.2. commit
- on main branch

```console
$ git commit -m "init 003-git-rebase-branch.txt"
[main (root-commit) 847b142] init 003-git-rebase-branch.txt
 1 file changed, 1 insertion(+)
 create mode 100644 003-git-rebase-branch.txt
```

## 2. configure secondary branch
### 2.1. create secondary branch
- on main branch

```console
$ git branch secondary-branch
```

### 2.2. switch secondary branch
- on main branch

```console
$ git checkout secondary-branch
Switched to branch 'secondary-branch'
```

> create and switch branch at the same time

```console
$ git checkout -b secondary-branch
Switched to a new branch 'secondary-branch'
```

### 2.3. show branch list
- on secondary branch

```console
$ git branch
  main
* secondary-branch
```

### 2.4. update sample file
- on secondary branch

```console
$ vi 003-git-rebase-branch.txt
```

```shell
init 003-git-rebase-branch
add secondary-branch
```

### 2.5. record changes to repository
#### 2.5.1. add file to index
- on secondary branch

```console
$ git add 003-git-rebase-branch.txt
```

#### 2.5.2. commit
- on secondary branch

```console
$ git commit -m "add secondary-branch"
[secondary-branch aabe3f4] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 3. rebase main branch
- on secondary branch

```console
$ git rebase -i main
```

```shell
pick aabe3f4 add secondary-branch

# Rebase 847b142..aabe3f4 onto 847b142 (1 command)
#
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

```console
Successfully rebased and updated refs/heads/secondary-branch.
```

## 4. merge secondary branch to main branch
### 4.1. switch to main branch
- on secondary branch

```console
$ git checkout main
Switched to branch 'main'
```

### 4.2. show sample file
- on main branch

```console
$ cat 003-git-rebase-branch.txt
init 003-git-rebase-branch
```

### 4.3. merge
- on main branch

```console
$ git merge secondary-branch
Updating 847b142..aabe3f4
Fast-forward
 003-git-rebase-branch.txt | 1 +
 1 file changed, 1 insertion(+)
```

### 4.4. show sample file after merging
- on main branch

```console
$ cat 003-git-rebase-branch.txt
init 003-git-rebase-branch
add secondary-branch
```

## 5. show commit logs
- on main branch

```console
$ git log
commit aabe3f42da1deece7c4a3827582f886d0ee10bbf (HEAD -> main, secondary-branch)
~
    add secondary-branch

commit 847b142a77a5c0a9bcef87e8953f99fe8718f2c2
~
    init 003-git-rebase-branch.txt
```

- on secondary branch

```console
$ git log
commit aabe3f42da1deece7c4a3827582f886d0ee10bbf (HEAD -> secondary-branch, main)
~
    add secondary-branch

commit 847b142a77a5c0a9bcef87e8953f99fe8718f2c2
~
    init 003-git-rebase-branch.txt
```

## 6. (Optional) delete secondary branch
- on main branch

```console
$ git branch -d secondary-branch
Deleted branch secondary-branch (was aabe3f4).
```
