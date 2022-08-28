# `git rm`

**Remove** files from the *working tree* and from the *index* (*staging area*).

## Usage

```bash
# remove files
git rm <file1> <file2> ...

# remove files only from index/staging area
git rm --cached <file1> <file2> ...

# file glob
git rm *.c

# remove all files in a directroy
git rm -r <dir>

# remove part-staged files
#
# The files being removed have to be identical to the tip of the branch,
# and no updates to their contents can be staged in the index,
# though that default behavior can be overridden with the **`-f`**/**`--force`** option.
git rm -f <file>
```

## References

- [Git Documentaton - `git rm`](https://git-scm.com/docs/git-rm)
