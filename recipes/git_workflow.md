# Git Workflow

## Git Branch Model

![Git Branch Model](https://leven-cn.github.io/git-cookbook/img/git-branch-model.png)

## Mainstream

Branch **`master`**/**`main`** contains codes only for official releases with some version tags for production.

**NOTE**: The perils of rebasing: **DONOT** `rebase` commits that you have pushed to a public repository.

```bash
git switch master
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

## Bugfix for Mainstream

```bash
git switch -b <bugfix-A> master
# ... (git add/rm/mv)
git diff [--cached] <path ...>
git diff --check # Avoid white space issues commit
# ... (git commit -m)
git diff <bugfix-A>..master

git switch master
git pull --rebase
git rebase <bugfix-A>
git branch -d <bugfix-A>
```

## Features

I think that it is better for same features by using *`rebase`*, while for different ones by using *`merge`*.
Since it will keep the branch structure clean.

```bash
git switch <feature-A> develop
git pull --rebase
# ... (git add/rm/mv)
git diff [--cached] <path ...>
git diff --check # Avoid white space issues commit
# ... (git commit -m)
git diff <feature-A>..develop

git switch develop
git pull --rebase
git merge --no-ff <feature-A>
```

## Releases

一旦 *`develop`* 分支上有了做一次发布（或者说快到了既定的发布日）的足够功能，就从 *`develop`* 分支上 fork/*`switch`* 一个发布分支 **`release`**。
新建的分支用于开始发布循环，所以从这个时间点开始之后新的功能不能再加到这个分支上 —— 这个分支只应该做**Bug修复**、**文档生成**和其它面向发布任务。
一旦对外发布的工作都完成了，发布分支合并到 *`master`*/*`main`* 分支并分配一个版本号打好 **`tag`**。
另外，这些从新建发布分支以来的做的修改要合并回 *`develop`* 分支。

## Let's Go! (GitFlow User Guide)

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

## References

- [Git Branch Model, 2010](http://nvie.com/posts/a-successful-git-branching-model/)
- [How to use a scalable Git branching model called git-flow (by Build a Module)](https://jeffkreeftmeijer.com/git-flow/)
- [GitFlow GitHub](https://github.com/nvie/gitflow)
- [GitHub Flow](http://scottchacon.com/2011/08/31/github-flow.html)
- [GitHub Flow Guide](https://guides.github.com/introduction/flow/index.html)
