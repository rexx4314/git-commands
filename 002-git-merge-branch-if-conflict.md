# GIT MERGE BRANCH IF CONFLICT
1. initialize (configure main branch)
2. configure secondary branch
3. update sample file on secondary branch
4. update sample file on main branch
5. merge secondary branch to main branch
6. updates remote refs
7. show commit logs
8. (Optional) delete secondary branch

## 1. initialize (configure main branch)
### 1.1. clone git repository
```
$ git clone ${GIT-REPOSITORY-URL}
$ cd ${GIT-REPOSITORY}
```

### 1.2. create sample file (on main branch)
```
$ vi 002-git-merge-branch-if-conflict.txt
---
init 002-git-merge-branch-if-conflict
---
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
```
$ git add 002-git-merge-branch-if-conflict.txt
```

#### 1.3.2. commit
```
$ git commit -m "init 002-git-merge-branch-if-conflict.txt"
[main aa4403f] init 002-git-merge-branch-if-conflict.txt
 1 file changed, 1 insertion(+)
 create mode 100644 002-git-merge-branch-if-conflict.txt
```

## 2. configure secondary branch
### 2.1. create secondary branch
```
$ git branch secondary-branch
```

### 2.2. switch secondary branch
```
$ git checkout secondary-branch
Switched to branch 'secondary-branch'
```

> create and switch branch at the same time

```
$ git checkout -b secondary-branch
```

### 2.3. show branch list
```
$ git branch
  main
* secondary-branch
```

## 3. update sample file on secondary branch
### 3.1. update sample file
```
$ vi 002-git-merge-branch-if-conflict.txt
---
init 002-git-merge-branch-if-conflict
add secondary-branch
---
```

### 3.2. record changes on secondary branch
#### 3.2.1. add file to index
```
$ git add 002-git-merge-branch-if-conflict.txt
```

#### 3.2.2. commit
```
$ git commit -m "add secondary-branch"
[secondary-branch 961da22] add secondary-branch
 1 file changed, 1 insertion(+)
```

## 4. update sample file on main branch
### 4.1. switch main branch
```
$ git checkout main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
```

### 4.2. update sample file
```
$ vi 002-git-merge-branch-if-conflict.txt
---
init 002-git-merge-branch-if-conflict
add main-branch
---
```

### 4.3. record changes on main branch
#### 4.3.1. add file to index
```
$ git add 002-git-merge-branch-if-conflict.txt
```

#### 4.3.2. commit
```
$ git commit -m "add main-branch"
[main 1d2669a] add main-branch
 1 file changed, 1 insertion(+)
```

## 5. merge secondary branch to main branch
### 5.1. merge
```
$ git merge secondary-branch
Auto-merging 002-git-merge-branch-if-conflict.txt
CONFLICT (content): Merge conflict in 002-git-merge-branch-if-conflict.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### 5.2. show sample file on main branch
```
$ cat 002-git-merge-branch-if-conflict.txt
init 002-git-merge-branch-if-conflict
<<<<<<< HEAD
add main-branch
=======
add secondary-branch
>>>>>>> secondary-branch
```

### 5.3. resolve conflict
#### 5.3.1. modify sample file
```
$ vi 002-git-merge-branch-if-conflict.txt
---
init 002-git-merge-branch-if-conflict
add main-branch
add secondary-branch
---
```

#### 5.3.2. add file to index
```
$ git add 002-git-merge-branch-if-conflict.txt
```

#### 5.3.3. commit
```
$ git commit -m "fix merge conflict"
[main b2a170d] fix merge conflict
```

### 6. updates remote refs
```
$ git push
Username for 'https://github.com': rexx4314-github-account
Password for 'https://rexx4314-github-account@github.com':
Counting objects: 12, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (12/12), 1.31 KiB | 1.31 MiB/s, done.
Total 12 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), done.
To https://github.com/rexx4314-github-account/git-merge-branch-if-conflict.git
   4d3ae2e..b2a170d  main -> main
```

## 7. show commit logs

- in main branch

```
$ git log
commit b2a170d18c2a31f98fda7105eadc0ae92ed23487 (HEAD -> main, origin/main, origin/HEAD)
Merge: 1d2669a 961da22
~
    fix merge conflict

commit 1d2669afcb1c51665ac989c5a8fcf677ff4f85e5
~
    add main-branch

commit 961da2243066f15af10cebbad47ba27cdcde5ef4 (secondary-branch)
~
    add secondary-branch

commit aa4403f69991c9607db693faa7248f9f1bcc82c6
~
    init 002-git-merge-branch-if-conflict.txt

commit 4d3ae2e4b75ab5cbee8e630afe90268c0197b043
~
    Initial commit
...
```

- in secondary branch

```
$ git log
commit 961da2243066f15af10cebbad47ba27cdcde5ef4 (HEAD -> secondary-branch)
~
    add secondary-branch

commit aa4403f69991c9607db693faa7248f9f1bcc82c6
~
    init 002-git-merge-branch-if-conflict.txt

commit 4d3ae2e4b75ab5cbee8e630afe90268c0197b043
~
    Initial commit
```

## 8. (Optional) delete secondary branch

- in main branch

```
$ git branch -d secondary-branch
Deleted branch secondary-branch (was ca6e37f).
```
