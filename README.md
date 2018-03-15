# Git Cookbook

Getting started with Git, please read the Chapter 1,2,3 of [Pro Git](https://www.git-scm.com/book/en/v2).

[Bash Cookbook](https://github.com/leven-cn/bash-cookbook) should be able to help you.

```bash
git version  # v1.9.5+
```

Before start, configure it:

**System wide configuration (All users in the system)**

```bash
sudo git config --system help.autocorrect 1
sudo git config --system core.eol lf
sudo git config --system core.autocrlf input
sudo git config --system core.filemode true
sudo git config --system core.editor vim
sudo git config --system color.ui auto
sudo git config --system diff.tool vimdiff
sudo git config --system merge.tool vimdiff
sudo git config --system push.default simple
sudo git config --system credential.helper "cache --timeout=3600"
sudo git config --system gui.encoding utf-8
```

**User wide configuration**

```bash
git config --global user.name 'Li Yun'                   # Your name
git config --global user.email leven.cn@gmail.com        # Your working email, just as GitHub registered email

# Show your current configuration
git config --list

# Warning: Store your password in local host, ensure you are working in a secure environment
git config --global credential.helper store
```

---

- Quick Start
- GitHub Workflow
- Git Workflow
- Commit Message
- Undo
- Log
- Version Difference
- Delete Branch
- Tag
- Remote Branch
- Patch
- Git Server (SSH-based)

---

## Quick Start

Refer to Chapter 5,6 of [Pro Git](http://www.git-scm.com/book/).

Text files (including code and doc) in your repo should be all `UTF-8` encoded.

1. `git clone <repo-url> [<dir>]`
1. (optional)`git remote add upstream <origin-repo-url>`
1. (optional)`git pull upstream <branch>`
1. `git checkout <branch>` (default `master`) or `git checkout -b <branch>`
1. Update files
1. `git status`
1. `git diff`
1. `git diff --check`
1. `git add|rm|mv <file ... or dir>`
1. `git diff --cached`
1. `git commit -m '<commit message>'`
1. `git push` to Git Server

## GitHub Workflow

- `Fork`
- `Pull Request`: `git merge --no-ff <branch-name>`

## Git Workflow

### Git Branch Model

![](https://raw.githubusercontent.com/leven-cn/git-cookbook/master/Git-Branch-Model.png)

### Mainstream

Branch `master` contains codes only for official releases with some version tags for production.

**NOTE**: The perils of rebasing: **DONOT** `rebase` commits that you have pushed to a public repository.

```bash
git checkout master
git pull --rebase
git merge --no-ff dev

# If any upstream repo (e.g., GitHub Fork)
git remote add upstream <git-url>
git fetch upstream
git merge --no-ff upstream/master

git tag -a <tag> -m '<tag-comment>' # e.g., git tag -a 'v0.1' -m 'v0.1 - Initial version'

git push
git push --tag
```

### Bugfix for Mainstream

```bash
git checkout -b <bugfix-A> master
# ... (git add/rm)
git diff [--cached] <path ...>
git diff --check # Avoid white space issues commit
# ... (git commit -m)
git diff <bugfix-A>..master

git checkout master
git pull --rebase
git rebase <bugfix-A>
git branch -d <bugfix-A>
```

### Features

I think that it is better for same features by using `rebase`, while for different ones by using `merge`. Since it will keep the branch structure clean.

```bash
git checkout <feature-A> develop
git pull --rebase
# ... (git add/rm)
git diff [--cached] <path ...>
git diff --check # Avoid white space issues commit
# ... (git commit -m)
git diff <feature-A>..develop

git checkout develop
git pull --rebase
git merge --no-ff <feature-A>
```

### Releases

一旦`develop`分支上有了做一次发布（或者说快到了既定的发布日）的足够功能，就从`develop`分支上fork一个发布分支`release`。新建的分支用于开始发布循环，所以从这个时间点开始之后新的功能不能再加到这个分支上 —— 这个分支只应该做**Bug修复**、**文档生成**和其它面向发布任务。一旦对外发布的工作都完成了，发布分支合并到master分支并分配一个版本号打好Tag。另外，这些从新建发布分支以来的做的修改要合并回`develop`分支。


## Commit Message

```
This update contains improvement and bug fixes, including:

    - Fixed bugs where user cannot signup

    - Fixed bugs that prevent A from doing sth

    - Fixed issues that could cause B crash when ...

    - Improved reliability of C when ...

    - Improved performance of D when ..
```

## Undo

```bash
git checkout -- <file ...>      # undo updates of `git add`

git reset HEAD <file ...>       # undo `git add`

git commit --amend              # update `git commit`
```

## Log

```bash
git log

git log -p             # Show difference
git log -p -N          # Show difference among lastest N commits
```

## Version Difference

```bash
git diff <branch-A>..<branch-B>
```

## Delete Branch

```bash
git branch -d <branch-name>    # merged branch

git branch -D <branch-name>    # NOT merged branch
```

## Tag

```bash
git tag -a <tag> -m '<tag-comment>'      # e.g., git tag -a 'v0.1' -m 'v0.1 - Initial version'

git push --tag                           # Add remote tag
git push origin :refs/tags/<tag-name>    # Delete remote tag
```

## Remote Branch

```bash
git remote -v
```

### Delete Remote Branch

```bash
git push [-f] <remote-repo> :<remote-branch>
```

## Patch

### Create Git Patch
```bash
... (git commit -m)
git format-patch -M <upstream-branch> <current-branch>.patch
```

### Apply Git Patch
```bash
git am <current-branch>.patch
... (git add+commit)
```

### Create Standard Patch
```bash
... (git commit)
git diff <upstream-branch> > <current-branch>.patch
```

### Apply Standard Patch
```bash
git apply --check <current-branch>.patch
git apply <current-branch>.patch
... (git add+commit)
```


## Git Server (SSH-based)

```bash
mkdir <project>.git
cd <project>.git
git init --bare

git clone --bare <project-dir> <git-repo>.git
scp -r <git-repo>.git <user>@<git-server>:/<path-to-git-repo>

# On Git Server
sudo adduer git
sudo passwd git
ssh <user>@<git-server>
sudo adduser git
sudo passwd git
sudo chown git:git  /<path-to-git-repo>
gpasswd -a <user> git
```
