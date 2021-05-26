# GIT SUBMODULE
1. initialize (configure submodule repository and main repository)
2. add repository as submodule to main repository
3. clone main repository with submodule
4. update submodule
5. update main repository with option for checking submodule changes
6. submodule foreach
7. delete submodule

## 1. initialize (configure submodule repository and main repository)
### 1.1. create empty git repository (main branch of submodule repository)
```console
$ cd ${REX-WORKSPACE-SUB}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-submodule/.git/
```

### 1.2. create sample file
- on main branch

```console
$ vi 006-git-submodule.txt
```

```shell
init 006-git-submodule
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
- on main branch

```console
$ git add 006-git-submodule.txt
```

#### 1.3.2. commit
- on main branch

```console
$ git commit -m "init 006-git-submodule.txt"
[master (root-commit) 3afb77b] init 006-git-submodule.txt
 1 file changed, 1 insertion(+)
 create mode 100644 006-git-submodule.txt
```

### 1.4. create secondary branch
- on main branch

```console
$ git checkout -b secondary-branch
Switched to a new branch 'secondary-branch'
```

### 1.5. update sample file
- on secondary branch

```console
$ vi 006-git-submodule.txt
```

```shell
init 006-git-submodule
add secondary-branch
```

### 1.6. record changes to repository
#### 1.6.1. add file to index
- on secondary branch

```console
$ git add 006-git-submodule.txt
```

#### 1.6.2. commit
- on secondary branch

```console
$ git commit -m "add secondary-branch"
[secondary-branch fa8d4f2] add secondary-branch
 1 file changed, 1 insertion(+)
```

### 1.7. switch to main branch
- on secondary branch

```console
$ git checkout master
Switched to branch 'master'
```

### 1.8. add remote repository
- on main branch

```console
$ git remote add origin https://github.com/rexx4314/git-submodule.git
```

### 1.9. rename branch
- on main branch

```console
$ git branch -M main
```

### 1.10. update remote refs
- on main branch

```console
$ git push -u origin --all
Username for 'https://github.com': rexx4314
Password for 'https://rexx4314@github.com':
Counting objects: 6, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (6/6), 525 bytes | 525.00 KiB/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/rexx4314/git-submodule.git
 * [new branch]      main -> main
 * [new branch]      secondary-branch -> secondary-branch
Branch 'main' set up to track remote branch 'main' from 'origin'.
Branch 'secondary-branch' set up to track remote branch 'secondary-branch' from 'origin'.
```

### 1.11. create empty git repository (main branch of main repository)
```console
$ cd ${REX-WORKSPACE-MAIN}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-mainmodule/.git/
```

### 1.12. create sample file
- on main branch

```console
$ vi 006-git-mainmodule.txt
```

```shell
init 006-git-mainmodule
```

### 1.13. record changes to repository
#### 1.13.1. add file to index
- on main branch

```console
$ git add 006-git-mainmodule.txt
```

#### 1.13.2. commit
- on main branch

```console
$ git commit -m "init 006-git-mainmodule.txt"
[master (root-commit) 2c2e77e] init 006-git-mainmodule.txt
 1 file changed, 1 insertion(+)
 create mode 100644 006-git-mainmodule.txt
```

### 1.14. add remote repository
- on main branch

```console
$ git remote add origin https://github.com/rexx4314/git-mainmodule.git
```

### 1.15. rename branch
- on main branch

```console
$ git branch -M main
```

### 1.16. update remote refs
- on main branch

```console
$ git push -u origin --all
Username for 'https://github.com': rexx4314
Password for 'https://rexx4314@github.com':
Counting objects: 3, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 279 bytes | 279.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/rexx4314/git-mainmodule.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

## 2. add repository as submodule to main repository
### 2.1. add repository as submodule
- on main repository

```console
$ git submodule add https://github.com/rexx4314/git-submodule.git
```

### 2.2. show status
- on main repository

```console
$ git status
```

```console
$ cat .gitmodules
```

```console
$ cat .git/config
```

### 2.3. record changes to repository
- on main repository

```console
$ git commit -m "add submodule"
```

### 2.4. update remote refs
```console
$ git push origin --all
```

## 3. clone main repository with submodule
### 3.1. clone
```console
$ cd ${REX-WORKSPACE-MAIN-2}
$ git clone https://github.com/rexx4314/git-mainmodule.git
$ cd git-mainmodule
```

### 3.2. initialize submodule in main repository
- on main repository

```console
$ git submodule init
```

### 3.3. update submodule in main repository
- on main repository

```console
$ git submodule update
```

> initialize and update submodule at the same time

```console
$ git submodule update --init --recursive
```

> clone main repository and submodule repository(initialize and update) at the same time

```console
$ git clone --recurse-submodules https://github.com/rexx4314/git-mainmodule.git
```

## 4. update submodule
- on main repository

```console
$ cd ${REX-WORKSPACE-SUB-2}
$ git fetch
$ git merge origin/main
```

```console
$ git submodule update --remote
$ git submodule update --remote submodule
$ git submodule update --remote --merge
$ git submodule update --remote --rebase
```

## 5. update main repository with option for checking submodule changes
- on main repository

### 5.1. '--recurse-submodules=check'
- push if all submodule changes have been pushed

```console
$ git push --recurse-submodules=check
```

### 5.2. '--recurse-submodules=on-demand'
- push after pushing all submodule changes
- 

```console
$ git push --recurse-submodules=on-demand
```

## 6. submodule foreach
- on main repository

### 6.1. show all submodule status
```console
$ git submodule foreach 'git status'
```

### 6.2. show all submodule changes
```console
$ git submodule foreach 'git diff'
```

### 6.3. update remote refs of all submodule
```console
$ git submodule foreach 'git push'
```

## 7. delete submodule
- on main repository

> git v1.8.5 or higher version

### 7.1. unregister submodule
```console
$ git submodule deinit -f submodule
```

### 7.2. remove submodule directory
```console
$ rm -rf .git/modules/submodule
```

### 7.3. remove submodule files from index
```console
$ git rm -f submodule
```
