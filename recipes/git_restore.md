# `git restore`

Restore/Discard updates/changes/modifications of untacked or modified but not staged files.

## Usage

```bash
# restore working tree files
git restore <file1> <file2> ...

# Git <= 2.23.0
git checkout -- <file1> <file2> ...

# file glob
git restore *.c

# all files in a directory
git restore <dir or .>

# restore index files (one of follows)
git restore --staged <file or dir>
git restore -S <file or dir>
git reset HEAD <file or dir>

# restore both working tree and index files (one of follows)
git restore --worktree --staged <file or dir>
git restore -WS <file or dir>
git restore --source=HEAD --worktree --staged <file or dir>
git restore -s@ -SW <file or dir>
git checkout <file or dir>  # Git <= 2.23.0

# restore from given tree
# `HEAD` by default
git restore --source=v1.2 <file or dir>
git restore -s v1.2 <file or dir>  # `v1.2` is a tag.
```

## References

- [Git Documentation - `git restore`](https://git-scm.com/docs/git-restore)
