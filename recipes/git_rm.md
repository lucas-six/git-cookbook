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
git rm -f|--force <file>
```

## References

- [Git Documentaton - `git rm`](https://git-scm.com/docs/git-rm)
