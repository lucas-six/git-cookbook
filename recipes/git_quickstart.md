# Git Quick Start

Getting started with Git, please read the Chapter 1,2,3 of [*Pro Git*](https://www.git-scm.com/book/en/).

## Git Version

Display **version information** about Git:

```bash
git version  # v2.23+
```

## Git Clone

```bash
git clone <repository-address> [<directory>]
```

**Clone** a repository into a *newly created* directory `directory` from `repository-address`.

`repository-address` is the (possibly remote) repository to clone from.
See the [[Git URL]] for more information on specifying repositories.

For example:

```bash
git clone https://github.com/leven-cn/git-cookbook.git
```

For more details for [[Git Clone]].

## Git Config

User info:

```bash
git config --global user.name 'Your Name'
git config --global user.email your@email.com  # Your working email, just as GitHub registered email
```

Editor (command line: *Vim*, *Emacs*)

```bash
git config --global core.editor vim
git config --global diff.tool vimdiff
git config --global merge.tool vimdiff
```

```bash
git config --global core.editor emacs
```

Editor (GUI: *VS Code*)

```bash
git config --global core.editor "code --wait"
git config --global diff.tool "code --wait ---diff $LOCAL $REMOTE"
```

Show your current configuration:

```bash
git config --list  # all configs

git config <name>  # specified config
```

For more details for [[Git config]].

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

For more details for [[Git add]], [[Git remove]], [[Git restore]], [[Git commit]], [[Git reset]],
[[Git diff]].

---

Before start, configure it:

```bash
sudo git config --system help.autocorrect 1
sudo git config --system core.filemode true
sudo git config --system gui.encoding utf-8
```

## More

- [Git Features](https://leven-cn.github.io/git-cookbook/recipes/git_features)

## References

- [Git Homepage](https://git-scm.com "Git Homepage")
- [Pro Git v2](https://git-scm.com/book/en/v2)
- [Git Reference](https://git-scm.com/docs)
