# `git remote`

## List Remote

```bash
git remote [-v|--verbose]
```

## Add a Remote

```bash
git remote add <name> <url>
```

## Remove a Remote

```bash
git remote rm|remove <name>
```

## Rename a Remote

```bash
git remote rename <old-name> <new-name>
```

## Get Remote URLs

```bash
git remote get-url <name>
```

## Set Remote URLs

```bash
git remote set-url <name> <url>
```

## Fetch From Remote

```bash
git fetch
```

Speficify remote repo and/or branch:

```bash
git fetch <remote=origin> <branch=master>
```

## Pull From Remote

`git pull` = `git fetch` + `git merge`

```bash
git pull
```

Speficify remote repo and/or branch:

```bash
git pull <remote=origin> <branch=master>
```

## Push To Remote

### Default Action

```bash
git push
```

Configure default action:

```bash
git config push.default simple
```

- **`simple`**: pushes the current branch with the same name on the remote. (default)
- **`upstream`**: push the current branch back to the branch
whose changes are usually integrated into the current branch. (for central workflow)
- **`current`**: push the current branch to update a branch with the same name on the receiving end.
(for central and non-centra workflows)
- **`nothing`**: do not push anything (error out) unless a refspec is given.
This is primarily meant for people who want to avoid mistakes by always being explicit.
- **`matching`**: push all branches having the same name on both ends.

### Speficify Repo/Branch

```bash
git push <remote=origin> <branch=master>
```

### Force to Push

Disable checks:

```bash
git push -f|--force <remote=origin> <branch=master>
```

## Delete Remote Branch

```bash
git push [-f] <remote-repo> :<remote-branch>
```

## References

- [Pro Git v2 - 3.5 Git Branching - Remote Branches](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches)
- [`git remote` Documentation](https://git-scm.com/docs/git-remote)
- [`git fetch` Documentation](https://git-scm.com/docs/git-fetch)
- [`git pull` Documentation](https://git-scm.com/docs/git-pull)
- [`git push` Documentation](https://git-scm.com/docs/git-push)
