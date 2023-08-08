# `git add`

Add or *track* file contents to the *index* or *staging area*.

## Recipes

### Add one file

```bash
git add README.md
```

### Add Multiple Files

```bash
git add <file1> <file2>
```

### Fileglobs

```bash
# Add all matching files whose extension is .c
git add *.c
```

### Add All Files in Current Directory

```bash
git add .
```

### Add Files With Leading Directory

Add all files in the directory `dir`, e.g. `dir/file1`, `dir/file2`:

```bash
git add <dir>
```

### Ignore Removal

Option **`--ignore-removal`** equivalent to **`--no-all`**.

Update the index by adding new files that are unknown to the index and files modified
in the working tree,
but ignore files that have been removed from the working tree.

```bash
git add --ignore-removal <dir>
git add --no-all <dir>
```

## References

- [Git Documentaton - `git add`](https://git-scm.com/docs/git-add)
