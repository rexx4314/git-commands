# GIT TAG
1. initialize (configure main branch)
2. tagging (lightweight tags)
3. tagging with message (annotated tags)
4. tagging past commit
5. check out tag
6. (Optional) delete tag

## 1. initialize (configure main branch)
### 1.1. create empty git repository (main branch)
```console
$ cd ${REX-WORKSPACE}
$ git init
Initialized empty Git repository in /home/ubuntu/workspace/user/rex/git-tag/.git/
```

### 1.2. create sample file
- on main branch

```console
$ vi 005-git-tag.txt
```

```shell
init 005-git-tag
```

### 1.3. record changes to repository
#### 1.3.1. add file to index
- on main branch

```console
$ git add 005-git-tag.txt
```

#### 1.3.2. commit
- on main branch

```console
$ git commit -m "init 005-git-tag.txt"
[main (root-commit) 2ebf41c] init 005-git-tag.txt
 1 file changed, 1 insertion(+)
 create mode 100644 005-git-tag.txt
```

## 2. tagging (lightweight tags)
### 2.1. modify sample file
- on main branch

```console
$ vi 005-git-tag.txt
```

```shell
init 005-git-tag
add main-branch v2.0
```

### 2.2. record changes to repository
#### 2.2.1. add file to index
- on main branch

```console
$ git add 005-git-tag.txt
```

#### 2.2.2. commit
- on main branch

```console
$ git commit -m "add 005-git-tag.txt v2.0"
[main (root-commit) 9c96e81] add 005-git-tag.txt v2.0
 1 file changed, 1 insertion(+)
```

### 2.3. create tag
- on main branch

```console
$ git tag v2.0
```

### 2.4. show tags (list)
- on main branch

```console
$ git tag
v2.0
```

### 2.5. show tag
- on main branch

```console
$ git show v2.0
commit 9c96e816403b33785940ec6dfe18d76653d297df (HEAD -> main, tag: v2.0)
~
    add 005-git-tag.txt v2.0

diff --git a/005-git-tag.txt b/005-git-tag.txt
index 454b3f9..a18df21 100644
--- a/005-git-tag.txt
+++ b/005-git-tag.txt
@@ -1 +1,2 @@
 init 005-git-tag
+add main-branch v2.0
```

## 3. tagging with message (annotated tags)
- on main branch

### 3.1. modify sample file
- on main branch

```console
$ vi 005-git-tag.txt
```

```shell
init 005-git-tag
add main-branch v2.0
add main-branch v3.0
```

### 3.2. record changes to repository
#### 3.2.1. add file to index
- on main branch

```console
$ git add 005-git-tag.txt
```

#### 3.2.2. commit
- on main branch

```console
$ git commit -m "add 005-git-tag.txt v3.0"
[main (root-commit) 4a65335] add 005-git-tag.txt v3.0
 1 file changed, 1 insertion(+)
```

### 3.3. create tag
- on main branch

```console
$ git tag -a v3.0 -m "version 3.0"
```

### 3.4. show tags (list)
- on main branch

```console
$ git tag
v2.0
v3.0
```

### 3.5. show tag
- on main branch

```console
$ git show v3.0
tag v3.0
~
version 3.0

commit 4a65335677636b7454588580617575e67445b926 (HEAD -> main, tag: v3.0)
~
    add 005-git-tag.txt v3.0

diff --git a/005-git-tag.txt b/005-git-tag.txt
index a18df21..a4e942c 100644
--- a/005-git-tag.txt
+++ b/005-git-tag.txt
@@ -1,2 +1,3 @@
 init 005-git-tag
 add main-branch v2.0
+add main-branch v3.0
```

## 4. tagging past commit
### 4.1. show commit history
- on main branch

```console
$ git log --pretty=oneline
4a65335677636b7454588580617575e67445b926 (HEAD -> main, tag: v3.0) add 005-git-tag.txt v3.0
9c96e816403b33785940ec6dfe18d76653d297df (tag: v2.0) add 005-git-tag.txt v2.0
2ebf41ce3980e74093242d0f99625fb79c03c911 init 005-git-tag.txt
```

### 4.2. create tag
- on main branch

```console
$ git tag -a v1.0 2ebf41c
```

```shell
Version 1.0
#
# Write a message for tag:
#   v1.0
# Lines starting with '#' will be ignored.
```

### 4.3. show tags (list)
- on main branch

```console
$ git tag
v1.0
v2.0
v3.0
```

### 4.4. show tag
- on main branch

```console
$ git show v1.0
tag v1.0
~
Version 1.0

commit 2ebf41ce3980e74093242d0f99625fb79c03c911 (tag: v1.0)
~
    init 005-git-tag.txt

diff --git a/005-git-tag.txt b/005-git-tag.txt
new file mode 100644
index 0000000..454b3f9
--- /dev/null
+++ b/005-git-tag.txt
@@ -0,0 +1 @@
+init 005-git-tag
```

## 5. check out tag
### 5.1. show commit logs
- on main branch

```console
$ git log
commit 4a65335677636b7454588580617575e67445b926 (HEAD -> main, tag: v3.0)
~
    add 005-git-tag.txt v3.0

commit 9c96e816403b33785940ec6dfe18d76653d297df (tag: v2.0)
~
    add 005-git-tag.txt v2.0

commit 2ebf41ce3980e74093242d0f99625fb79c03c911 (tag: v1.0)
~
    init 005-git-tag.txt
```

### 5.2. checkout
- on main branch

```console
$ git checkout v1.0
Note: checking out 'v1.0'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 2ebf41c init 005-git-tag.txt
```

### 5.3. show commit logs
- on main branch

```console
$ git log
commit 2ebf41ce3980e74093242d0f99625fb79c03c911 (HEAD, tag: v1.0)
~
    init 005-git-tag.txt
```

## 6. (Optional) delete tag
### 6.1. show tags (list)
- on main branch

```console
$ git tag
v1.0
v2.0
v3.0
```

### 6.2. delete tag
- on main branch

```console
$ git tag -d v2.0
Deleted tag 'v2.0' (was 9c96e81)
```

### 6.3. show tags (list)
- on main branch

```console
$ git tag
v1.0
v3.0
```
