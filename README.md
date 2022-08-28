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
- [Git Configuration](https://leven-cn.github.io/git-cookbook/recipes/git_config)
- [Git URL](https://leven-cn.github.io/git-cookbook/recipes/git_url)
- [Git Clone](https://leven-cn.github.io/git-cookbook/recipes/git_clone)
- [Git Workflow](https://leven-cn.github.io/git-cookbook/recipes/git_workflow)
- [Git whitespace errors](https://leven-cn.github.io/git-cookbook/recipes/git_whitespace_errors)
- [Git Handling Line Endings (CRLF)](https://leven-cn.github.io/git-cookbook/recipes/git_line_endings)
- [`git add`](https://leven-cn.github.io/git-cookbook/recipes/git_add)
- [`git rm`](https://leven-cn.github.io/git-cookbook/recipes/git_rm)

***

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
