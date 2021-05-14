# GIT MERGE BRANCH IF CONFLICT
1. initialize (configure main branch)
2. configure secondary branch
3. update sample file on main branch (for conflict)
4. merge secondary branch to main branch
5. resolve conflict
6. show commit logs
7. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. create empty git repository (main branch)
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-merge-branch-if-conflict/.git/
```

### 1.2. create sample file
- on main branch

```console
$ vi 002-git-merge-branch-if-conflict.txt
```

```shell
init 002-git-merge-branch-if-conflict
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
- on main branch

```console
$ git add 002-git-merge-branch-if-conflict.txt
```

#### 1.3.2. commit
- on main branch

```console
$ git commit -m "init 002-git-merge-branch-if-conflict.txt"
[main c293295] init 002-git-merge-branch-if-conflict.txt
 1 file changed, 1 insertion(+)
 create mode 100644 002-git-merge-branch-if-conflict.txt
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

- on main branch

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
$ vi 002-git-merge-branch-if-conflict.txt
```

```shell
init 002-git-merge-branch-if-conflict
add secondary-branch
```

### 2.5. record changes to repository
#### 2.5.1. add file to index
- on secondary branch

```console
$ git add 002-git-merge-branch-if-conflict.txt
```

#### 2.5.2. commit
- on secondary branch

```console
$ git commit -m "add secondary-branch"
[secondary-branch aff567e] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 3. update sample file on main branch (for conflict)
### 3.1. switch main branch
- on secondary branch

```console
$ git checkout main
Switched to branch 'main'
```

### 3.2. update sample file
- on main branch

```console
$ vi 002-git-merge-branch-if-conflict.txt
```

```shell
init 002-git-merge-branch-if-conflict
add main-branch
```

### 3.3. record changes to repository
#### 3.3.1. add file to index
- on main branch

```console
$ git add 002-git-merge-branch-if-conflict.txt
```

#### 3.3.2. commit
- on main branch

```console
$ git commit -m "add main-branch"
[main 465f1b7] add main-branch
 1 file changed, 1 insertion(+)
```

## 4. merge secondary branch to main branch
- on main branch

```console
$ git merge secondary-branch
Auto-merging 002-git-merge-branch-if-conflict.txt
CONFLICT (content): Merge conflict in 002-git-merge-branch-if-conflict.txt
Automatic merge failed; fix conflicts and then commit the result.
```

## 5. resolve conflict
### 5.1. show sample file
- on main branch

```console
$ cat 002-git-merge-branch-if-conflict.txt
init 002-git-merge-branch-if-conflict
<<<<<<< HEAD
add main-branch
=======
add secondary-branch
>>>>>>> secondary-branch
```

### 5.2. modify sample file
- on main branch

```console
$ vi 002-git-merge-branch-if-conflict.txt
```

```shell
init 002-git-merge-branch-if-conflict
add main-branch
add secondary-branch
```

### 5.3. add file to index
- on main branch

```console
$ git add 002-git-merge-branch-if-conflict.txt
```

### 5.4. commit
- on main branch

```console
$ git commit -m "fix merge conflict"
[main ff5072a] fix merge conflict
```

### 5.5. show sample file after merging
- on main branch

```console
$ cat 002-git-merge-branch-if-conflict.txt
init 002-git-merge-branch-if-conflict
add main-branch
add secondary-branch
```

## 6. show commit logs
- on main branch

```console
$ git log
commit ff5072a336753ed6495db72851e15f58e523fb02 (HEAD -> main)
Merge: 465f1b7 aff567e
~
    fix merge conflict

commit 465f1b70c1650b914328dcef50515a361270cf90
~
    add main-branch

commit aff567e46c04eb7f46e5dd76c3fc98a1133091b3 (secondary-branch)
~
    add secondary-branch

commit c293295f99de2769a15a62d35c83253fbbdf0bd5
~
    init 002-git-merge-branch-if-conflict.txt
```

- on secondary branch

```console
$ git log
commit aff567e46c04eb7f46e5dd76c3fc98a1133091b3 (HEAD -> secondary-branch)
~
    add secondary-branch

commit c293295f99de2769a15a62d35c83253fbbdf0bd5
~
    init 002-git-merge-branch-if-conflict.txt
```

## 7. (Optional) delete secondary branch
- on main branch

```console
$ git branch -d secondary-branch
Deleted branch secondary-branch (was aff567e).
```
