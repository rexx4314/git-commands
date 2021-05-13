# GIT REBASE BRANCH
1. initialize (configure main branch)
2. configure secondary branch
3. update sample file on secondary branch
4. rebase main branch
5. merge secondary branch to main branch
6. show commit logs
7. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. create empty git repository
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-rebase-branch/.git/
```

### 1.2. create sample file (on main branch)
```console
$ vi 003-git-rebase-branch.txt
```

```shell
init 003-git-rebase-branch
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
```console
$ git add 003-git-rebase-branch.txt
```

#### 1.3.2. commit
```console
$ git commit -m "init 003-git-rebase-branch.txt"
[main (root-commit) 0f8feda] init 003-git-rebase-branch.txt
 1 file changed, 1 insertion(+)
 create mode 100644 003-git-rebase-branch.txt
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

## 3. update sample file on secondary branch
### 3.1. update sample file
```console
$ vi 003-git-rebase-branch.txt
```

```shell
init 003-git-rebase-branch
add secondary-branch
```

### 3.2. record changes on secondary branch
#### 3.2.1. add file to index
```console
$ git add 003-git-rebase-branch.txt
```

#### 3.2.2. commit
```console
$ git commit -m "add secondary-branch"
[secondary-branch b1a70f2] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 4. rebase main branch
```console
$ git rebase -i HEAD~1
Successfully rebased and updated refs/heads/secondary-branch.
```

## 5. merge secondary branch to main branch
### 5.1. switch to main branch
```console
$ git checkout main
Switched to branch 'main'
```

### 5.2. show sample file on main branch
```console
$ cat 003-git-rebase-branch.txt
init 003-git-rebase-branch
```

### 5.3. merge
```console
$ git merge secondary-branch
Updating 0f8feda..b1a70f2
Fast-forward
 003-git-rebase-branch.txt | 1 +
 1 file changed, 1 insertion(+)
```

### 5.4. show sample file on main branch
```console
$ cat 003-git-rebase-branch.txt
init 003-git-rebase-branch
add secondary-branch
```

## 6. show commit logs

- in main branch

```console
$ git log
commit b1a70f28a157e8f01f581cc35523118c99956aa9 (HEAD -> main, secondary-branch)
~
    add secondary-branch

commit 0f8fedad3caf496836bb2a25c929ad032cdaabbf
~
    init 003-git-rebase-branch.txt
```

- in secondary branch

```console
$ git log
commit b1a70f28a157e8f01f581cc35523118c99956aa9 (HEAD -> secondary-branch, main)
~
    add secondary-branch

commit 0f8fedad3caf496836bb2a25c929ad032cdaabbf
~
    init 003-git-rebase-branch.txt
```

## 7. (Optional) delete secondary branch

- in main branch

```console
$ git branch -d secondary-branch
Deleted branch secondary-branch (was c957a83).
```
