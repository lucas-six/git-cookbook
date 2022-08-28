# Git Quick Start

Getting started with Git, please read the Chapter 1,2,3 of [*Pro Git*](https://www.git-scm.com/book/en/).

## Git Version

Display **version information** about Git:

```bash
git version  # v2.23+
```

## Git Config

```bash
# user info
git config --global user.name 'Your Name'
git config --global user.email your@email.com  # Your working email, just as GitHub registered email

# editor/diff-tool (Command-Line: Vim)
sudo git config --system core.editor vim
sudo git config --system diff.tool vimdiff
sudo git config --system merge.tool vimdiff

# editor/diff-tool (GUI: VSCode)
git config --global core.editor "code --wait"
git config --global diff.tool "vscode"
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'

# Line Endings Issues (CRLF)
git config --global core.autocrlf input  # Local: Linux, macOS, UNIX
git config --global core.autocrlf true   # Local: Windows, Remote: non-Windows
git config --global core.autocrlf false  # Both Windows

git config --global push.default simple

sudo git config --system core.eol native
sudo git config --system core.safecrlf true
sudo git config --system core.filemode true
sudo git config --system help.autocorrect 1
sudo git config --system gui.encoding utf-8

# Show your current configuration
git config --list
```

More details to see [Git Configuration](https://leven-cn.github.io/git-cookbook/recipes/git_config).

## Git Clone

```bash
git clone https://github.com/leven-cn/git-cookbook.git
```

More details to see [Git Clone](https://leven-cn.github.io/git-cookbook/recipes/git_clone) and [Git URL](https://leven-cn.github.io/git-cookbook/recipes/git_url).

## Lifecyle

Git has three main states that your files can reside in: **modified**, **staged**, and **committed**:

- Modified means that you have changed the file but have not committed it to your database yet.

- Staged means that you have marked a modified file in its current version
to go into your next commit snapshot.

- Committed means that the data is safely stored in your local database.

![Git Lifecyle: The Three States](https://leven-cn.github.io/git-cookbook/img/git-lifecycle-noalpha.png)

This leads us to the three main sections of a Git project: the **working tree**,
the **staging area**, and the **Git directory**.

![Git Three Sections](https://leven-cn.github.io/git-cookbook/img/git-three-sections-noalpha.png)

Git has two other states: **untracked** and **unmodified**:

![Git Lifecyle: The Five States](https://leven-cn.github.io/git-cookbook/img/git-lifecycle-all.jpg)

## Basic Git Workflow

The basic Git workflow goes something like this:

- You modify files in your working tree, or discard changes (**`git restore`**).

- You selectively stage (**`git add`**, **`git rm`**, **`git mv`**, **`git restore --staged`**)
just those changes you want to be part of your next commit,
which adds only those changes to the staging area.

- You do a commit (**`git commit`**), which takes the files as they are in the staging area
and stores that snapshot permanently to your Git directory (.git directory).

```bash
# Show the working tree status
$ git status

# short status
$ git status --short
Or
$ git status -s
```

```bash
# stage modified files or directories from the working tree
git add <file ... or directory>

# remove files or directories from the working tree and from the index
git rm <file ... or directory>

# remove files or directories only from the index
git rm --cached <file ... or directory>

# rename or move a file or directory, or a symlink
git mv <source> <destination>

# commit staged files or directories to .git repository
git commit -m '<commit message>'

# commit all tracked and modified files or directories
git commit -a -m '<commit message>'
```

More details about [`git add`](https://leven-cn.github.io/git-cookbook/recipes/git_add),
[`git rm`](https://leven-cn.github.io/git-cookbook/recipes/git_rm),
[`git restore`](https://leven-cn.github.io/git-cookbook/recipes/git_restore),
[`git commit`](https://leven-cn.github.io/git-cookbook/recipes/git_commit),
[[Git reset]], [[Git diff]].

## More

- [Git Features](https://leven-cn.github.io/git-cookbook/recipes/git_features)
- [Git URL](https://leven-cn.github.io/git-cookbook/recipes/git_url)
- [Git Clone](https://leven-cn.github.io/git-cookbook/recipes/git_clone)
- [`git add`](https://leven-cn.github.io/git-cookbook/recipes/git_add)
- [`git rm`](https://leven-cn.github.io/git-cookbook/recipes/git_rm)
- [`git restore`](https://leven-cn.github.io/git-cookbook/recipes/git_restore)
- [`git commit`](https://leven-cn.github.io/git-cookbook/recipes/git_commit)

## References

- [Git Homepage](https://git-scm.com "Git Homepage")
- [Pro Git v2](https://git-scm.com/book/en/v2)
- [Git Reference](https://git-scm.com/docs)
