# GIT MERGE BRANCH
1. initialize (configure main branch)
2. configure secondary branch
3. update sample file on secondary branch
4. merge secondary branch to main branch
5. show commit logs
6. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. create empty git repository
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-merge-branch/.git/
```

### 1.2. create sample file (on main branch)
```console
$ vi 001-git-merge-branch.txt
```

```shell
init 001-git-merge-branch
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
```console
$ git add 001-git-merge-branch.txt
```

#### 1.3.2. commit
```console
$ git commit -m "init 001-git-merge-branch.txt"
[main (root-commit) 17913f8] init 001-git-merge-branch.txt
 1 file changed, 1 insertion(+)
 create mode 100644 001-git-merge-branch.txt

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
$ vi 001-git-merge-branch.txt
```

```shell
init 001-git-merge-branch
add secondary-branch
```

### 3.2. record changes on secondary branch
#### 3.2.1. add file to index
```console
$ git add 001-git-merge-branch.txt
```

#### 3.2.2. commit
```console
$ git commit -m "add secondary-branch"
[secondary-branch c957a83] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 4. merge secondary branch to main branch
### 4.1. switch to main branch
```console
$ git checkout main
Switched to branch 'main'
```

### 4.2. show sample file on main branch
```console
$ cat 001-git-merge-branch.txt
init 001-git-merge-branch
```

### 4.3. merge
```console
$ git merge secondary-branch
Updating 17913f8..c957a83
Fast-forward
 001-git-merge-branch.txt | 1 +
 1 file changed, 1 insertion(+)
```

### 4.4. show sample file on main branch
```console
$ cat 001-git-merge-branch.txt
init 001-git-merge-branch
add secondary-branch
```

## 5. show commit logs

- in main branch

```console
$ git log
commit aba37f730f3a1a46907863c6b868ad23ed35db71 (HEAD -> main, secondary-branch)
~
    add secondary-branch

commit 17913f8bddf38addda9b083e5dd78ef68ed72764
~
    init 001-git-merge-branch.txt
```

- in secondary branch

```console
$ git log
commit aba37f730f3a1a46907863c6b868ad23ed35db71 (HEAD -> secondary-branch, main)
~
    add secondary-branch

commit 17913f8bddf38addda9b083e5dd78ef68ed72764
~
    init 001-git-merge-branch.txt
```

## 6. (Optional) delete secondary branch

- in main branch

```console
$ git branch -d secondary-branch
Deleted branch secondary-branch (was c957a83).
```
