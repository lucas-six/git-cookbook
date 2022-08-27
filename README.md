# Git Cookbook

<section align="center">
  <img src="https://leven-cn.github.io/git-cookbook/img/git-logo.png"
    alt="Git Logo" width="512" height="214" style="text-align:center;" title="Git Logo">
  <br><br>
  <p>
    <a href="https://github.com/leven-cn/git-cookbook/actions/workflows/lint.yml">
      <img src="https://github.com/leven-cn/git-cookbook/actions/workflows/lint.yml/badge.svg"
      alt="GitHub Actions - lint" style="max-width:100%;">
    </a>
  </p>
  <p>Recipes for <code>Git</code>.</p>
  <p><a href="https://leven-cn.github.io/git-cookbook/">https://leven-cn.github.io/git-cookbook/</a></p>
</section>

**Git** is a free and open source **distributed** **version control system** (**VCS**) designed
to handle everything from small to very large projects with *speed* and *efficiency*.
Actually, it is used for *tracking changes* in any set of files,
usually used for coordinating work among programmers collaboritively developing source code
during software development, thus it is called *source code management system*, *SCM*.

Git was created by *Linus Torvalds* in *2005* for development of the Linux kernel,
with other kernel developers contributing to its initial development.
Since 2005, *Junio Hamano* has been the core maintainer.

## Recipes

- [Git Features](https://leven-cn.github.io/git-cookbook/recipes/git_features)
- [Git Quick Start](https://leven-cn.github.io/git-cookbook/recipes/git_quickstart)

***

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

***

## GitHub Workflow

Reter to:

- [GitHub Flow](http://scottchacon.com/2011/08/31/github-flow.html)
- [GitHub Flow Guide](https://guides.github.com/introduction/flow/index.html)

And follow steps:

- `Star` / `Watch`
- `Fork`
- `Pull Request`: `git merge --no-ff <branch-name>`

## Git Workflow

### Git Branch Model

Refer to Vincent Driessen's [Git Branch Model, 2010](http://nvie.com/posts/a-successful-git-branching-model/)
and [How to use a scalable Git branching model called git-flow (by Build a Module)](https://jeffkreeftmeijer.com/git-flow/)

![Git Branch Model](https://raw.githubusercontent.com/leven-cn/git-cookbook/master/Git-Branch-Model.png)

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
# ... (git add/rm/mv)
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

I think that it is better for same features by using `rebase`, while for different ones by using `merge`.
Since it will keep the branch structure clean.

```bash
git checkout <feature-A> develop
git pull --rebase
# ... (git add/rm/mv)
git diff [--cached] <path ...>
git diff --check # Avoid white space issues commit
# ... (git commit -m)
git diff <feature-A>..develop

git checkout develop
git pull --rebase
git merge --no-ff <feature-A>
```

### Releases

一旦`develop`分支上有了做一次发布（或者说快到了既定的发布日）的足够功能，就从`develop`分支上fork一个发布分支`release`。
新建的分支用于开始发布循环，所以从这个时间点开始之后新的功能不能再加到这个分支上 —— 这个分支只应该做**Bug修复**、**文档生成**和其它面向发布任务。一旦对外发布的工作都完成了，发布分支合并到master分支并分配一个版本号打好Tag。另外，这些从新建发布分支以来的做的修改要合并回`develop`分支。

### Let's Go! (GitFlow User Guide)

Read [GitFlow GitHub](https://github.com/nvie/gitflow).

```bash
git flow init [-d]
```

```bash
git flow feature/release/hotfix
git flow feature/release/hotfix start <branch-name>
git flow feature/release/hotfix finish <branch-name>

git flow feature/release/hotfix pull <reomote> <branch-name>
git flow feature/release/hotfix publish <branch-name>
```

## Commit Message

```markdown
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

## License

[MIT License](https://github.com/leven-cn/git-cookbook/blob/main/LICENSE)
