# `git commit`

Record changes to the repository.

The new commit is a direct child of `HEAD`, usually the tip of the current branch,
and the branch is updated to point to it
(unless no branch is associated with the working tree, in which case `HEAD` is "detached")

## Usage

```bash
# launch an editor, which is specified by `core.editor`, to let user input the commit message
git commit

# short commit message (one of follows)
# if multiple `-m` given, their values are concatenated as separate paragraphs
git commit -m '<commit message>'
git commit --message '<commit message>'

# commit unstaged
git commit -a
git commit --all

# change the last commit, including commit message
git commit --amend

# amend a commit without changing its commit message
git commit --amend --no-edit

# override the commit author
git commit --author='xxx <xxxx@xxx.xxx>'

# change the commit author of last commit
git commit --amend --author='xxx <xxxx@xxx.xxx>'

# change the commit author of last commit without its commit message
git commit --amend --author='xxx <xxxx@xxx.xxx>' --no-edit
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

## References

- [Git Documentation - `git commit`](https://git-scm.com/docs/git-commit)
