# GIT MERGE BRANCH
1. initialize (configure main branch)
2. configure secondary branch
3. merge secondary branch to main branch
4. show commit logs
5. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. create empty git repository (main branch)
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-merge-branch/.git/
```

### 1.2. create sample file
- on main branch

```console
$ vi 001-git-merge-branch.txt
```

```shell
init 001-git-merge-branch
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
- on main branch

```console
$ git add 001-git-merge-branch.txt
```

#### 1.3.2. commit
- on main branch

```console
$ git commit -m "init 001-git-merge-branch.txt"
[main (root-commit) 50d1646] init 001-git-merge-branch.txt
 1 file changed, 1 insertion(+)
 create mode 100644 001-git-merge-branch.txt
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
$ vi 001-git-merge-branch.txt
```

```shell
init 001-git-merge-branch
add secondary-branch
```

### 2.5. record changes to repository
#### 2.5.1. add file to index
- on secondary branch

```console
$ git add 001-git-merge-branch.txt
```

#### 2.5.2. commit
- on secondary branch

```console
$ git commit -m "add secondary-branch"
[secondary-branch b245d9c] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 3. merge secondary branch to main branch
### 3.1. switch to main branch
- on secondary branch

```console
$ git checkout main
Switched to branch 'main'
```

### 3.2. show sample file
- on main branch

```console
$ cat 001-git-merge-branch.txt
init 001-git-merge-branch
```

### 3.3. merge
- on main branch

```console
$ git merge secondary-branch
Updating 50d1646..b245d9c
Fast-forward
 001-git-merge-branch.txt | 1 +
 1 file changed, 1 insertion(+)
```

### 3.4. show sample file after merging
- on main branch

```console
$ cat 001-git-merge-branch.txt
init 001-git-merge-branch
add secondary-branch
```

## 4. show commit logs
- on main branch

```console
$ git log
commit b245d9c310fc97c0acef640585310473b9d41b0b (HEAD -> master, secondary-branch)
~
    add secondary-branch

commit 50d164692179ca4e7b0833154405c07165088f25
~
    init 001-git-merge-branch.txt
```

- on secondary branch

```console
$ git log
commit b245d9c310fc97c0acef640585310473b9d41b0b (HEAD -> secondary-branch, master)
~
    add secondary-branch

commit 50d164692179ca4e7b0833154405c07165088f25
~
    init 001-git-merge-branch.txt
```

## 5. (Optional) delete secondary branch
- on main branch

```console
$ git branch -d secondary-branch
Deleted branch secondary-branch (was b245d9c).
```
