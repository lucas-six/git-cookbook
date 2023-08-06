# Git Branch

## Usage

```bash
# list existing local branch: `-l`/`--list` (by default)
# The current branch will be highlighted in green and marked with an asterisk (`*`)
$ git branch
* main
  develop


# list remote-tracking branches: `-r`/`--remotes`
$ git branch -r
origin/HEAD -> origin/main
origin/main
upstream/main


# show both local and remote branches: `-a`/`--all`
$ git branch -a
* main
  develop
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
  remotes/upstream/main


# Show sha1 and commit subject line for each head,
# along with relationship to upstream branch (if any): `-v`/`--verbose`
$ git branch -v
  iss53   93b412c Fix javascript issue
* master  7a98805 Merge branch 'iss53'
  testing 782fd34 Add scott to the author list in the readme


# Create a New Branch
# This creates a new *pointer* to the same commit you’re currently on.
# It didn’t switch to the new branch.
# If branch existed: `fatal: A branch named 'existed-branch' already exists.`
git branch <new-branch>
git branch --orphan <orphan-branch>


# Create a new branch to the `start-point` commit,
# and force to reset branches already existed: `-f`/`--force`
# `start-point` can be the branch name, commit id, tag name.
git branch [-f|--force] <new-branch> <start-point>


# Switch branches (one of follows)
# If branch not existed: `fatal: invalid reference: non-existed-branch`
git switch <another-branch>
git checkout <another-branch>  # Git <= 2.23


# Switch back to the previous branch
git switch -


# Create new branch if branch not existed and switch to it: `-c`/`--create`
# If branch existed: `fatal: A branch named 'existed-branch' already exists.`
git switch -c|--create [-t|--track [direct|inherit]] <new-branch>
git checkout -b [-t [direct|inherit]] <new-branch>  # Git <= 2.23


# Create new branch if branch already exists, and switch to it: `-C`/`--force-create`
# `start-point` can be the branch name, commit id, tag name.
git switch -C|--force-create <new-branch> <start-point>
git checkout -B <new-branch> <start-point>  # Git <= 2.23


git switch --orphan <new-branch>
git checkout --orphan <new-branch>  # Git <= 2.23


# Track remote
git branch --track <branch> <remote-branch>


# Only list branches whose tips are reachable from the specified `commit` (`HEAD` if not specified)
git branch --merged [<commit>]


# Only list branches whose tips are not reachable from the specified `commit` (`HEAD` if not specified)
git branch --no-merged [<commit>]
```

### Rename Branches

```bash
# rename branch: `-m`/`--move`
# If branch existed: `fatal: A branch named 'new-branch' already exists.`
git branch -m|--move <old-branch> <new-branch>


# force to rename: `-M` / `--move --force`
git branch -M <old-branch> <existed-branch>
git branch --move --force <old-branch> <existed-branch>
```

### Copy Branches

```bash
# copy branch: `-c`/`--copy`
# If branch existed: `fatal: A branch named 'b-branch' already exists.`
git branch -c|--copy <old-branch> <new-branch>


# force to copy: `-C` / `--copy, --force`
git branch -C <old-branch> <new-branch>
git branch --copy --force <old-branch> <new-branch>
```

### Delete Branches

```bash
# delete branch: `-d`/`--delete`
git branch -d|--delete <branch>    # fully merged branch


# force to delete: `-D` / `--delete, --force``
git branch -D <branch>    # NOT merged branch
git branch --delete --force <branch>    # NOT merged branch
```

### Set Up Upstream Tracking

Use option **`-u`**/**`--set-upstream-to`** (*`--set-upstream`* 废弃):

```bash
git branch --set-upstream-to=<remote-branch> <branch>
```

### Remove Upstream Tracking

Use option **`--unset-upstream`**:

```bash
git branch --unset-upstream <branch>
```

### Merge Branches

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
