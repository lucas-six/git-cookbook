# Git Patch

## Usage

### Create Git Patch

```bash
... (git commit -m)
git format-patch -M <upstream-branch> <current-branch>.patch
```

### Apply Git Patch

```bash
git am <current-branch>.patch
... (git add+commit)
```

### Create Standard Patch

```bash
... (git commit)
git diff <upstream-branch> > <current-branch>.patch
```

### Apply Standard Patch

```bash
git apply --check <current-branch>.patch
git apply <current-branch>.patch
... (git add+commit)
```

## References

- [Git Documentation - `git format-patch`](https://git-scm.com/docs/git-format-patch)
- [Git Documentation - `git am`](https://git-scm.com/docs/git-am)
- [Git Documentation - `git apply`](https://git-scm.com/docs/git-apply)
