# Git Branch

## List Branches

### List Local Branches (`-l`/`--list`) (default)

```bash
$ git branch
* main
  develop
```

The current branch will be highlighted in *green* and marked with an *asterisk* (*`*`*)

### List Remote-Tracking Branches (`-r`/`--remotes`)

```bash
$ git branch -r
origin/HEAD -> origin/main
origin/main
upstream/main
```

### List Both Local and Remote Branches (`-a`/`--all`)

```bash
$ git branch -a
* main
  develop
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
  remotes/upstream/main
```

### List Branches Verbosely (`-v`/`--verbose`)

Show sha1 and commit subject line for each head, along with relationship to upstream branch (if any):

```bash
$ git branch -v
  iss53   93b412c Fix javascript issue
* master  7a98805 Merge branch 'iss53'
  testing 782fd34 Add scott to the author list in the readme
```

### List Merged Branches (`--merged`)

Only list branches whose tips are reachable from the specified `commit` (`HEAD` if not specified):

```bash
git branch --merged [<commit>]
```

### List Un-Merged Branches (`--no-merged`)

Only list branches whose tips are not reachable from the specified `commit` (`HEAD` if not specified):

```bash
git branch --no-merged [<commit>]
```

## Create a New Branch

```bash
# `start-point` can be the *branch name*, *commit id*, *tag name*.
git branch [-f|--force] <new-branch> [<start-point>]

# track remote upstream
git branch -t|--track <branch> <remote-branch>

git branch --orphan <orphan-branch>
```

### Error

```bash
# already exists
$ git branch existed-branch
fatal: A branch named 'existed-branch' already exists.
```

## Switch Branches

```bash
git switch <another-branch>

# back to previous
git switch -

# create and switch
#   `start-point` can be the *branch name*,
#                            *commit id*,
#                            *tag name*.
git switch -c|--create <new-branch> [<start-point>]
git switch -C|--force-create <new-branch> <start-point>

# track remote upstream
git switch -c|--create -t|--track [direct|inherit] <new-branch>

git switch --orphan <new-branch>
```

### Error

```bash
# not exists
$ git switch a-branch
fatal: invalid reference: a-branch

# already exists
$ git switch -c existed-branch
fatal: A branch named 'existed-branch' already exists.
```

### Switch Branches (`git checkout`, Git 2.23-)

```bash
git checkout <another-branch>

# create and switch
git checkout -b <new-branch> [<start-point>]
git checkout -B <new-branch> <start-point>

# track remote upstream
git checkout -b -t|--track=[direct|inherit] <new-branch>

git checkout --orphan <new-branch>
```

## Rename Branches

```bash
# If branch existed: `fatal: A branch named 'new-branch' already exists.`
git branch -m|--move <old-branch> <new-branch>


# force to rename:
# `-M` = `--move --force`
git branch -M <old-branch> <existed-branch>
```

## Copy Branches

```bash
# If branch existed: `fatal: A branch named 'b-branch' already exists.`
git branch -c|--copy <old-branch> <new-branch>


# force to copy
# `-C` = `--copy, --force`
git branch -C <old-branch> <new-branch>
```

## Delete Branches

```bash
git branch -d|--delete <branch>    # fully merged branch

# force to delete
# `-D` = `--delete, --force``
git branch -D <branch>    # NOT merged branch
```

## Upstream Tracking

### Set Up Upstream Tracking

```bash
# `--set-upstream`* deprecated
git branch -u|--set-upstream-to=<remote-branch> <branch>
```

### Remove Upstream Tracking

```bash
git branch --unset-upstream <branch>
```

## Merge Branches

```bash
git merge <branch>
```

Merge a specific commit into `branch`:

```bash
git cherry-pick <commit>
```

## References

- [Pro Git v2 - 3. Git Branching](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell)
- [Git Documentation - `git branch`](https://git-scm.com/docs/git-branch)
- [Git Documentation - `git switch`](https://git-scm.com/docs/git-switch)
- [`git merge` Documentation](https://git-scm.com/docs/git-merge)
- [`git cherry-pick` Documentation](https://git-scm.com/docs/git-cherry-pick)
