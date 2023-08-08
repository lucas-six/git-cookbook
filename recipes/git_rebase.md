# Git Rebase

## Modify commit (already commited)

Back to specified commit of current branch:

```bash
git rebase -i|--interactive <commit-id>
```

if back to the first commit (root commit) of current branch, use **`--root`**:

```bash
git rebase -i --root
```

Modify author:

```bash
git commit --amend --reset-author
```

After that, (vim) editor comes out, and you can change *`picked`* to *`edit`*, and exit vim by `:wq`:

Back to normal state:

```bash
git rebase --continue
```

At last, force to push modifications to remote repo:

```bash
git push -f
```
