# `git add`

Add or *track* file contents to the *index* or *staging area*.

## Usage

```bash
# add one file
git add README.md

# add multiple files
git add <file1> <file2> ...

# file glob
# Add all matching files whose extension is .c
git add *.c

# add all files in a directory
git add <dir or .>

# ignore removal
# or `git add --no-all <dir>`
#
# For Older versions of Git
#   `git add <dir>` equivalent to `git add --no-all <dir>`
git add --ignore-removal <dir>
```

## References

- [Git Documentaton - `git add`](https://git-scm.com/docs/git-add)
