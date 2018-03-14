# Git Cookbook

Getting started with Git, please read the Chapter 1, 2, 3 of [Pro Git](https://www.git-scm.com/book/en/v2).

```bash
git version  # v1.9.5+
```

Before start, configure it:

```bash
git config --global user.name 'Li Yun'                   # Your name
git config --global user.email leven.cn@gmail.com        # Your working email, just as GitHub registered email

# Show your current configuration
git config --list

# Warning: Store your password in local host, ensure you are working in a secure environment
git config --global credential.helper store
```

---

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

git push --tag                           # Add tag remotely
git push origin :refs/tags/<tag-name>    # Delete tag remotely
```

## Remote Branch

```bash
git remote -v
```

### Delete Remote Branch

```bash
git push [-f] <remote-repo> :<remote-branch>
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
