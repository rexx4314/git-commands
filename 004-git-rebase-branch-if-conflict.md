# GIT REBASE BRANCH IF CONFLICT
1. initialize (configure main branch)
2. configure secondary branch
3. rebase main branch
4. reconfigure main branch (for conflict)
5. reconfigure secondary branch (for conflict)
6. rebase main branch (on secondary branch)
7. resolve conflict
8. merge secondary branch to main branch
9. show commit logs
10. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. create empty git repository
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-rebase-branch-if-conflict/.git/
```

### 1.2. create sample file (on main branch)
```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
```

### 1.3. record changes to repository (main branch)
#### 1.3.1. add file to index
```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

#### 1.3.2. commit
```console
$ git commit -m "init 004-git-rebase-branch-if-conflict.txt"
[main (root-commit) 0ee3bbe] init 004-git-rebase-branch-if-conflict.txt
 1 file changed, 1 insertion(+)
 create mode 100644 004-git-rebase-branch-if-conflict.txt
```

## 2. configure secondary branch
### 2.1. create secondary branch
```console
$ git branch secondary-branch
```

### 2.2. switch secondary branch
```console
$ git checkout secondary-branch
Switched to branch 'secondary-branch'
```

> create and switch branch at the same time

```console
$ git checkout -b secondary-branch
Switched to branch 'secondary-branch'
```

### 2.3. show branch list
```console
$ git branch
  main
* secondary-branch
```

### 2.4. update sample file
```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
add secondary-branch
```

### 2.5. record changes on secondary branch
#### 2.5.1. add file to index
```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

#### 2.5.2. commit
```console
$ git commit -m "add secondary-branch"
[secondary-branch 4d5bc5b] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 3. rebase main branch
```console
$ git rebase -i main
```

```shell
pick 4d5bc5b add secondary-branch

# Rebase 0ee3bbe..4d5bc5b onto 0ee3bbe (1 command)
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

## 4. reconfigure main branch (for conflict)
### 4.1. switch to main branch
```console
$ git checkout main
Switched to branch 'main'
```

### 4.2. update sample file
```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
add main-branch
```

### 4.3. record changes on main branch
#### 4.3.1. add file to index
```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

#### 4.3.2. commit
```console
$ git commit -m "add main-branch"
[main c9be4c2] add main-branch
 1 file changed, 1 insertion(+)
```

## 5. reconfigure secondary branch (for conflict)
### 5.1. switch secondary branch
```console
$ git checkout secondary-branch
Switched to branch 'secondary-branch'
```

### 5.2. update sample file
```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
add secondary-branch
add secondary-branch-2
```

### 5.3. record changes on secondary branch
#### 5.3.1. add file to index
```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

#### 5.3.2. commit
```console
$ git commit -m "add secondary-branch 2"
[secondary-branch c480511] add secondary-branch 2
 1 file changed, 1 insertion(+)
```

## 6. rebase main branch (on secondary branch)
```console
$ git rebase -i main
```

```shell
pick 4d5bc5b add secondary-branch

# Rebase c9be4c2..4d5bc5b onto c9be4c2 (1 command)
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
Auto-merging 004-git-rebase-branch-if-conflict.txt
CONFLICT (content): Merge conflict in 004-git-rebase-branch-if-conflict.txt
error: could not apply 4d5bc5b... add secondary-branch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

Could not apply 4d5bc5b... add secondary-branch
```

## 7. resolve conflict
### 7.1. show sample file on secondary branch
```console
$ cat 004-git-rebase-branch-if-conflict.txt
init 004-git-rebase-branch-if-conflict
<<<<<<< HEAD
add main-branch
=======
add secondary-branch
>>>>>>> 4d5bc5b... add secondary-branch
```

### 7.2. resolve conflict
#### 7.2.1. modify sample file
```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
add main-branch
add secondary-branch
```

#### 7.2.2. add file to index
```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

```console
$ git rebase --continue
```

```shell
add secondary-branch

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Committer: Ubuntu <ubuntu@ip-10-0-0-150.ap-northeast-2.compute.internal>
#
# interactive rebase in progress; onto c9be4c2
# Last command done (1 command done):
#    pick 4d5bc5b add secondary-branch
# No commands remaining.
# You are currently rebasing branch 'secondary-branch' on 'c9be4c2'.
#
# Changes to be committed:
#       modified:   004-git-rebase-branch-if-conflict.txt
#
```

```console
[detached HEAD 870fff2] add secondary-branch
 1 file changed, 1 insertion(+)
Successfully rebased and updated refs/heads/secondary-branch.
```

## 8. merge secondary branch to main branch
### 8.1. switch to main branch
```console
$ git checkout main
Switched to branch 'main'
```

### 8.2. show sample file on main branch
```console
$ cat 004-git-rebase-branch-if-conflict.txt
init 004-git-rebase-branch-if-conflict
add main-branch
```

### 8.3. merge
```console
$ git merge secondary-branch
Updating c9be4c2..870fff2
Fast-forward
 004-git-rebase-branch-if-conflict.txt | 1 +
 1 file changed, 1 insertion(+)
```

### 8.4. show sample file on main branch
```console
$ cat 004-git-rebase-branch-if-conflict.txt
init 004-git-rebase-branch-if-conflict
add main-branch
add secondary-branch
```

## 9. show commit logs

- in main branch

```console
$ git log
commit 870fff26bec35eee8aea7a8db0e1a247ee2925f2 (HEAD -> main, secondary-branch)
~
    add secondary-branch

commit c9be4c2a397ad75b78180a8d3c630f7418d002ac
~
    add main-branch

commit 0ee3bbe1355efbd33f16bef0952ca9027754a76d
~
    init 004-git-rebase-branch-if-conflict.txt
```

- in secondary branch

```console
$ git log
commit 870fff26bec35eee8aea7a8db0e1a247ee2925f2 (HEAD -> secondary-branch, main)
~
    add secondary-branch

commit c9be4c2a397ad75b78180a8d3c630f7418d002ac
~
    add main-branch

commit 0ee3bbe1355efbd33f16bef0952ca9027754a76d
~
    init 004-git-rebase-branch-if-conflict.txt
```

## 10. (Optional) delete secondary branch

- in main branch

```console
$ git branch -d secondary-branch
Deleted branch secondary-branch (was c957a83).
```
