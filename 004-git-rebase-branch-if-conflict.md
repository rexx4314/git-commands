# GIT REBASE BRANCH IF CONFLICT
1. initialize (configure main branch)
2. configure secondary branch
3. rebase main branch
4. modify sample file on main branch (for conflict)
5. rebase main branch again
6. resolve conflict
7. rebase main branch with '--continue'
8. merge secondary branch to main branch
9. show commit logs
10. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. create empty git repository (main branch)
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-rebase-branch-if-conflict/.git/
```

### 1.2. create sample file
- on main branch

```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
- on main branch

```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

#### 1.3.2. commit
- on main branch

```console
$ git commit -m "init 004-git-rebase-branch-if-conflict.txt"
[main (root-commit) 270c807] init 004-git-rebase-branch-if-conflict.txt
 1 file changed, 1 insertion(+)
 create mode 100644 004-git-rebase-branch-if-conflict.txt
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
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
add secondary-branch
```

### 2.5. record changes to repository
#### 2.5.1. add file to index
- on secondary branch

```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

#### 2.5.2. commit
- on secondary branch

```console
$ git commit -m "add secondary-branch"
[secondary-branch c745ae4] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 3. rebase main branch
- on secondary branch

```console
$ git rebase -i main
```

```shell
pick c745ae4 add secondary-branch

# Rebase 270c807..c745ae4 onto 270c807 (1 command)
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

## 4. modify sample file on main branch (for conflict)
### 4.1. switch to main branch
- on secondary branch

```console
$ git checkout main
Switched to branch 'main'
```

### 4.2. update sample file
- on main branch

```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
add main-branch
```

### 4.3. record changes to repository
#### 4.3.1. add file to index
- on main branch

```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

#### 4.3.2. commit
- on main branch

```console
$ git commit -m "add main-branch"
[main 5a5184a] add main-branch
 1 file changed, 1 insertion(+)
```

## 5. rebase main branch again
### 5.1. switch secondary branch
- on main branch

```console
$ git checkout secondary-branch
Switched to branch 'secondary-branch'
```

### 5.2. rebase
- on secondary branch

```console
$ git rebase -i main
```

```shell
pick c745ae4 add secondary-branch

# Rebase 5a5184a..c745ae4 onto 5a5184a (1 command)
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
error: could not apply c745ae4... add secondary-branch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

Could not apply c745ae4... add secondary-branch
```

## 6. resolve conflict
### 6.1. show sample file
- on secondary branch

```console
$ cat 004-git-rebase-branch-if-conflict.txt
init 004-git-rebase-branch-if-conflict
<<<<<<< HEAD
add main-branch
=======
add secondary-branch
>>>>>>> c745ae4... add secondary-branch
```

### 6.2. modify sample file
- on secondary branch

```console
$ vi 004-git-rebase-branch-if-conflict.txt
```

```shell
init 004-git-rebase-branch-if-conflict
add main-branch
add secondary-branch
```

### 6.3. add file to index
- on secondary branch

```console
$ git add 004-git-rebase-branch-if-conflict.txt
```

## 7. rebase main branch with '--continue'
- on secondary branch

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
# interactive rebase in progress; onto 5a5184a
# Last command done (1 command done):
#    pick c745ae4 add secondary-branch
# No commands remaining.
# You are currently rebasing branch 'secondary-branch' on '5a5184a'.
#
# Changes to be committed:
#       modified:   004-git-rebase-branch-if-conflict.txt
#
```

```console
[detached HEAD d4a4ccf] add secondary-branch
 1 file changed, 1 insertion(+)
Successfully rebased and updated refs/heads/secondary-branch.
```

## 8. merge secondary branch to main branch
### 8.1. switch to main branch
- on secondary branch

```console
$ git checkout main
Switched to branch 'main'
```

### 8.2. show sample file
- on main branch

```console
$ cat 004-git-rebase-branch-if-conflict.txt
init 004-git-rebase-branch-if-conflict
add main-branch
```

### 8.3. merge
- on main branch

```console
$ git merge secondary-branch
Updating 5a5184a..d4a4ccf
Fast-forward
 004-git-rebase-branch-if-conflict.txt | 1 +
 1 file changed, 1 insertion(+)
```

### 8.4. show sample file after merging
- on main branch

```console
$ cat 004-git-rebase-branch-if-conflict.txt
init 004-git-rebase-branch-if-conflict
add main-branch
add secondary-branch
```

## 9. show commit logs
- on main branch

```console
$ git log
commit d4a4ccf0dfd426f27eb46c922f938bdef9717c01 (HEAD -> main, secondary-branch)
~
    add secondary-branch

commit 5a5184a5c8b98e1bdd1c08d2a962b2089a62bd53
~
    add main-branch

commit 270c807b75f6046f1f0a5260af06236451f62102
~
    init 004-git-rebase-branch-if-conflict.txt
```

- on secondary branch

```console
$ git log
commit d4a4ccf0dfd426f27eb46c922f938bdef9717c01 (HEAD -> secondary-branch, main)
~
    add secondary-branch

commit 5a5184a5c8b98e1bdd1c08d2a962b2089a62bd53
~
    add main-branch

commit 270c807b75f6046f1f0a5260af06236451f62102
~
    init 004-git-rebase-branch-if-conflict.txt
```

## 10. (Optional) delete secondary branch
- on main branch

```console
$ git branch -d secondary-branch
Deleted branch secondary-branch (was d4a4ccf).
```
