# `git tag`

## List Tags

```bash
git tag
```

## Delete a Local Tag

```bash
git tag -d|--delete <tag-name>
```

## Push to Remote

```bash
git push --tag
```

## Delete Remote Tag

```bash
git push <repo-name> :refs/tags/<tag-name>
```

## Make an Unsigned, Annotated Tag Object

```bash
git tag -a|--annotate <tag-name> -m|--message '<tag-comment>'
```

## References

- [Git Documentation - `git tag`](https://git-scm.com/docs/git-tag)
- [Semantic Versioning](https://semver.org)
